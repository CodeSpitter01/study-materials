# Cryptography 
a secure communication technique that allows only the sender and receiver of a message to view it 
# Terminologies 
- Plaintext - an unencrypted message 
- Ciphertext - an encrypted message 
- Cipher - the process (algo) used to encrypt and decrypt a message 
- Cryptanalysis - the art of cracking cryptographic systems 
# Cryptographic algorithms - 
1. Hashing algorithm -->  the simplest type of cryptographic operation and produces a fixed length string from an input plaintext that can be of any length  . The output can be referred to as a checksum, message, digest or hash 
	- Hashing Collision - this occurs when two different plain texts produce the exact same hash value 
	- hashing algorithm , are used to verify the integrity of a file or password 
	- Secure Hash Algorithm (SHA) - considered to be the strongest algorithm with the most popular being the SHA-256 which produces a 256-bit digest 
	- Message Direct Algorithm (MD5) - produces a 128-bit digest 
	- Downgrade Attack - Before two devices communicate securely , both sides must first decide on the best possible encryption algo to use . Imagine if the attacker was able to sit in between both devices and influence the conversation by downgrading the encryption algorithm that can be broken easily 
- Encryption algorithm is a type of cryptographic process that encodes data so that it can be recovered or decrypted 
- The use of a *key* with the encryption cipher ensures that decryption can only be performed by authorized persons .
1. Symmetric encryption cipher - Here both encryption and decryption are performed by the same secret key and can be used for confidentiality 
	- it is very fast and is used for bulk encryption of large amounts of data but can be vulnerable if the key is stolen 
	- cannot be used for authentication or integrity 
	- Stream Cipher - each byte or bit of data is encrypted one at a time 
	- Block Cipher - the plaintext is divided into equal size blocks (usually 128 bit) . if there is not enough data in the plaintext it is padded to the correct size 
	- the *Advanced Encryption Standard* (AES) is the default symmetric encryption cipher for most products (128 or 256 bits) 
	- Key Length - the range of key values available to use with a particular cipher is called the *keyspace* and is roughly equal to two to the power of the size of the key . the longer the key , the more powerful the encryption 
2. Asymmetric encryption cipher - Here both encryption and decryption are performed by two different but related public and private keys in a key pair . Each key is capable of reversing the operation of its pair and they are linked in such a way as to make it impossible to derive one from the other 
- can be used to prove identity as the holder of the private key cannot be impersonated by anyone else 
- the major drawback of this encryption is that it involves substantial computing resources 
- mostly used for authentication and non-repudiation and for key agreement and exchange 
- Asymmetric encryption is often referred to as *public key cryptography* and the products are based on the *RSA* algorithm 
# Digital Signature 
- Public key cryptography can authenticate a sender while hashing can prove integrity 
- Both can be combined to authenticate a sender and prove the integrity of a message and this usage is called a *Digital Signature*
- a digital signature is a hash that is encrypted usign a private key . Without the encryption, another party could intercept and modify the file thus computing a new hash and sending the modified file and hash to the recipient 
- the recipient must have some means of validating that the public key really was issued by original 
- Digital signatures do not provide confidentiality 
# Digital Signature Algorithm (DSA)
dsa uses elliptic curve cryptography (ECC) rather than the RSA cipher to achieve similar goals 
# Digital Envelopes & Key Exchange 
Both are used within the same product in a type of key exchange system known as a *digital envelope* or *hybrid encryption* . This allows the sender and recipient to exchange a symmetric encryption key securely by using public key cryptography  
# Digital Certificates 
a third party known as a *certificate authority* (CA) can validate the owner of the public key by issuing the subject with a certificate 
the process of issuing and verifying certificates is called *public key infrastructure* (PKI) 
# How to calculate hash value of video,image,pdf 
1. Windows 
``` powershell
Get-FileHash -Path "C:\Videos\sample.mp4" -Algorithm SHA256
Get-FileHash -Path "D:\Images\photo.jpg" -Algorithm MD5
Get-FileHash -Path "C:\Documents\report.pdf" -Algorithm SHA1
```
`-Algorithm` flags: `MD5`, `SHA1`, `SHA256` (default), `SHA384`, `SHA512`

