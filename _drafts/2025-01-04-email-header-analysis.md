---
layout: post
title:  "Email Header Analysis"
date:   2025-01-04
categories: Email 
author: "Nicholas McAtee"

---

**What is Email Header Analysis?**

Email header analysis involves examining the raw message data of an email to determine whether the email is legitimate or potentially phishing, spam, or malicious.
By analyzing the information embedded in the email’s header, you can uncover crucial details about the email’s origin, routing path, and authenticity. 
This process helps to identify red flags that may indicate fraudulent or unwanted emails, such as mismatched sender addresses or suspicious server routes. 
 
**Key Elements of an Email Header**

One of the first things to examine in an email header is the **Received:** header. In a raw email message, there can be multiple **Received:** headers:

• The topmost **Received:** header is the most recent and closest to the destination.

• The bottommost **Received:** header is the earliest and closest to the sender (source).

**Case Study: Analyzing a Suspicious Email**

I had received an email from **brighthorizonstech.uk** about my **"2025 Free Score."** The below screenshot shows you the raw data from the email that we will be analyzing in this post. 
To see the raw text you can find it in this .txt document [here](/assets/documents/2025%20Free%20Score.txt)

![Picture of Raw Email Message](/assets/email-images/Screenshot_1.png)

**Step 1: Review the Received Headers**

• The bottommost **Received:** header indicates that the email originated from an IP address **193.32.163.204**, which is the source mail server. 
• The sender used the EHLO command to identify itself as **rare.swjuk.brighthorizonstech.uk** to the receiving SMTP server. 
• The email was then received by the server at **10.213.170.250,** which is a private IP address that is typically used within an internal network.

The screenshot below shows you the bottommost **Received:** header.

![Bottommost Header](/assets/email-images/Screenshot_2.png)

**Step 2: Perform an IP Address and WHOIS Lookup**

To investigate the sender of the email, I looked up the IP address **193.32.163.204:**

• The IP address is registered to an organization called **Rare Mood Agency SRL**, based in Romania.
• However, the IP address is geographically located in San Jose, California, USA, indicating it may be using a hosting provider in the United States.
• The IP is associated with the website www.vpsforvpn.com.

• The screenshot below shows you the WHOIS lookup information for the sender IP **196.32.163.204**.

![Whois Sender IP](/assets/email-images/Screenshot_3.png)

A WHOIS lookup further confirmed the IP details and revealed the following information about the domain **brighthorizonstech.uk**:

• The domain is only 418 days old.
• There is no associated address or name linked to the domain.
• The screenshot below shows you the WHOIS lookup on **brighthorizonstech.uk** domain.

![Whois brighthorizonstech.uk](/assets/email-images/Screenshot_4.png)

**Step 3: Conduct DNS Lookups**

• I ran a Nslookup on the IP address **193.32.163.204** and it returned with the message: "Non-existent domain."

• The screenshot below shows you the Nslookup on **193.32.163.204.**

![Nslookup 193.32.163.304](/assets/email-images/Screenshot_5 nslookup.png)

• I ran a Nslookup on the domain **brighthorizonstech.uk** which failed to resolve to any IP address.

• The screenshot below shows you the Nslookup on the domain **brighthorizonstech.uk.**

![Nslookup brighthorizonstech.uk](/assets/email-images/Screenshot_6.png)

These results highlight that the domain and IP Address does not match which raises further red flags.

**Step 4: Compare with Known Domains**

There is an existing domain **brighthorizons.co.uk**, which appears legitimate and unrelated to **brighthorizonstech.uk.**
This mismatch further confirms the email’s suspicious nature.

The screenshot below shows you existing domain **brighthorizons.co.uk.**

![Legitmate website](/assets/email-images/Screenshot_7.png)

The below screenshot is the email that I had received **brighthorizonstech.uk.**

![2025 Free Score Email](/assets/email-images/2025_Free_Score_Screenshot.png)

**Findings**

From the gathered information, it is clear that the email did not originate from **brighthorizonstech.uk:**

• The domain did not resolve to any IP address.
• The sender’s IP address and associated organization do not match the purported sender.
• The email’s unsubscribe address is in Texas, which further contradicts its claimed origin.

**Conclusion**

Email header analysis is an essential skill for identifying phishing and other malicious emails. 
By systematically examining the email’s headers, routing paths, and associated domains, you can uncover discrepancies and protect yourself from potential scams. 
Thank you for reading! I hope you enjoyed learning about Email Header Analysis as much as I have. 

**References:**

Gungor, Arman. Email Header Analysis and Forensic Investigation, YouTube, 2020, www.youtube.com/watch?v=nK5QpGSBR8c.

SocketLabs. “SMTP 101: A Beginners Guide.” SocketLabs, 30 June 2023, www.socketlabs.com/blog/beginners-smtp-guide/. 

Whois Lokup, Domain Availability & IP Search - DmainTools, whois.domaintools.com/. Accessed 1 Jan. 2025. 
 
FireEmerald, et al. “How to Use NSLOOKUP Windows Command (11 Examples).” Active Directory Pro, 18 Dec. 2022, activedirectorypro.com/use-nslookup-check-dns-records/. 

“Whois Record for BrightHorizonsTech.Uk.” Whois Lookup Captcha, whois.domaintools.com/brighthorizonstech.uk. Accessed 4 Jan. 2025. 

“IP Information for 193.32.163.204.” Whois Lookup Captcha, whois.domaintools.com/193.32.163.204. Accessed 4 Jan. 2025. 