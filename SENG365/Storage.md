#SENG365
Cookie have limitations
- only 4KB
- have to be sent with each request

HTML5 web storage
- allows up to 5MB
- Two types:
	- Local storage
	- Session storage
- Not more secure than cookies

## Cookies
- Has expiry date
- Set and sent via headers (`Cookie:` and `Set-Cookie:`)
## Local storage
- Stores permanent data for site (no expiry)
- Key value pairs
- All data must be strings
- Accessed via getters and setters

## Session storage
- Stores temporary data for site (is removed after window/tab closed)
- Key value
- All data must be strings
- Getters and setters
## IndexedDB
- Web API for creating NoSQL databases in browser
- Allows multiple object stores
- Primary keys
- Indexes
- CRUD requests are async w promises
- `same-origin` policy
- Read/Write is transactional

![[Pasted image 20240610231406.png]]
## CacheStorage
- Another Web API
- Stores Request and Response objects
- Can be up to hundreds of MB in size