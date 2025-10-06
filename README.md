# information-gathering
This repository documents an information-gathering practical performed on Kali Linux. It includes explanations of tools, example commands, and suggested next steps. Only test systems you have authorization to test.

## what is information gathering?

Information gathering is the very first and most critical step of every penetration test.

It does not matter if you have to assess the security of an entire network or a single web application, you need to know your targets in as much detail as possible.

**⭐Now we are using tools of information gathering.**

Whois lookup,
Netcraft,
nslookup,
nc(netcat),
whatweb.

**⭐Whois lookup**

Whois lookup is a tool that helps you find details about a domain name, like who owns it, when it was registered, and which company manages it. It’s useful for getting basic information about a website during the information-gathering part of security testing.

Using whoise on Kali Linux:

<img width="767" height="434" alt="Screenshot 2025-10-06 083554" src="https://github.com/user-attachments/assets/1007ce19-4f27-467c-b2ed-6a86ac77492c" />

The whois google.com command is used to gather registration details about the domain google.com. The output shows information such as:

Domain Name: The domain you searched (in this case, GOOGLE.COM).

Registrar: The company that manages the domain registration (MarkMonitor Inc.).

Creation and Expiry Dates: When the domain was created (1997-09-15) and when it will expire (2028-09-14).

Updated Date: When the domain record was last modified.

Name Servers: The DNS servers that handle domain queries (NS1.GOOGLE.COM, NS2.GOOGLE.COM, etc.).

Domain Status: Lists restrictions applied to the domain, such as preventing unauthorized transfers or deletions.

Registrar Contact Info: Includes an abuse contact email and phone number.

This information helps identify who registered the domain, how long it has been active, and which DNS servers are in use — all useful during the information-gathering phase of security testing.

Instead of using the command line tools, you can also rely on webbased tools such as: [whois.domaintools.com]( whois.domaintools.com)

<img width="1007" height="864" alt="Screenshot 2025-10-06 145844" src="https://github.com/user-attachments/assets/ae397538-71b9-44ef-95b4-02a64adda03b" />


Moreover we can get the IP address of one of the machines of the organization we are studying.

<img width="1179" height="1022" alt="Screenshot 2025-10-06 083902" src="https://github.com/user-attachments/assets/b0b87792-ac10-4f47-8f9a-00d5fed4aabb" />

This Whois information confirms that google.com is officially owned and managed by Google LLC through the registrar MarkMonitor. The record includes key administrative details such as creation and expiry dates, domain protection settings, and DNS server configuration — all valuable during the information-gathering phase to verify authenticity and ownership of a domain.

**⭐Using Netcraft**

Netcraft is a great alternative to the process previously illustrated.

[sitereport.netcraft.com](sitereport.netcraft.com)

<img width="1855" height="939" alt="Screenshot 2025-10-06 114539" src="https://github.com/user-attachments/assets/c0074840-7585-4c44-b9c1-5d861fde5b7a" />
<img width="1833" height="1000" alt="Screenshot 2025-10-06 114634" src="https://github.com/user-attachments/assets/6521a038-154a-4480-8f49-60c5fed95df4" />

**👉General Information:**

Website: Google.com

First seen: November 1998

Popularity rank: 106 globally

Language: English

Description: Search engine for webpages, images, videos, and more

**👉Domain & Hosting:**

Domain registrar: MarkMonitor

Hosting company: Google (USA)

IP addresses: 142.250.191.206 (IPv4), 2a00:1450:400b:c02::8a (IPv6)

Nameserver: ns1.google.com

DNSSEC: Enabled (protects against DNS tampering)

**👉Network & Security:**

Reverse DNS: ord38s31-in-f14.1e100.net

X-Frame-Options: Same origin (prevents clickjacking)

Content Security Policy (CSP): Active (prevents malicious scripts)

X-XSS-Protection: Disabled (modern browsers rely on CSP instead)

**👉Privacy & Standards:**

P3P: Declares privacy practices (older privacy standard)

Doctype: HTML5 (modern web standard for pages) 

Essentially, it’s a combination of WHOIS data, DNS info, and basic site metrics that gives an overview of the site’s technical and organizational setup.

**Summary:**
This report shows Google’s technical setup, security features, and privacy practices. It highlights:

Who owns and hosts the site

The IP addresses and network info

Security headers used to protect users

Privacy standards and modern web technologies

**⭐nslookup**

