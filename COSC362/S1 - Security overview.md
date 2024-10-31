**Week 1, Lecture 01:**

> Cybersecurity is about protecting, preventing damage to, and restoring electronic communications systems (including the information included in these systems)

> Information security is concerned with making sure data in any form is kept secure (protecting the CIA of the data)

**Week 1, Lecture 02:**

Computer Security
> The protection afforded to an automated information system in order to attain the applicaable objectives of preserving the integrity, availablity, and confidentiality of information system resources (includes hardware, software, firmware, information/data, and telecommunications) 

### Confidentiality
- Data confidentiality
	- Assures that confidential information is not disclosed to unauthorised individuals. A violation of this is a **data breach**
- Privacy
	- Assures that individuals control or influence which information related to them may be collected/stored and by whom and to whom that information may be disclosed. A violation of this is a **privacy breach** (type of data breach)
- Data is confidential if it has not been viewed by a third party - use encryption

### Integrity
- Data integrity
	- Assures that information and programs are changed only in a specified and authorised manner
- System integrity
	- Assures that a system performs its operations in an unimpaired manner.
	- Violations are attackers gaining access to the server / installing malicious programs
- Data has maintained integrity if it has not been modified in transit - use hash funcs

### Availability
- Assures systems work properly, violation would be a DOS attack that crashes the server
- For any information system to serve its purpose, the information must be available when it is needed

### Authenticity
- The property of being genuine and being able to be verified and trusted; confidence in the validity of a transmission, message, or message origin
- Veifiying that users are who they say they are and that each input arriving at the system came from a trusted source
- Sometimes included under Integrity
- E.g. deepfakes - AI generated videos of people saying things they didn't actually say

### Accountability
- The requirement for actions of an entity to be traced uniquely to that entity
- Systems must keep records of their activities to permit later forensic analysis to tract security breaches or to aid in transaction disputes

## Risk
- Risk is a product of the assets, threats, and vulnerabilities. Consider a vulnerability a hole in a wall, and a threat something trying to use that hole to get to the assets.

## Attacks
Passive attacks
- Attempt to learn or make use of information from the system that does not affect system resources; eavesdropping on, or monitoring of, transmissions.
- Release of message contents, traffic analysis

Active attacks
- Attempt to alter system resources or affect their operation
- Four categories
	- Replay - capture a valid packet and replay it later on. Countermeasure is timestamps
	- Masquerade - one entity pretending to be another
	- Modification of messages - a portion of the message is changed
	- Denial of service - prevents normal use/management of the service

Origin - Whether the attack has originated from inside/outside the security perimeter

## Security Design Principles
- Economy of mechanism - Security mechanisms should be as simple as possible
	- More complex -> more likely for there to be holes in it
- Fail-safe defaults - Access decisions should be based on permission rather than exclusion
- Complete mediation - Every object access should be checked to ensure they are allowed
- Open design - Security should not depend on secrecy of its design or implementation
- Separation of privilege - Multiple privilege attributes are required to achieve access to a restricted resource
- Least privilege - An entity should be given the least set of privileges needed to perform a task. Reduces risk if an attacker gains access to an account
- Least common mechanism - Design should minimize the functions shared by different users
- Psychological acceptability - Security mechanisms should not interfere unduly with the work of users
- Isolation
	- Public access should be isolated from critical resources
	- User processes and files should be isolated from one another (except when desired)
	- Security mechanisms should be isolated (preventing access to those mechanisms)
- Layering - defence in depth
	- Use of multiple, overlapping protection approaches
- Encapsulation
	- Hide internal structures of object, only interfaces needed to function should be exposed.
- Modularity
	- Development of security functions as separate, protected modules
	- Use of a modular architecture for design and implementation
- Least astonishment
	- Program should respond in a way that is least likely to astonish the user