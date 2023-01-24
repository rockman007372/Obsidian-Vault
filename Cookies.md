---
tags: processed
course: CS2105
Date: 2022-08-22 Monday
---
Links: [[Application Layer]]
- - -

### Definition

HTTP is designed to be stateless. Server maintains no info abt past clients requests → However, sometimes states may be good.

**HTTP cookie** (web cookie, browser cookie) is a *small piece of data* that a server sends to a user's web browser. The browser may store the cookie and send it back to the same server *with later requests*. Typically, an HTTP cookie is used to tell if **two requests come from the same browser**—keeping a user logged in, for example. It remembers stateful information for the *stateless HTTP protocol.*

Main points:
- HTTP messages contain cookie header field
- Cookie file is kept on **user**'s host, managed by browsers
- Cookies are processed by back-end database at Web **servers**

![[Pasted image 20220817021408.png]]

### **Conditional GET** 

An HTTP GET request that operates based on cookies → Server will not retransmit files (objects) if cookie is up-to-date
- Goal: Dont send object if client's cache has up-to-date cached version (stored in cookie)
- Cache: specify date of cached copy in HTTP request
- Server: response contains *no object* if cached copy is up-to-date

![[Pasted image 20220817021653.png]]