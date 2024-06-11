#SENG365
A **single page applications** (SPA) a web app implementation that loads only a single web document, and then updates the body content of that single document via [[HTTP & Javascript#Javascript|Javascript]].
They prioritize responsiveness and interactivity, which is difficult as managing user interactions is a lot more difficult as managing predictable interactions with a server.

>Single page apps are distinguished by their ability to redraw any part of the UI without requiring a server round trip to retrieve HTML. This is achieved by separating the data from the presentation of data by having a model layer that handles data and a view layer that reads from the models

Some features of SPAs:
- Seperate the data and the content/presentation of the application
- Reduces the communication with the server
	- Occasionally download resources (HTML, CSS, JS)
	- Async fetching of data with AJAX or `fetch()`
	- Fetch data only (e.g. JSON)
	- Fetch data from different servers: **CORS**
- 'Page navigation' is simulated with client-side Javascript, not actually sending requests
- Rebalances the workload between the server-side and client-side, i.e.
	- Node.js on server-side
	- React on front-end
	- Communication between the two is done by a specified API

# SPA Communication
**AJAX** - Asynchronous Javascript and XML
**XHR** - XMLHttpRequest

Use XHR web API to issue async HTTP requests while staying single threaded, or ideally some abstraction (jQuery $.ajax(), axios, fetch, etc.)

Uses the **event demultiplexer** to store and forward the async callbacks to the event queue on fulfillment.

# CORS
Cross-origin resource sharing 
### Why?
Cross-site request forgery (CSRF): send fake client requests to another application
Solution: same-origin policy (**SOP**) - on by default.

SOP only stops loading resources (HTML, CSS, images, files, more importantly JS) from other domains, attackers can still make raw requests.

It's perfectly regular to request things from other domains, so need a system to let *some* domains through SOP.

Origin consists of protocol, domain, and port. If any of those changes, the request is cross origin. Subdomains -> parent is same-origin, but parent -> subdomain is cross-origin.

CORS manages this via headers, so these are forbidden (cannot be changed):
- Access-Control-*
	- Access-Control-Origin
	- Access-Control-Headers
	- etc.
- Origin
- (lots more)

**It is the browser's responsibility to honour CORS headers**
# Web sockets
### HTTP and AJAX
- Unidirectional communication
	- Client sends request, server sends response
- Stateless
- Less efficient
- Good for resource retrieval
- Has to implement polling to get resources from server (needs client request to get data)
## Web socket
- Persistent two-way communcation
- Maintains state
- Fast, lightweight, allows lot more connections
- Good for real-time comms
- Server can push data to client (no need for request for server to send data)
### Handshake
1. Client sends HTTP GET requets to server
2. Server responds with info on how to connect to socket
3. Client sends HTTP GET with 'Connection: Upgrade' and connection is upgraded to socket