```cmd
certutil -hashfile "C:\Videos\sample.mp4" SHA256
certutil -hashfile "D:\Images\photo.jpg" MD5
certutil -hashfile "C:\Documents\report.pdf" SHA1
```
2. MacOS
```
shasum -a 256 /Users/username/Videos/sample.mp4
md5 /Users/username/Images/photo.jpg
shasum /Users/username/Documents/report.pdf
openssl dgst -sha512 /Users/username/Videos/sample.mp4
```
3. Linux
```
sha256sum /home/username/Videos/sample.mp4
md5sum /home/username/Images/photo.jpg
sha1sum /home/username/Documents/report.pdf
openssl dgst -sha256 /home/username/Videos/sample.mp4
```
# Public & Private key usage 
- the main problem with public key cryptography is that you may not really know with whom you are communicating as the system is vulnerable to MITM attacks 
- Public Key infrastructure (PKI) aims to prove that the owners of public keys are who they say they are with the use of digital certificates guaranteed by a certificate authority 
# Certificate Authority 
this is the entity responsible for issuing and guaranteeing certificates 
Private CAs can be setup within an organization for internal communication while most OS have certificate services 
For public or b2b communications , the CA must be trusted by each party and such third party CA services include IdenTrust , GlobalSign and Digicert 
 # PKI Trust Models 
 - Single CA ==> 
	- a single CA issues certificates to users and the users trust certificates by that CA exclusively 
	- if the CA is compromised , the entire PKI collapses 
 - Hierarchical (intermediate CA) ==>
	- a single CA called the root issues certificates to several intermediate CAs. The intermediate CAs issue certificates to subjects (leaf or end entities)
	- Each lead certificate can be traced back to the root CA along the certificate path and this is reffered to as *certificate chaining* or *chain of trust*
	- the root is still a single point of failure but it can be taken offline as most of the regular CA activities are handled by the intermediate CA servers . 
 - Online versus Offline CAs ==> 
	 - an online CA is one that is available to accept and process certificate signing requests and management tasks 
	 - Because of the high risk posed by a compromised root CA , a secure configuration will involve making the root an offline CA meaning it is disconnected from any network and only brought back online to add or update intermediate CAs 
# Registration Authorities and CSRS 
- Registration is the process by which end users create an account with the CA and become authorized to reques certificates 
- When a subject wants to obtain a certificate , it completes a certificate signing request (CSR) and submits it ot the CA 
- The CA reviews the certificate and checks that the information is valid. If the request is accepted , the CA signs the certificate and sends it to the subject 
# Digital Certificate 
is essentially a wrapper for a subject's public key . As well as the public key , it contains information about the subject and the certificate's issuer .
they are based on the X.509 standard approved by the International Telecommunications Union and standardized by the Internet Engineering Taskforce
# Subject Name Attributes 
- The subject alternative name (SAN) extension field is structured to represent field is structured to represent different types of identifiers including domain names 
- a *wildcard* domain such as *.comptia.org* means that the certificate issued to the parent domain will be accepted as valid for all subdomains 
# Enhanced Key Usage 
can have the following values 
- server authentication 
- client authentication 
- code signing 
- email Protection 
# Web server certificate types 
- a server certificate guarantees the identity of e commerce sites or any sort of websites to which users submit data that should be kept confidential 
- differently graded certificates might be used to provide levels of security eg. an online bank would require a higher security than a site that collects marketing data 
- # Domain Validation (DV) - proves the ownership of a particular domain 
- # Extended Validation - subjecting to a process that requires more rigorous checks on the subjects's legal identity and control over the domain  
- Machine Certificates - machine without valid domain-issued certificates could be prevented from accessing network resources .eg - servers , PCs , smartphone 
- email/user certificates - can be used to sign and encrypt email messages typically using secure multipart internet message extensions or pretty good privacy 
- code signing certificates - this type of certificate is issued to a software publisher following some sort of identity check and validation process by the CA 
- root certificates - one that identifies the CA itself and is self - signed . A root certificate would normally use a key size of at least 2048 bits but many providers are switching to 4096 bits 
- self-signed certificates - these certificates will be marked as untrusted by the operating system or browser but an admin user can choose to override this 
# M-of-N control 
- meaning that of N number of admins permitted to access a system , M must be present for access to be granted . eg - when M=2 and N=4 , any two of the four admins must be present 
- another way to use M-of-N control is to split a key between several storage device ( such as three USB sticks , any two of which could be used to recreate the full key) 
- if the key used to decrypt data is lost or damaged, encrypted data cannot be recovered unless a backup of the key exists . However making too many backups can make it more difficult to keep the key secure 
- *Escrow* means that something is held independently which in terms of key management, means a third party is trusted to store the key securely 
# Certificate Management 
1. Certificate Renewal - When you are renewing a certificate , it is possible to use the existing key referred to specifically as *key renewal* or generated a new key in which case the certificate is *rekeyed* 
2. Certificate Expiration - Certificate are issued with a limited duration set by the CA policy for the certificate type eg a root certificate might have a 10 year expiry date while a web server certificate might be issued for 1 year only . 
3. Certificate Revocation Lists -
	1. a revoked certificate is no longer valid and cannot be reinstated 
	2. a suspended certificate can be re enabled 
