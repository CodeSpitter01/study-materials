# Threats vs Risks 
threats can exists without risk but a risk needs an associated threat to exist 
- the path or tool used by a malicious threat actor can be referred to as the *attack vector* 
- risks are often measured on the *probability* that an event might occur as well as the impact of the event on the business 
# Threat modelling vs Risk Assessment 
- risk assessment involves identification of security risks through the analysis of assets threats and vulnerabilities inc. their impacts and likelihood  
# Risks are *event focused* 
eg -  database server goes down 
# Threats focus on intentions 
eg - hacker wants to take down the database server 

---
Analyzing the new modern nature of cyber threats involves identifying the attributes of threat actors in terms of _locations_, *intent*, & *capability* 
# Location 
- *external threat* has no account or authorized access to the target system . eg - they use malware or social engineering to infiltrate the security system 
- *insider threat* has been granted permissions eg - employee , third party contractor 
# Intent 
- intent describes what an attacker hopes to *achieve* while motivation is the *reason* for perpetrating 
- Motivation could be driven by *greed , curiosity , or grievance*  
- Threats can be structured or unstructured . Eg- criminal gang attempting to steal financial data is a *structured targeted* threat , while a script kiddie launching a series of spam emails is *unstructured and opportunistic* 
---
# Script Kiddie 
use hacker tools without necessarily understanding how they work or have the ability to craft new attacks 
# Black Hat 
skilled , financial interests 
# White Hat 
hack systems and networks with full authorization to discover vulnerabilities 
# Grey Hat 
uses black hat tactics for white hat objectives 
# Hacktivists 
Hacking for a cause , might attempt to obtain and release confidential information to the public or deface a website 
# State Actors & Advanced Persistent Threats (APTs)
 refers to the ongoing ability of an adversary to compromise network security and maintain access by using a variety of tools and techniques
# Criminal Syndicates 
these can operate across the internet from different jurisdictions than its victim increasing the complexity of prosecution
# Insider Threats 
- compromised Employee 
- Disgruntled Employee (ex)
- Second Streamer
- spy/saboteur
- shadow it 
- unintentional 
---
# Attack Surface
this refers to all the points at which a malicious threat actor could try to exploit a vulnerability 
- attack surface for an external actor is and should be far smaller than that for an insider threat 
- minimizing the attack surface means restricting access so that only a few known endpoints , protocols/ports and services are permitted 
# Attack Vector 
- direct access 
- removable media 
- email 
- remote & wireless 
- supply chain 
- web & social media 
- cloud 
---
# Vulnerable Software 
this contains a flaw in its code or design that can be exploited to have access control or to crash the process 
Due to the complexity of modern software and the speed with which new versions must be released to market , almost no software is free from vulnerabilities 
# Unsupported Systems & Applications 
vendor no longer develops update or patches for it 
using isolation as a substitute for patch management is an example of a compensating control 
# Network Vectors 
an exploit technique for any given software vulnerability can be classed as either remote or local 
- remote means , vulnerability can be exploited by sending code to the target over a network 
- local means , the exploit code must be executed from an authenticated session on the computer 
@ unsecure network is one that lacks the attributes of CIA while a secure network uses an access control framework and cryptographic solutions to identify, authenticate , authorize and audit network users , hosts and traffic 
$ some threat vectors associated with unsecure networks are 
1. Direct Access- getting physical access to an unlocked workstation, stealing a PC or maybe using a boot disk to install malicious tools 
2. Wired Network- a threat actor attaches an unauthorized device to a physical network port and is able to launch eavesdropping or Dos attacks 
3. Remote & Wireless Network- the attacker either obtains creds for a remote access or wireless connection to the network or cracks the security protocols used for authentication 
4. Cloud Access- the attacker is likely to target the accounts used to develop services in the cloud or manage cloud systems . They may also try to attack the cloud service provider as a way of accessing the victim system 
5. Bluetooth Network- the threat actor exploits a vulnerability or misconfiguration to transmit a malicious file to a user's device over the bluetooth personal area wireless networking protocol 
6. Default Creds- the attacker gains control of a network device or app because it has been left configured with a default password
7. Open Service Port- the threat actor is able to establish an unauthenticated connection to a logical TCP or UDP network port 
---
# Lure 
this is something superficially attractive that causes its target to want it even though it may be concealing something dangerous 
- Removable Device
- Executable File 
- Document Files 
- Image Files 
# Message Based Vectors 
- email
- SMS 
- Instant Messaging 
- Web & Social Media 
The most powerful exploits are zero-click which means that simply receiving an attachment or viewing an image on a webpage can trigger the exploit  
# Vendor Management
is the process of choosing supplier companies and evaluating the risks inherent in relying on a third party product or service 
- risk cannot be wholly transfered to the vendor . If a vendor suffers a data breach , you may be able to claim costs from them but your company will still be held liable in terms of legal penalties and damage to reputation 
- *system integration* refers to the process of using components/services from multiple vendors to implement a business workflow 
- when vendor has become deeply embedded within a workflow , lack of vendor support can be serious as retooling the workflow with a new vendor can be a long and complex process 
# Data Storage 
- vendor may need to be granted access to your data 
- vendor may have to be used to host the data or the data backups 
# Precautions to be taken 
- ensure the same protections for data as though it were stored on premises 
- monitor and audit third-party access to the data 
- evaluate compliance impacts from storing personal data on a third party system 
# Cloud based vs On-premises risks 
1. On-premises risks refer to vulnerabilities and 3rd part issues arising from endpoints located in the company building 
2. clouds operate a shared responsibility model meaning that the cloud service provider is responsible for the security of the cloud , while the cloud consumer is responsible for security in the cloud 
# Social Engineering 
1. Lunchtime Attack - employee does not log off before leaving the workstation for lunch 
2. Piggy Backing - an attacker enters a secure building with the permission of an employee  
3. Tailgating - the attacker without access authorization closely follows an authorized person in a reserved area 
4. Shoulder Surfing - obtaining sensitive information by spying 
5. Dumpster Diving - obtaining sensitive information by going through the company trash 
# Prevention 
- be observant 
- ask questions 
- sensitive files should be properly shredded 
# Impersonation 
using stolen credentials to infiltrate a network 
# Credential Harvesting 
using phishing emails and spamming campaigns to gather information which can then be sold 
software, programs, scripts and malware are typically used 
# Pharming 
redirecting victims to a malicious website DNS cache poisoning 
# Water Hole Attack 
an attack that aims to compromise a specific group of end-users by infecting existing websites or creating a new one that will attract them 
# Typo Squatting / URL hijacking 
hackers register misspelled domain names of popular websites hoping to capture sensitive information . eg - fackbook.com , instagarm.com
# Influence Campaigns 
a major program launched by an adversary with a high level of capability such as a nation-state actor or terrorist group 
the goal is to shift public opinion on some topic and when deployed along with espionage , disinformation/fake news and hacking , it can be characterized as *Hybrid Warfare* 
