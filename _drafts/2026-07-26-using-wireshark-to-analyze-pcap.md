---
layout: post
title:  "Using Wireshark To Analyze a PCAP file"
date:   2026-07-27
categories: Wireshark 
author: "Nicholas McAtee"

---

**PCAP Analysis with Wireshark**

**What is PCAP Analysis?**

**PCAP** stands for **Packet Capture**. During a packet capture, a **PCAP** file is generated and contains the captured network traffic. 
For this blog post, PCAP analysis involves using Wireshark to analyze an existing PCAP file. 
Analysts would use PCAP files to examine the network traffic for security issues, troubleshoot network problems, understand how network protocols work, and observe communication between devices on a network.  

**Case Study: PCAP Analysis with Wireshark**

In this post we are going to be using a Brad Duncan’s malware traffic analysis exercise to investigate a infected computer that has been infected with the NetSupport Manager RAT. 
The objectives of this PCAP Analysis are to discover the IP address, MAC address, hostname, user account name, and the full name of the user of the infected Windows client.
 
**Step 1: Identify the IP address of the Infected Windows Client**

![Infected Client IP address](/assets/PCAP-images/IPaddress.png)

**Step 2: Identify the Mac address of the infected client**
 
The next piece of information that we are looking for is the mac address of the infected client.  
I was able to find the mac address using the dhcp in the filter and in the packet under Dynamic Host Configuration Protocol (Request) with the line that said **Client Mac Address: Intel_b2:4d:ad (00:19:d1:b2:4d:ad).**
The mac address of the infected client is **00:19:d1:b2:4d:ad**.
 
![Infected Client mac address](/assets/PCAP-images/macaddress.png)
 
**Step 3: Identify the host name of the infected Windows client**
 

![Infected Client host name](/assets/PCAP-images/dhcp-hostname.png)

![Infected Client nbns host name](/assets/PCAP-images/nbns-hostname.png)
  
**Step 4: Identify the user account name of the infected Windows client**


![Infected Client user account](/assets/PCAP-images/useraccount.png)

**Step 5: Identify the full name of the user who uses the infected Windows client**


![Infected Client Full Name](/assets/PCAP-images/FullName-1.png)

**Findings:**

From the information gathered, the infected client had an IP address of 10.2.28.88. The mac address is 00:19:d1:b2:4d:ad. 
The host name is DESKTOP-TEYQ2NR. The user account name is brolf and the full name is Becka Rolf.

**Conclusion:**


**References:**

Duncan, Brad. “2026-02-28 - TRAFFIC ANALYSIS EXERCISE: EASY AS 123.” Malware-Traffic-Analysis.Net, 28 Feb. 2026, www.malware-traffic-analysis.net/2026/02/28/index.html.
 
Duncan, Brad. “Unit 42 Wireshark Workshop Part 3: Host Identification  Unit 42 .” Youtube, 1 Oct. 2021, www.youtube.com/watch?v=S-ny315TOyk&t=1693s.
 
Sharpe, Richard, et al. “Chapter 1. Introduction.” Chapter 1. Introduction, www.wireshark.org/docs/wsug_html_chunked/ChapterIntroduction.html. Accessed 22 July 2026.
 
“NetBIOS/NBNS - Wireshark Wiki.” Wireshark, 8 Nov. 2020, wiki.wireshark.org/NetBIOS/NBNS.
 
Duncan, Brad. “Wireshark Tutorial: Identifying Hosts and Users.” Unit 42 Paloalto Networks, 10 Oct. 2023, unit42.paloaltonetworks.com/using-wireshark-identifying-hosts-and-users/.
 
“Kerberos Authentication Overview in Windows Server  Microsoft Learn.” Microsoft Windows-Server, 17 July 2025, learn.microsoft.com/en-us/windows-server/security/kerberos/kerberos-authentication-overview. 

“What Is a PCAP File?  Sysdig.” What Is a PCAP File?, 31 Mar. 2026, www.sysdig.com/learn-cloud-native/what-is-a-pcap-file. 
---