Biometrics have two classes:
- Verification (My biometrics prove I am who I say I am)
	- Usually paired a seperate way of identification (name, PIN, etc)
- Identification (My biometrics say who I am)

Lots of data online that can be scraped for exploitation in the future (high quality photos of face -> face/retina, high quality photos of hands -> fingerprint).

### Biometric accuracy
Since a read can never be perfectly correct (reading inaccuracy, hot day causes sweat -> slightly different fingerprint) biometric readers have a threshold where they will accept differing values. Ideally, we want the entirety of the attacker's range under the threshold and the entirety of the genuine user's range above the threshold. Practically, there will always be some overlap between an attackers range and a genuine user's range, so the job is to minimize the overlap/figure out where the threshold should be.

- The rate at which the imposter is above the threshold is called the 'false match rate'
- The rate at which the genuine user is below the threshold is called the 'false nonmatch rate'

#### Attacks against biometrics
- Presentation attacks - creating something that will cause the biometric sensor to generate the desired value. Could be images found online, eye scans / fingerprints pulled off glasses (movie stuff).
- Sensor output interception - MITM attack, get the genuine user's biometric info from the machine itself and use it at a later time
- Database-related vulnerability - attacker can steal biometric information. Valuable on its own, but can sometimes be used to use at a later time to gain access. 


## Access control
Elements include:
- Subject - entity who can access objects.
	- Owner (creator)
	- Group (group which the owner is in)
	- World (everyone else)
- Object - a resource we want to control (files, directories, programs)
- Access right - the way a subject may access an object (read, write, delete, search, etc)

### Categories
- Discretionary access control (DAC) - Can user 123456 read file X?
	- Access matrix. User A \* File 1 = Own, Read, Write
- Mandatory access control (MAC) - Compare security label to security clearance, one with access to X cannot pass that access to others
- Role-based access control (RBAC) - Does the user have the role to allow them to do X?
	- Access rights assigned to roles, company structure; many-to-many.
	- Matrix structure, User has a set of roles, which each have a set of permissions
- Attribute-based access control (ABAC) - attributes of the user, resource being access, context