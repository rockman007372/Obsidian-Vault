---
tags: processed
course: CS2105
Date: 2022-08-28 Sunday
---
Links: [[CS2105]]
- - -

## Extra reading
[How does HTTP and DNS work together](https://www.easyredir.com/blog/how-http-dns-work-together-to-make-url-redirects-happen/)

## Notes

Two ways to identify a host:
- Hostname: http://www.example.org/
- IP address: 93.184.216.34

**DNS** (Domain Name System) translates between Hostname and IP address.

A client must carry out a DNS query to determine the IP address of the corresponding server name prior to the connection (before it can establish TCP connection and send HTTP request)

Mapping between Hostnames and IP addresses are stored as **R**esource **R**ecord (RR)

> RR format: (name, value, type, ttl)

Some common types in RR format:
- type = A
	- **name** is hostname
	- **value** is IP address
- type = NS
	- **name** is domain (nus.edu.sg)
	- **value** is hostname of authoritative name server for this domain
- type = CNAME
	- **name** is alias name for some real name (eg: www.nus.edu.sg)
	- **value** is real/canonical name (mgnzsqc.x.incapdns.net)
- type = MX
	- **value** is name of *mail server* associated with the **name**

### Distributed, Hierarchical Database

DNS stored RR in distributed databases implemented in hierarchy of many name servers

![[Pasted image 20220828203453.png]]

Hierarchy: Root servers → Top-level Domain server → Authoritative Servers
- **Root servers:** Divided into 13 root zones based on geography
- **Top-level Domain servers:** responsible for com, org, net, edu, … and all top-level country domains, e.g., uk, sg, jp
- **Authoritative servers:** Organisations' own DNS servers, providing *authoritative hostname to IP mappings* for the org's named hosts

If a client wants IP address for www.facebook.com
- Client queries root server to find `.com` DNS server
- Client queries `.com` DNS server to get `facebook.com` DNS server
- Client queries `facebook.com` DNS server to get IP address for www.facebook.com

### Local DNS server
- Does not strictly belong to hierarchy
- Each ISP (Intenet Service Provider) has one local DNS server - AKA "default name server".
- When a host makes a DNS query, query is *sent to its local DNS server* → Retrieve name-to-address translation from *local cache* → If answer is not found, local DNS asts as proxy and forward query into hierarchy.
- Once a name server learns mapping, it caches mapping
	- Cached address can be out-of-date
	- Cached entries expire after **Time-To-Live (TLL)** runs out.
	- If name host changes IP address, may not be known internet-wide until TLL expires.
- DNS runs over **UDP** → Fast

#### DNS Name Resolution

If local DNS cache does not return answer, it can send queries to hierarchy in **2 ways**
1. Interative Query
   ![[Pasted image 20220828204904.png]]
2. Recursive Query (Less popular)
   ![[Pasted image 20220828204919.png]]

## Practice Questions

