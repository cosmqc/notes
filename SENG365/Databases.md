#SENG365
## C.A.P. Theorum
#### Consistency
The client receives the most up to date data, or an error message if the read fails.
#### Availability
The client receives a set of the requested data for every request, using cached data if necessary.
#### Partition tolerance
Database continues to function properly even if some nodes are unaccessible. Especially crucial if there are multiple client processes running in parallel, or in distributed databases where data is spread across multiple nodes/servers.

The CAP theorem (also known as Brewer's theorem) states that only two of the three categories are possible at any one time. i.e. when using multiple partitions, you can either choose perfect availability (always return some sort of data) or perfect consistency (always return the most updated data, or an error of some sort). This is quite reductive, and was used mainly to sway the ACID cultists into considering non-relational database systems. 

Partitions are inevitable in real life, so relational databases focus on consistency via the ACID principles, and other types of databases focus on availability via the BASE principles.  
### A.C.I.D. database principles
ACID is a set of principles that define a transaction. A transaction is any operation that is treated as a single unit of work and ensures there aren't any issues with data reliability and integrity. ACID focuses on the Consistency of CAP, so is typically used in situations where data consistency and reliability is essential, like banking applications or medical records. 
#### Atomicity
Each statement in a transaction is treated as a single unit. Either the entire statement is executed, or none of it is executed. If any part of a transaction fails, the previous statements are reverted, rolling the transaction back to the initial state. This prevents integrity issues if, for example, the power goes out during a statement's execution.
#### Consistency
The database is kept in a consistent state before and after the transaction executes.
The execution of the transaction shouldn't leave references not pointing at anything, or data in a field that doesn't match its data type.
#### Isolation
One transaction shouldn't see the effects of other in-progress transactions. This means transactions can execute as if they were happening one-by-one, when they are all running simultaneously. Eliminates [[L16 - Interrupt Processing#Shared data problem|race conditions]] by not committing changes until everything statement in the transaction is complete.
#### Durability
Once a transaction is committed, it should be persistent (even in the event of system failure)

## B.A.S.E. principles
BASE is a set of principles that sacrifice perfect consistency to be able to have perfect availablility.
#### Basic Availability
The database should always make data available, even if there are multiple failures. Instead of having a single data store, data is spread across mutiple nodes with a high degree of replication
#### Soft state
The database can have differing states across the whole system, and the retrieved data may not be the latest across the whole system. This is the 'con' of the BASE system, but the issue is reduced with replication.
#### Eventual consistency
Due to the nodes replicating their new data to their neighbours (and given enough time), the entire system will become consistent.

## Key-value databases
- Unstructured data
- Primary key is the only storage mechanism
- Simpler CRUD operations
- Typically use BASE principles

#### Advantages
- Simple
- Fast
- Flexible (can store any serializable data-type)
- High scalability
- Can engineer high availability

#### Disadvantages
- Stored data is not checked
	- No null checks
	- color vs colour
- Complex to handle consistency -> typically becomes the applications problem
- No relationships, aggregates, Complex searching

#### Examples
- DynamoDB
- Redis (in-RAM)
- IndexedDB (browser-based)

## Database examples
#### DynamoDB
Amazon's very own serverless key-value database.
- Reliablility is primary requirement
	- Make agreements with clients that service will be up 99.99999% of the time
- Super simple (just get and put)

#### Redis
- Key-value
- In-memory storage (RAM)
- Extremely fast access
- Usually paired with another DB, Redis for catching + another DB for long-term
- Values can be much more complex (Sets, Hashes, Streams, etc.)

#### Document database
- Stores documents (mostly JSON or XML, sometimes binary data)
- Builds index from contexts and metadata
- Don't need to do any data parsing, just store it
- Don't need to do any costly schema migration
- Same data can be duplicated across multiple files, no optimization of similar data

#### Graph database
- Nodes and edges represent entities and relationships
- Unidirectional / bidirectional edges
- Properties can describe attributes of the node or edge
- Hypergraphs - one edge can join multiple nodes
- Can be represented in RDBMS, but becomes v inefficient as nodes and edges increase 