How to transmit a secret key securely?
- Select a key and physically deliver it
- Use an already communicated key
- Use of a key distrubution centre - kerberos
- Public-key cryptography

![](images/Pasted%20image%2020240726112557.png)
Provides confidentiality - noone but Bob can read the message, but anyone can send it

![](images/Pasted%20image%2020240726112710.png)
Provides authentication and data integrity - anyone can read the message, but it can only have come from Alice and we know it hasn't been changed since she sent it.

### Asymmetric encryption algorithms
Diffie-Hellman key exchange
RSA
Digital signature standard (DSS)
- Provide a digital signature function to verify a documents contents haven't been changed
- Cannot be used for encryption/decryption or key exchange
Elliptic curve cryptography (ECC)
- Offer equal security to RSA with a much smaller key size
- Can be used for encryption/decryption, digital signature, and key exchange
- Used as an extension to other cryptographic schemes

### RSA (Rivest, Shamir, Adleman)
- Most widely used and implemented method
- Can be used for encryption/decryption, digital signature, and key exchange
- Relies on the difficulty of factorising large primes 
![](images/Pasted%20image%2020240726113232.png)

![](images/Pasted%20image%2020240726113450.png)

Key generation:
1. Select two large primes p,q
2. Compute modulus n=pq (typically ~1024 bits)
3. Compute phi(n) = (p-1)(q-1)
4. Pick an integer e, such that e and phi(n) are coprime (no common factors), and e<phi(n)
5. Compute d, such that (ed mod phi(n) = 1), d < phi(n)
	- d is the multiplicative inverse of e (mod phi(n))
	- Found using the extended euclidean algorithm

- The primes must have a sufficient size
- The prime must be fully random to avoid attackers exploiting the patterns
- The most efficient e is a Fermat number (?), only 5 Fermat primes known so we usually pick the largest one (65537). 3 was used historically (the smallest one)

### Diffie-Hellman key exchange
- Limited to the exchange of keys
- Widely used in other protocols
- Allows two users ot exchange a secret key in real-time on an untrusted network
- Requires no prior secrets
- Based on the difficulty of computing discrete logs of large numbers
![](images/Pasted%20image%2020240726114734.png)

![](images/Pasted%20image%2020240726114839.png)
g^ab is now the common secret, and secure communication can be established