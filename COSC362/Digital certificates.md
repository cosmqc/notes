How can you distribute public keys?
- Use an already secure mechanism
- Public key announcement
	- Major weakness: anyone can forge a public announcement
- Public key directory
	- Maintenance and distribution by a trusted entity
	- Vulnerable to tampering of the records
- Public key authority
	- Each participant knows a public key for the authority, with only the authority knowing the private key
	- Vulnerable to tampering, authority is the bottleneck 
- Public key certificate
	- A binding between an entity's public key and one or more attributes relating to its identity.
	- Certificate is often signed by a trusted third party
		- Often a certificate authority (CA)
![](images/Pasted%20image%2020240812175615.png)

### Some problems:
- How are digital certificates issued?
- How can I check if a certificate is valid?
- How can I revoke a certificate?
- Who is revoking certificates?

### X.509 certificates
- Most widely accepted format for public-key certificates
- Used in most network security applications
- Each certificate contains the public key of the user, and is signed with the private key of the trusted CA
![](images/Pasted%20image%2020240812180139.png)

- Before using any certificate, an application must check its validity, and ensure that it was not revoked before it expires.
	- Users private key is compromised
	- User is no longer certified by this CA
	- CA is compromised

![](images/Pasted%20image%2020240812180727.png)