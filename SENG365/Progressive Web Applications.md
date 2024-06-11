#SENG365
**Progressive Web Applications** (PWAs) are web applications that appear to be 'installed' as native apps. 
- Need to start as a browser tab then can be 'installed'.
- Rely on service workers to do tasks like notifications and background sync

Advantages:
- Much smaller size
- Adaptable (changes to app don't need to go through app store)
- Automatic updates
- New operating systems
- Faster, more efficient development

Criteria:
- Responsive
- Connectively independant
- App-like interactions
- Fresh
- Safe
- Discoverable
- Re-engagable
- Installable
- Linkable

Good to have:
- Mobile-friendly
- Near-instant loading
- Work across devices / browsers
- Fluid animations
### Service Worker
- A proxy server that sit between web apps and the browser/network.
- Uses headless Javascript (no access to the DOM) that runs on its own thread.
- Can be used to execute long running processes
- Must be started and registered by a web page
- Allows websites to run offline using caching
- Must use https
- Max scope is the location of the worker

Storage is done with either Web storage ([[Storage#Local storage|Local Storage]]), IndexedDB, or using CacheStorage API 