Nslookup is another very handy tool that lets you translate hostnames to IP addresses and vice versa.

<img width="307" height="182" alt="Screenshot 2025-10-06 121147" src="https://github.com/user-attachments/assets/4e37a350-6568-4a7c-9bc1-d8390f6f6ebc" />

The nslookup command queries the DNS to find the IP addresses associated with a domain.

Server: 10.128.253.185 → The DNS server used for the query

Non-authoritative answer: Shows the IP addresses of google.com

IPv4: 172.217.24.238

IPv6: 2404:6800:4002:816::200e

This means google.com can be reached at these IP addresses.

**👉Reverse DNS Lookup (PTR)**

<img width="555" height="219" alt="Screenshot 2025-10-06 121908" src="https://github.com/user-attachments/assets/77f0da30-2279-4bc5-8e9c-a49bf6c2cc33" />

Using nslookup -type=PTR 172.217.24.238 queries the DNS to find the domain names associated with an IP address.

Non-authoritative answer: Lists several hostnames for the IP 172.217.24.238, such as:

kul06s17-in-f238.1e100.net

hkg12s34-in-f14.1e100.net

tzdela-bb-in-f14.1e100.net

del03s05-in-f14.1e100.net

This shows that reverse DNS mapping can return multiple hostnames for a single IP, especially for large services like Google

**👉Nameserver (NS) lookup**

<img width="452" height="336" alt="Screenshot 2025-10-06 122110" src="https://github.com/user-attachments/assets/2be9e1d3-61a8-4fa9-a9da-a44f2ab60d38" />

This command lists the authoritative DNS servers for google.com.
Output shows four nameservers: ns1.google.com, ns2.google.com, ns3.google.com, ns4.google.com.
The authoritative section also returns their IP addresses (IPv4 and IPv6), e.g. ns1.google.com → 216.239.32.10 and 2001:4860:4802:32::a.

Meaning: NS records tell you which DNS servers are responsible for the domain. The presence of multiple NS entries provides redundancy — if one DNS server fails, others can respond.

**⭐nc(Netcat)**

nc (netcat): A lightweight command-line utility for reading from and writing to network connections. It can open TCP/UDP ports, act as a simple client or server, transfer files, and test services — often described as the “Swiss Army knife” of networking.

<img width="391" height="326" alt="Screenshot 2025-10-06 144413" src="https://github.com/user-attachments/assets/eafe2ed2-8cc4-4324-9090-398cbe6877a9" />


no port[s] to connect to — nc usually requires a port (e.g., nc 172.217.26.110 80). This message indicates you didn’t explicitly provide a port.

Despite that, a HTTP exchange occurred and server-like responses were returned. The output shows two different HTTP responses:

A 200 OK header block (includes Content-Length, Content-Type, Last-Modified) — this looks like a cached/initial header response.

Followed by 403 Forbidden with Cache-Control: no-cache and a short body — the final response indicates access to the requested resource was denied.

Client-Peer: 5.22.145.121:80 — the request appears to have been handled via an intermediate host or proxy at that IP and port.

Timestamps (Client-Date, Last-Modified) are in GMT and show when the server generated those headers.

**⭐Whatweb**

WhatWeb: A command-line web scanner that identifies web technologies (servers, frameworks, CMS, headers, cookies, and more) used by a website.

<img width="1906" height="131" alt="Screenshot 2025-10-06 145033" src="https://github.com/user-attachments/assets/37185608-988b-4a8e-ad3c-ca1b366fc93a" />

whatweb https://google.com 

The site https://google.com first responds with 301 Moved Permanently and redirects to https://www.google.com/.

The redirect response includes uncommon headers like content-security-policy-report-only (CSP in report-only mode) and alt-svc (advertises alternate services/protocols).

The final URL https://www.google.com/ returns 200 OK, serves HTML5, and is powered by the gws server.

Cookies observed: AEC and NID (both marked HttpOnly, so not accessible to JavaScript).

Security headers: X-Frame-Options: SAMEORIGIN (prevents other sites from framing the page) and X-XSS-Protection: 0 (disabled — modern sites rely on CSP instead).

Other notes: accept-ch header present (client hint declarations) and Script detected (site serves JavaScript). IP addresses shown are Google IPs.

Takeaway: Google redirects google.com → www.google.com, serves a modern HTML5 site with CSP in report-only mode, has HttpOnly cookies, and uses common anti-framing protections.

