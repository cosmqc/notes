#SENG365
## REST
Representational State Transfer (REST) is a set of best practice specifications that APIs should confirm to allow clients to interfact with server resources in a standardized way. Uses the HTTP verbs (i.e. GET, POST, DELETE, PUT, PATCH) together with endpoints that relate to domain entities (usually nouns) to build an intuitive way of interacting with the server.
RESTful APIs should
- Use the HTTP verbs
- Have noun-named endpoints that describe resources.
- Be platform independant (Mac client can talk to Unix host)
- Be language independant (C# client can talk to Java host)
- Be accepted through firewalls (unlike SOAP)

RESTful clients should
- Hide as many implementation details as possible
	- Hide implementation file extensions
- Be consistent with the naming of endpoints
	- Plural/singular
	- Lowercase
	- Use hyphens, not spaces
- Use stateless requests; server shouldn't have to remember who we are, all data the server will need to generate a response should be provided.
#### Solved problem: too many endpoints, unintuitive names
![[Pasted image 20240607132708.png]]

#### REST API ✨
![[Pasted image 20240607132616.png]]

**Safe methods** are methods that don't modify resources, i.e. read only.
#### REST method guarantees
Idempotency and safety (nullipotency) are guarentees that servers make to their clients.
An operation doesn't become safe or idempotent just because it's implemented using a safe method (for eg), there needs to be an effort to match the specification. Adhering to these guarantees helps make an API fault-tolerant and robust

> A poorly written server application might use GET methods to update a record in the 
> database or to send a message to a friend… This is a really, really bad design.

**Safe methods** are methods that don't modify resources, i.e. read only.
**Idempotent methods** are methods where the state is the same regardless of how many times you call it.

![[Pasted image 20240607153030.png]]

#### Problems with REST
- Tightly coupled to HTTP/HTTPS
- Request-response format, cannot use complex communication strategies like broadcast.
- Often multiple request-responses necessary to get complete set of needed data
	- Implied tree-structure (need data from different branches, need more requests)
	- Underfetching and overfetching
	- Latency increases with number of requests made

## SOAP
SOAP (Simple Object Access Protocol) is a API communication protocol defined earlier than the REST specification. Soap is:
- Platform independant
- Language independant
- Transport independant (can work over any protocol: SMTP, HTTP, etc.)
- A transport for XML, JSON, and CSV data

It provides its own security, but has trouble with firewalls.

![[Pasted image 20240607154905.png]]

## GraphQL
APIs tend to be designed to match the views of a webpage, which works fine until the views change, users was different/more/less information, which means the API gets disordered or has to be reworked. 

GraphQL is a specification that defines how you specify data and how to query that data.
This means you can request all data you want in one request and it will return only that information. Some features of GraphQL:
- Define objects and fields that are queryable
- Define entry points for a query
- The client can dynamically compose the content of the query
- Server side is much more flexible
- All queries return 200 response, except for network errors (4xx/5xx)
- Isn't querying the database directly, rather making requests to the server and the server creates the low-level query
- Still needs a sort of schema but they're a lot more atomic than REST
- GET and POST
- GraphQL can sit as a middleman between client and another REST API

## API Testing
### Postman
![[Pasted image 20240610171905.png]]

### Mocha / Chai
Node.js automated testing packages.
**Mocha** is an async testing environment (i.e. JUnit), where **Chai** is an assertion library (mockMvc).

Test files are run in order of occurence (in file system folder, system dependant)
Each test should be independant and run asynchronously, easy using `before()`, `beforeEach()`, and `after()`. 
Avoid the use of `return` and `done()` together, as they are two methods of doing the same thing.
- `done()` forces the test to not finish until the test hits the done() line
- `return` will cut execution immediately
