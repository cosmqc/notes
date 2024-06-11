#SENG301
### Command pattern
Encapsulate a request as an object thereby letting you parameterise clients with different requests, queue or log requests, and support undoable operations.
i.e. in restaurant, ordering food is an example of this pattern. waitor takes order (invoker takes command), and chef makes something based on that order (receiver processes command) 

**Command** provides an interface for executing operation
**ConcreteCommand**
- implements execute()
- Defines binding between receiver object and an action
**Client**
- Creates ConcreteCommand and sets receiver
Invoker
- Asks command to carry out request
Receiver
- Knows how to carry out request (can be any class)