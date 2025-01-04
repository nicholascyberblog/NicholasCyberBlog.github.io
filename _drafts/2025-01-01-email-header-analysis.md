---
layout: post
title:  "Email Header Analysis"
date:   2025-01-02
categories: Email 
author: "Nicholas McAtee"
draft: true
---

What is Email Header Analysis?

Email header analysis involves examining the raw message data of an email to determine whether the email is legitimate or if it is potentially phishing, spam, or malicious. 
By analyzing the information embedded in the email's header, you can uncover important details about the email’s origin, routing path, and authenticity. 
This process helps to identify red flags that may indicate fraudulent or unwanted emails, such as mismatched sender addresses or suspicious server routes. 

One of the first things to examine in an email header is the Received: header. In a raw email message, there can be multiple Received: headers. 
The topmost Received: header is the most recent and closest to the destination, while the bottommost one is the earliest and closest to the sender (source).

Here is an example of an email I have received from brighthorizonstech.uk about my 2025 Free Score. 
You can view the full header as a .txt document here.    


The bottommost Received: header indicates that the email originated from the IP address 193.32.163.204, which is the source mail server.
The sender used the EHLO command to identify itself as rare.swjuk.brighthorizonstech.uk to the receiving SMTP server. 
The email was then received by the server at 10.213.170.250.

Notably, 10.213.170.250 is a Private IP address, which is typically used within an internal network.

By looking up the sender's IP address 193.32.163.204, I found that it is registered to an organization called Rare Mood Agency SRL, which is based in Romania. 
However, the IP address is geographically located in San Jose, California, USA, indicating it may be using a hosting provider in the United States. 
The IP is associated with the website www.vpsforvpn.com.  
















References:

Gungor, Arman. Email Header Analysis and Forensic Investigation, YouTube, 2020, www.youtube.com/watch?v=nK5QpGSBR8c.

SocketLabs. “SMTP 101: A Beginners Guide.” SocketLabs, 30 June 2023, www.socketlabs.com/blog/beginners-smtp-guide/. 

 Whois Lokup, Domain Availability & IP Search - DmainTools, whois.domaintools.com/. Accessed 1 Jan. 2025. 
 
