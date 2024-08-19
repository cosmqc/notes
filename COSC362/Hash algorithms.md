### Message digest algorithms
- developed by Ronald Rivest
- MD2, MD4, MD5
	- MD5 is the secure version of MD4, but vulnerable to collision attacks

### SHA family
- Secure Hash Algorithm
- SHA0, SHA1, SHA2, SHA3
	- SHA0 and SHA1 are vulnerable to collision attacks

## Applications of Hash functions
- Message authentication
![](images/Pasted%20image%2020240812173550.png)

- Message authentication + digital signature
![](images/Pasted%20image%2020240812173614.png)

- Keyed hash MAC 
![](images/Pasted%20image%2020240812173819.png)

![](images/Pasted%20image%2020240812173951.png)

- Password hashing
	- Store hash value, when user logs in and sends password, the hash is calculated and checked against the stored value
- Integrity checks (checksum)
	- Verifies the file hasn't been altered in transit

