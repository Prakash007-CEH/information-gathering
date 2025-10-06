# information-gathering
This repository documents an information-gathering practical performed on Kali Linux. It includes explanations of tools, example commands, and suggested next steps. Only test systems you have authorization to test.

## what is information gathering?**

Information gathering is the very first and most critical step of every penetration test.

It does not matter if you have to assess the security of an entire network or a single web application, you need to know your targets in as much detail as possible.

**Now we are using tools of information gathering.**

Whois lookup
Netcraft
nslookup
nc(netcat)
whatweb

**Whois lookup**

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

<img width="954" height="705" alt="Screenshot 2025-10-05 194544" src="https://github.com/user-attachments/assets/e87e92c9-9dc5-4039-9dfe-faaa0682c980" />

Moreover we can get the IP address of one of the machines of the organization we are studying.
