2025-08-24 23:04

Status:

Tags:

# Cryptography
“Cryptography” comes from the Greek words kryptos, meaning “concealed, hidden, veiled, secret, or mysterious,” and graphia, meaning “writing”; thus, cryptography is “the art of secret writing.”

- Cryptography Process
Plaintext (readable format) is encrypted by means of encryption algorithms such as RSA, DES, and AES, resulting in a ciphertext (unreadable format) that, on reaching the destination, is decrypted into readable plaintext.
![[Pasted image 20250824230845.png]]
### Types of Cryptography
Cryptography is categorized into two types according to the number of keys employed for encryption and decryption:
####  Symmetric Encryption 
Symmetric encryption requires that both the sender and the receiver of the message possess the same encryption key. The sender uses a key to encrypt the plaintext and sends the resultant ciphertext to the recipient, who uses the same key (used for encryption) to decrypt the ciphertext into plaintext. Symmetric encryption is also known as secret-key cryptography, as it uses only one secret key to encrypt and decrypt the data. This type of cryptography works well when you are communicating with only a few people. Because the sender and receiver must share the key before sending any messages, this technique is of limited use for the Internet, where individuals who have not had prior contact frequently require a secure means of communication. The solution to this problem is asymmetric encryption (public-key cryptography).
![[Pasted image 20250824231155.png]]
#### Asymmetric Encryption
The concept of asymmetric encryption (also known as public-key cryptography) was introduced to solve key-management problems. Asymmetric encryption involves both a public key and a private key. The public key is publicly available, whereas the sender keeps the private key secret. An asymmetric-key system is an encryption method that uses a key pair comprising a public key available to anyone and a private key held only by the key owner, which helps to provide confidentiality, integrity, authentication, and nonrepudiation in data management.
1. An individual finds the public key of the person he or she wants to contact in a directory.
2. This public key is used to encrypt a message that is then sent to the intended recipient.
3. The receiver uses the private key to decrypt the message and reads it. 
![[Pasted image 20250824231330.png]]

###  Ciphers 
In cryptography, a cipher is an algorithm (a series of well-defined steps) for performing encryption and decryption. Encipherment is the process of converting plaintext into a cipher or code; the reverse process is called decipherment. A message encrypted using a cipher is rendered unreadable unless its recipient knows the secret key required to decrypt it. Communication technologies (e.g., Internet, cell phones) rely on ciphers to maintain both security and privacy. Cipher algorithms may be open-source (the algorithmic process is in the public domain while the key is selected by a user and is private) or closed-source (the process is developed for use in specific domains, such as the military, and the algorithm itself is not in the public domain). Furthermore, ciphers may be free for public use or licensed. 

#### Types of ciphers
![[Pasted image 20250824232158.png]]
Ciphers are of two main types: classical and modern. 

#####  Classical Ciphers 
Classical ciphers are the most basic type of ciphers, which operate on letters of the alphabet (A–Z). These ciphers are generally implemented either by hand or with simple mechanical devices. Because these ciphers are easily deciphered, they are generally unreliable.

- Types of classical ciphers 
- Substitution cipher: The user replaces units of plaintext with ciphertext according to a regular system. The units may be single letters, pairs of letters, or combinations of them, and so on. The recipient performs inverse substitution to decipher the text. Examples include the Beale cipher, autokey cipher, Gronsfeld cipher, and Hill cipher. For example, “HELLO WORLD” can be encrypted as “PSTER HGFST” (i.e., H=P, E=S, etc.).
- Transposition cipher: Here, letters in the plaintext are rearranged according to a regular system to produce the ciphertext. For example, “CRYPTOGRAPHY” when encrypted becomes “AOYCRGPTYRHP.” Examples include the rail fence cipher, route cipher, and Myszkowski transposition.
##### Modern Ciphers
Modern ciphers are designed to withstand a wide range of attacks. They provide message secrecy, integrity, and authentication of the sender. A user can calculate a modern cipher using a one-way mathematical function that is capable of factoring large prime numbers. 
- Types of Modern ciphers
- Based on the type of key used 
	- Symmetric-key algorithms (Private-key cryptography): Use the same key for encryption and decryption.
	- Asymmetric-key algorithms (Public-key cryptography): Use two different keys for encryption and decryption.
