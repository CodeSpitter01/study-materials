# Identity Access Management 
an access control system is the set of technical controls that govern how subjects may interact with objects which could be networks, servers, databases 
# 4 main processes 
- Identification - creating an account or ID that uniquely represents the user or device on the network 
- Authentication - proving that a subject is who or what they claim to be when attempting to access a resource 
- Authorization - determining what rights subjects should have on each resource 
- Accounting - tracking authorized usage of a resource and alerting when unauthorized use is detected or attempted 
The servers and protocols that implement these functions are referred to as authentication , authorization and accounting (AAA) 
# something you know authentication 
this includes passwords , passphrases or PINs . A *knowledge*factor is also used for account reset mechanisms 
an *ownership* factor means that the account holder possess something that no one else does such as a smart card , hardware token or smartphone 
# something you are/do authentication
a *biometric* factor uses either physiological identifiers like fingerprints or behavioral identifiers such as the way someone walks talks 
# multifactor authentication 
this requires a combination of different technologies 
# authentication design 
this refers to selecting a technology that satisfies the CIA requirements 
# Biometric Authentication 
the first step is enrollment and the chosen biometric is scanned by a biometric reader and coverted to binary information
1. False Rejection Rate (FRR) - where a legitimate user is not recognized . also referred to as a type1 error or false no-match rate 
2. False Acceptance Rate (FAR) - where an interloper is accepted . also referred to as type2 error or false match rate 
3. Crossover Error Rate (CER) - the point at which FRR and FAR meet . the lower the CER the more efficient and reliable the technology 
# Fingerprint & Facial recognition 
most widely used as it's inexpensive and non-intrusive 
# Behavioral Technology 
a template is created by analyzing a behavior such as typing or walking 
- voice recognition
- gait analysis 
- signature recognition 
- typing 
# Account Password Policy 
local_security_policy > security_setting > account_policies > password_policy & account_lockout_policy
# Access Control Schemes 
an important consideration when designing a security system is to determine how users receive rights or permissions . the different model are referred to as *access control schemes* 
# Discretionary Access Control (DAC) 
this is based on the primacy of the resource owner and this means the owner has full control over the resource and can decide who to grant rights to . it is very flexible but also the easiest to compromise as it's vulnerable to insider threats and abuse of compromised accounts 
# Role-Based Access Control (RBAC)
this adds an extra degree of centralized control to the DAC model where users are not granted rights explicitly (assigned directly) but rather implicitly (through assigned a role) 
RBAC can be partially implemented through the use of security group accounts  
# File System Permissions 
with file system security , each object in the file system has an ACL associated with it . The ACL contains a list of accounts allowed to access the resource and each record in the ACL is called an *access control entry (ACE)*
in *LINUX* , there are three basic permissions - read (r) , write (w) , execute (x) 
`d rwxr-xr-x home` --> owner has (r,w,x) and other have (r,x) 
`chmod` command is used to modify permissions 
symbolic mode --> (r,w,x)  ; absolute mode --> (r=4 , w=2 , x=1) {example above can be written as --> `chmod 755 home` }
# Mandatory Access Control (MAC) 
this is based on the idea of security clearance levels (labels) instead of ACLs . In a hierarchical one , subjects are only permitted to access objects at their own clearance level or below ! 
the labelling of objects and subjects takes place using pre established rules which cannot be changed by any subject account and are therefore non-discretionary 
subjects are not permitted to change their own label 
# Attribute-Based Access Control (ABAC) 
this is capable of making access decisions based on a combination of subject and object attributes plus any system-wide attributes 
this system can monitor the number of events or alerts associated with a user account or track resources to ensure they are consistent in terms of timing of requests 
# Rule Based Access Control 
This is a term that can refer to any sort of access control model where access control policies are determined by system-enforced rules rather than system users rg -RBAC , ABAC , MAC
# Conditional Access 
this monitors account or device behavior throughout a session . If certain conditions are met , the account may be suspended or the user might need to reauthenticate 
the *user account control (uac)* and sudo restrictions on privileged accounts are examples of conditional access 
# Privileged Access Management 
a privileged account is one that can make significant configuration to a host  
# Directory Services 
these are the principal means of providing privilege management and authorization on an enterprise network as well as storing information about users, security groups and services 
the *lightweight directory access protocol* (LDAP) is a protocol widely used to query and update X.500 format directories 
type of attributes , what information they contain and the way object types are defined through attributes is described by the directory schema 
- CN - common name 
- OU - organizational unit 
- C - country 
- DC - domain component 
# Federation & Attestation
this is the notion that a network needs to be accessible to more than just a well-defined group of employees 
In business , a company might need to make parts of its network open to partners , suppliers and customers 
federation means that the company trusts accounts created and managed by a different network 
eg - user might want to use both google and twitter . and if both companies establish a federated network , user can log on to twitter using google credentials 
# Identity Providers & Attestation 
in these models , the networks perform federated identity management . A user from one network is able to provide attestation that prove their identity 
# Security Assertions Markup Language (SAML) 
implement user identity assertions and transmit attestations between the principal , relying party and identity provider . 
the saml authorizations are written in extensible markup language (xml) and communications are established using http/https and the simple object access protocol (SOAP) 
# OAUTH and OPENID Connect 
many public clouds use application programming interfaces (APIs) based on Representational State Transfer (REST) rather than SOAP 
authentication and authorization for a *RESTful* API is often implemented using the Open Authorization (OAuth) protocol 
OAuth is designed to facilitate sharing of information within a user profile between sites 
the user account is hosted by one or more resource servers. A single authorization server can manage multiple resource servers 
# Account Attributes 
a user account is defined by a unique security identifier (SID) , a name and a credential . Each account is associated with a profile which can be defined with custom identity attribute describing the user , such as fill name , email address , contract number 
# Access Policies 
each account can be assigned permissions over files and other network resources . these permissions might be assigned directly to the account or inherited through membership of a security group of role 
on a windows active directory network access policies can be configured via *group policy objects (GP0s)* 
# Location Based Policies 
a user or device can have a logical network loction identified by an IP address which can be used as an account restriction mechanism 
geo location of a user or device can be calculated using --> 
- Ip address 
- Location Services 
*Geofencing* refers to accepting or rejecting access requests based on location 
# Time Based Restrictions 
there are three main types of time-based policies 
- A time of day policy established authorized logon hours for an account 
- A time based login policy established the maximum amount of time an account may be logged in for 
- an impossible travel time/risky login policy tracks the location of login events over time 
# Account Permissions 
too many restrictions --> less productivity ; too many privileges --> weakens the security of a system 
"authorization creep" -- when employee gains more and more access privileges the longer they remain with the organization 
A user may be granted elevated privileges temporarily (escalation)  
# Account & Usage Audits 
Accounting and auditing processes are used to detect whether an account has been compromised or is being misused 
Usage auditing means configuring the security log to record key indicators and then reviewing the logs for suspicious activity 
@ some categories that get logged include > 
- account logon and management events 
- process creation 
- object access (file systems / file shares)
- changes to audit policy 
- changes to system security and integrity 
# Account Lockout & Disablement 
if account misuse is detected or suspected , the account can be manually disabled by setting an account property . an account lockout means that login is prevented for a period 
# Local Network Authentication 
@ Windows Authentication 
- windows local sign-in , the local security authority (LSA) compares the submitted credential to a hash stored in the security Accounts Manager (SAM) database  
- windows network sign-in , the LSA can pass the credentials for authentication to a network service either Kerberos or NT LAN Manager (NTLM) authentication 
- Remote sign-in , if the user's device is not connected to the local network authentication can take place over some type of virtual private network (VPN) or web portal
@ Linux Authentication 
- local user account names are stored in `/etc/passwd` , when a user logs in to a local interactive shell , the password is checked against a hash stored in /etc/shadow 
- a pluggable authentication module (PAM) is a package for enabling different authentication providers 
@ Single Sign-On (SSO)
This system allows the user to authenticate once to a local device and be authenticated to compatible application servers without having to enter credentials again 
in windows , SSO is provided by the 'Kerberos' framework
# Kerberos Authentication 
kerberos is a single sign on network authentication and authorization protocol used on many networks notably as implemented by Microsoft's Active Directory (AD) service 
this protocol is made up of 3 parts 
- KDC 
- Principal 
- Application Server 

the client sends the authentication service (AS) a request for a Ticket Granting Ticket (TGT) and its time-stamped 
- TGT , the contains information about the client (name & IP address) and a validity period . This is encrypted using KDC's secret key 
- TGS session key for use in communication between the client and the TGS , this is encrypted using a hash of the user's password 