4. online certificate status protocol (OCSP) server referred to as an OCSP responder , ocsp servers can obtain the real time status of a certificate 
5. certificate pinning - 
	1. pinning refers to several techniques to ensure that when a client inspects the certificate presented by a server , he is inspecting the proper certificate 
# Certificates Formats 
1. Encoding - cryptography data (both certificates and keys) are processed as binary using Distinguished Encoding Rules. Binary format files are not commonly used so the binary data is typically represented as ASCII text characters using Base64 *Privacy-enhanced Electronic Mail* encoding 
2. File Extensions - both .DER and .PEM can be used as file extension 
# Contents 
- the *PKCS#12* format allows the export of the private key with certificate . On  windows these usually have a *.PFX* extension while MacOS and iOS use *.P12* 
- the *P7B* format implements *PKCS#7* which is a measure of building multiple certificates in the same file . This is often used to deliver a chain of certificates that must be trusted by the processing host 
# OpenSSL 
for linux , CA services are typically implemented using the OpenSSL sutie and many operations can be accomplished using its commands 
# Root CA 
to configure a root CA , an RSA key pair is first created 
`openssl genrsa -aes256 -out cakey.pem 4096`
the -aes256 argument encrypts the key while the 4096 argument sets the key length 
the next step is to use this RSA key pair to generate a self-signed root X.509 digital certificate 
`openssl req -config openssl.cnf -key cakey.pem -new -x509 -days 7300 -sha256 -out cacert.pem`
# Certificate Signing Requests 
to configure a certificate on a host , create a certificate signing request (CSR) with a new key pair 
`openssl req -nodes -new -newkey rsa:2048 -out www.csr -keyout www.key`
this csr file must then be transmitted to the CA server 
`openssl ca -config openssl.cnf -extensions webserver -infiles www.csr -out www.pem`
the certificate can be viewed to check the details by 
`openssl x509 -noout -text -in www.pem`
`openssl verify -verbose -cafile cacert.pem www.pem`
# Key and Certificate Management 
you can export a copy of the private key from a server to be held in escrow as a backup . the key must first be password protected 
`openssl rsa -aes256 - in www.key -out www.key.bak`
The following command can be used to maek the certificate compatible with an application server like Java 
`openssl x509 -outform der -in www.pem -out www.der`
another use case is to export a key and certificate for use in Windows 
`openssl pkcs12 -export -inkey www.key -in www.pem -out www.pfx`
# Longevity 
this refers to the measure of confidence that people have in a given cipher ,in another sense , it is the consideration of how long data must be kept secure 
# Salting 
passwords stored as hashes are vulnerable to brute force and dictionary attacks , a password hash cannot be decrypted as they are one-way 
both attacks can be slowed down by adding a salt value when creating the hash `*(salt + password)*SHA = HASH` 
the salt is not kept secret because any system verifying the hash must know the value of the salt but it's presence means that an attacker cannot use pre-computed tables of hashes 
# Homomorphic Encryption 
this is the conversion of data into ciphertext that can be analyzed and worked with as if it were still in its original form . it enables complex mathematical operations to be performed on encrypted data without compromising the encryption 
# Blockchain 
this is a concept in which an expanding list of transactional records is secured using cryptography . Each record is referred to as a block and is run through a hash function . The hash value of the previous block in the chain is added to the hash calculation of the next block and thus ensures that each successive block is cryptographically linked 
the blockchain is recorded in a public ledger that is decentralized across a peer to peer (P2P) network in order to mitigate the risks associated with a single point of failure 
# Steganography 
this is a technique for obscuring the presence of a message such as hiding a message in a picture . the container document or file is called the *covertext* | "security by obscurity" 