-  Based on the type of input data
	-  Block cipher: Deterministic algorithms operating on a block (a group of bits) of fixed size with an unvarying transformation specified by a symmetric key. Most modern ciphers are block ciphers. They are widely used to encrypt bulk data. Examples include DES, AES, IDEA, etc. When the block size is less than that used by the cipher, padding is employed to achieve a fixed block size.
	- Stream cipher: Symmetric-key ciphers are plaintext digits combined with a key stream (pseudorandom cipher digit stream). Here, the user applies the key to each bit, one at a time. Examples include RC4, SEAL, etc.

### Symmetric Encryption Algorithms 
The table below shows specified symmetric encryption algorithms, including information such as cipher type, key size, block size, and application areas.
![[Pasted image 20250824232801.png]]

### Cryptography Toolkits 
- open SSL 
### PGP encryption 
(“Pretty Good Privacy”)
-  When a user encrypts data with PGP, PGP first compresses the data.
Compressing the data reduces patterns in the plaintext that could be exploited by most cryptanalysis techniques to crack the cipher, thereby increasing the resistance to cryptanalysis considerably.
-  PGP then creates a random key (GSkAQk49fPD2h) that is a one-time-only secret key. 
- PGP uses the random key generated to encrypt the plaintext, resulting in a ciphertext. 
- Once the data is encrypted, a random key is encrypted with the recipient’s public key.
- The public-key-encrypted random key (Td7YuEkLg99Qd0) is sent along with the ciphertext to the recipient.
### Encrypting Email Messages in Outlook 
To perform these steps, a signing certificate should be attached to the keychain. 
- Select File → Options → Trust Center → Trust Center Settings.
- Choose the Email Security option from the left pane. 
- In the Encrypted email section, click on the Settings option beside Default Setting. 
- In the Change Security Settings pop-up window, under the Certificates and Algorithms section, choose the S/MIME certificate for the Signing certificate and Encryption certificate options and click OK.
### Email Encryption Tools 
Some important email encryption tools used to secure email messages are as follows: 
- RMail
-  Mailvelope (https://mailvelope.com) 
- Virtru (https://www.virtru.com) 
- WebrootTM (https://www.webroot.com) 
- Secure Email (S/MIME) Certificates (https://www.ssl.com) 
- Proofpoint Email Protection (https://www.proofpoint.com) 
- Paubox (https://www.paubox.com)

### Disk Encryption
#### Disk Encryption Tools 
-  VeraCrypt
-  Rohos Disk Encryption
-  BitLocker Drive Encryption
- Symantec Encryption (https://www.broadcom.com) 
- SafeGuard Enterprise Encryption (https://www.sophos.com) 
- GiliSoft Full Disk Encryption (https://www.gilisoft.com) 
- Check Point Full Disk Encryption (https://www.checkpoint.com) 
- DiskCryptor (https://diskcryptor.org)

#### Disk Encryption Tools for Linux 
- Cryptsetup
-  Cryptmount (https://cryptmount.sourceforge.net) 
- Tomb (https://dyne.org) 
- CryFS (https://www.cryfs.org) 
- GnuPG (https://www.gnupg.org) 
- Harmony Endpoint (https://www.checkpoint.com)
#### Disk Encryption Tools for macOS 
- FileVault
- VeraCrypt (https://www.veracrypt.fr) 
- BestCrypt Volume Encryption (https://www.jetico.com) 
- Dell Full Disk Encryption (https://www.dell.com) 
- Comodo Disk Encryption (https://www.comodo.com) 
- GravityZone Full Disk Encryption (https://www.bitdefender.com)

### Blockchain
A blockchain is a type of distributed ledger technology (DLT) that is used to record and store the history of transactions securely in the form of blocks. Data recorded in blockchains is resistant to unwanted modifications, and account transparency is maintained through cryptographic techniques. For multiple transactions, multiple blocks are created, which are cryptographically linked together to form a “blockchain.” 
##  Cryptanalysis
tackers may implement various cryptography attacks to evade the security of a cryptographic system by exploiting vulnerabilities in code, ciphers, cryptographic protocols, or key management schemes. This process is known as cryptanalysis. 
### Cryptanalysis Methods
#### Linear Cryptanalysis
- Commonly used on block ciphers •
- It is a known plaintext attack and uses a linear approximation to describe the behavior of the block cipher
- Given sufficient pairs of plaintext and corresponding ciphertext, bits of information about the key can be obtained
-  For example, with a 56-bit DES key, brute force could take up to 256 attempts

#### Differential Cryptanalysis
- Differential cryptanalysis is a form of cryptanalysis applicable to symmetric key algorithms
- It is the examination of differences in an input and how that affects the resultant difference in the output
- It originally worked only with chosen plaintext It can now also work with known plaintext and ciphertext only
####  Integral Cryptanalysis
- This attack is useful against block ciphers based on substitution-permutation networks, an extension of differential cryptanalysis
- Integral analysis, for block size b, holds b-k bits constant and runs the other k through all 2k possibilities
- For k=1, this is just differential cryptanalysis, but with k>1 it is a new technique


#### Quantum Cryptanalysis
-  Quantum cryptanalysis is the process of cracking cryptographic algorithms using a quantum computer
-  To perform cryptanalysis, attackers must obtain the encrypted content, and the process requires significant time and quantum resources such as Circuit Width, Circuit Depth, Number of Gates, Number of T-Gates, T-Depth, and MAXDEPTH
 
### Brute-Forcing VeraCrypt Encryption 
Steps to Brute-force VeraCrypt Encryption Using hashcat 
1.  Extract VeraCrypt Hash 
	* ``dd.exe if=<path_to_container> of=<path_to_hashfile.tc> bs=512 count=1 ``
2. hash will be used for brute forcing.
	- Crack the Hash value using hashcat 
	- Run the following command for brute-forcing a 4-digit numeric password:
		- `` hashcat.exe -a 3 -w 1 -m 13721 <path_to_hashfile.tc> ?d?d?d?d``
3.  brute forcing with a wordlist.txt file containing default passwords:
	- ``hashcat.exe -w 1 -m 13721 hash.tc wordlist.txt``

### Cryptanalysis Tools
-  CrypTool 
-  RsaCtfTool (https://github.com) 
- Msieve (https://sourceforge.net) 
- Cryptol (http://cryptol.net) 
- CryptoSMT (https://github.com) 
- MTP (https://github.com)
####  Online MD5 Decryption Tools
- MD5 Decrypter (https://www.dcode.fr) 
- MD5 Decrypt (https://iotools.cloud/tool) 
- Md5 Encrypt & Decrypt (https://md5decrypt.net) 
- MD5Hashing.net (https://md5hashing.net) 
- MD5 Encrypt/Decrypt (https://10015.io) 
- MD5 Decryption (https://www.md5online.org) 
- MD5Decrypter.com (https://www.md5decrypter.com) 
- Online Hash Crack (https://www.onlinehashcrack.com) 
- Md5.My-Addr.com (https://md5.my-addr.com)
-  Cmd5 (https://www.cmd5.org) 
- Hashes (https://hashes.com) 
- Online MD5 Hashed Validator (https://www.javainuse.com) 
- MD5 Hash Decode (https://md5.web-max.ca) 
- MD5 Decrypt (https://allinone.tools) 
- GettHIT.com (https://www.getthit.com)


# Lab 1: Encrypt the Information using Various Cryptography Tools
## Task 1: Perform Multi-layer Hashing using CyberChef
- open windows 11
1. create txt file add this **My Account number is 0234569198**) and save 
2. open browser and go to cybercheif wesite  
3. ck on **Open file as input** button present at the top of the **Input** section.
4.  we will calculate MD5 hash of the **Secret.txt** file we will calculate MD5 hash of the **Secret.txt** file
	-  **Operations** section, type md5 and drag **MD5**
5.  search for **sha1** and drag **SHA1** from the **Operations** section to **Recipe** section ensure the number of rounds is **80**.
6. we will add **HMAC** as another layer of hash
7.   In addition, we can set break point to the hash operation by clicking on the **Set breakpoint** button present in the Recipe.
8. We can also disable a hash operation by clicking the **Disable Operation** button present in the Recipie.

## Task 2: Perform File and Text Message Encryption using CryptoForge
- open windows 11 
	- cd to ``E:\CEH-Tools\CEHv13 Module 20 Cryptography\Cryptography Tools\CryptoForge and`` Right-click the **Confidential.txt** file and click **Show more options** and select **Encrypt** from the context menu.
	- we are using this file ``Confidential.txt``
1. **Enter Passphrase - CryptoForge Files**
	- password used is ``qwerty@1234``
- open windows 2019 server cd to ``Z:\CEHv13 Module 20 Cryptography\Cryptography Tools\CryptoForge``
1. open ``Confidential.txt``
- open windows 2019
1. search and open  ``CryptoForge Text``
2. type any text in fildes and click encrypt 
3. enter the password as test@123
	1. save file -> file -> save 
- open windows 11 cd to ``E:\CEH-Tools\CEHv13 Module 20 Cryptography\Cryptography Tools\CryptoForge``
	- -CryptoForge Text
1. open file which you have save
2. click  decrypt 
3.  Enter Passphrase
. What is the extension of the encrypted file?
- ``.cfd`` for txt 
- ``.cfe`` for file  

# Lab 2: Create a Self-signed Certificate
## Task 1: Create and Use Self-signed Certificates

- open windows 2019 server  
1. open browser and go to ``https://www.goodshopping.com``
	- As you are using an https channel to browse the website, it displays a page stating that **Unable to connect**.
2. search and open ``Internet Information Services (IIS) Manager``
	-  (**SERVER2019 (SERVER2019\Administrator**))
3. double-click **Server Certificates** in the **IIS** section.
	- click **Create Self-Signed Certificate** from right-hand **Actions**
4. type **GoodShopping** in the **Specify a friendly name for the certificate** field. Ensure that the **Personal** option is selected in the **Select a certificate store for the new certificate**
5.  **Sites** node from the left, and select **GoodShopping** . Click **Bindings** from the right **Actions
![16O.jpg](https://labondemand.blob.core.windows.net/content/lab168802/instructions255479/16O.jpg)

6. **Site Bindings** window appears; click **Add**
	1.  **Host name** field, type **www.goodshopping.com**. Under the **SSL certificate** field, select **GoodShopping**
	2.  Choose the **IP address** on which the site is hosted (here, **10.10.1.19**).
	3.  right click on site Goodshopping and refresh  

# Lab 3: Perform Disk Encryption
## Task 1: Perform Disk Encryption using VeraCrypt
- open windows 11
1. search and open VeraCrypt
	- create volume  **Create an encrypted file container** 
2. **Volume Type** wizard, keep the default settings
3. **Volume Location**, click **Select** **File…**.
	- location (here, **Desktop**), provide the **File name** as **MyVolume**, and click **Save**.
4. **Encryption Options** wizard, keep the default settings
5. **Volume Size**, ensure that the **MB**  is selected and  size of the VeraCrypt container as **5**
 6. **Volume Password** -> password as ``qwerty123``
	- done with creating volume 
7. **VeraCrypt** main window appears; select a drive (here, **I:**) and click **Select File**
	1. **Select a VeraCrypt Volume** window appears; navigate to **Desktop**, click **MyVolume**
	2. selected **volume** under the Volume field; then, click **Mount**.
		-  **Enter password** : qwerty123
8. Create a text file on **Desktop** and name it **Test**. Open the text file and insert text.
	- Copy the file from **Desktop** and paste it into **Local Disk** (**I:**)
9. VeraCrypt window, click **Dismount**, and then click **Exit**.
### Brute-Forcing VeraCrypt Encryption 
Steps to Brute-force VeraCrypt Encryption Using hashcat 
1.  Extract VeraCrypt Hash 
	* ``dd.exe if=<path_to_container> of=<path_to_hashfile.tc> bs=512 count=1 ``
2. hash will be used for brute forcing.
	- Crack the Hash value using hashcat 
	- Run the following command for brute-forcing a 4-digit numeric password:
		- `` hashcat.exe -a 3 -w 1 -m 13721 <path_to_hashfile.tc> ?d?d?d?d``
3.  brute forcing with a wordlist.txt file containing default passwords:
	- ``hashcat.exe -w 1 -m 13721 hash.tc wordlist.txt``

# Lab 4: Perform Cryptography using AI

## Task 1: Perform Cryptographic Techniques using ShellGPT
- open parrot 
1. give prompt to chat gpt as 
	- ``--shell "Calculate MD5 hash of text 'My Account number is 0234569198'"**``
	- command 
		- ``echo -n 'My Account number is 0234569198' | md5sum | awk '(print $1}'``
2. perform multi-layer hashing
	- ``sgpt --shell "Calculate MD5 hash of text 'My Account number is 0234569198' and calculate the SHA1 hash value of the MD5 value"``
	- command 
		- ``echo -n 'My Account number is 0234569198' | mdSsum | awk '(print $1)' | xargs echo -n | shalsum | awk '{print $1}"``

3. calculate hash of a file -crc32
	- ``sgpt --chat hash --shell "Calculate CRC32 hash of the file passwords.txt located at /home/attacker"``
	- command 
		- ``crc32 /home/attacker/passwords.txt``
4. basic encryption
	- ``sgpt --shell "Encrypt 'Hello World' text using base64 algorithm and save the result to Output.txt file"``
	- command 
		- ``echo  'Hello world' | base64 > Output.txt``
5. decrypt the encrypted data
	- ``sgpt --shell "Decrypt the contents of encrypted Output.txt file located at /home/attacker using base64 algorithm"``
	- command 
		- ``base64 -d Output.txt > Decrypted.txt `` 



PhoneSploit-Pro

## BCTextEncoder
 **BCtetx.txt**

13. In Windows : open password file **pawned.txt** in /**Documents**. Open **BCTextEncoder.exe** in E :/CEH-Tools/CEHv13 Module 20 Cryptography/Cryptography Tools/BCTextEncoder


## CRC value 
Deep CRC Search (Without apktool)

Method A: Check ZIP Metadata

unzip -v org_malwarebytes_antimalware.apk | awk ‘{print $1,$8}’ | grep -i « 614c »

This filters CRC values and filenames, showing matches ending with 614c.

Method B: Hex Dump Analysis

If the CRC is hidden in binaries:

xxd org_malwarebytes_antimalware.apk | grep -i « 614c »

Look for patterns like ____614c in the hex output.

Method C: Extract and Search All Files

unzip org_malwarebytes_antimalware.apk -d extracted_apk

grep -r -a « 614c » extracted_apk/  # -a treats binaries as text

4. Focus on Key Areas

If the above fails, the CRC might be in:

Native libraries:

strings extracted_apk/lib/*/*.so | grep -i « 614c »

Certificate metadata:

keytool -printcert -file extracted_apk/META-INF/CERT.RSA | grep -i « 614c »

Resource files:

grep -r -a -o « [0-9a-f]\{8\} » extracted_apk/ | grep -i « 614c$ »

5. Alternative Tools

If standard tools fail: Install apktool (recommended):

sudo apt install apktool

apktool d org_malwarebytes_antimalware.apk

grep -r « 614c » org_malwarebytes_antimalware/

##  cryptanalysis

### References
