---
layout: post
title:  "Using Wireshark To Analyze a PCAP file"
date:   2026-09-15
categories: Wireshark 
author: "Nicholas McAtee"

---

**PCAP Analysis with Wireshark**

**What is PCAP Analysis?**

**PCAP** stands for **Packet Capture**. During a packet capture, a **PCAP** file is generated and contains the captured network traffic. 
For this blog post, PCAP analysis involves using Wireshark to analyze an existing PCAP file. 
Analysts use PCAP files to examine the network traffic for security issues, troubleshoot network problems, understand how network protocols work, and observe communication between devices on a network.   

**Case Study: PCAP Analysis with Wireshark**

In this post, we are going to be using one of Brad Duncan’s malware traffic analysis exercises to investigate a computer that has been infected with the NetSupport Manager RAT. 
The objectives of this PCAP Analysis are to discover the infected Windows client IP address, MAC address, hostname, user account name, and the full name of the user. 
 
**Step 1: Determine the Client IP Address**

To start finding information on the infected Windows client, we begin by identifying the client’s IP address. 
**DHCP** (Dynamic Host Configuration Protocol) is responsible for assigning IP addresses to devices to communicate on the network. 
The DHCP server will assign an IP address to the client.

In Wireshark, you will apply the **dhcp** display filter to isolate the DHCP traffic in the packet capture. 
The results of the **DHCP** traffic are shown below in the screenshot. 

 I was able to find the IP address when I clicked on the first DHCP Request and looked under **Option: (50) Requested IP address (10.2.28.88)** for the client’s IP address.
 The IP address of the infected Windows client is **10.2.28.88** which is highlighted in yellow.
 
![Infected Client IP address](/assets/PCAP-images/IPaddress.png)

**Step 2: Determine the Client MAC Address**
 
The next piece of information that we are looking for is the MAC address of the infected client. 
I was able to find the MAC address using the **dhcp** display filter and in the highlighted packet that is currently open. Under Dynamic Host Configuration Protocol (Request) with the line that says **Client Mac Address: Intel_b2:4d:ad (00:19:d1:b2:4d:ad)**.
The MAC address of the infected client is **00:19:d1:b2:4d:ad**. 
 
![Infected Client mac address](/assets/PCAP-images/macaddress.png)
 
**Step 3: Determine the Client Hostname**
 
The next piece of information we are looking for is the computer name of the client. The computer name is also known as the hostname. 
I used the same filter as the previous question for  **DHCP**, since the **DHCP** filter provided us with the **IP address**,**MAC address**, and **hostname**. 
The hostname of the infected client that is highlighted in the screenshot is **DESKTOP-TEYQ2NR**. You can also use another filter to get the host’s name called **NBNS**(NetBIOS Name Service).
 
If you use the **DHCP** filter, you will find the hostname under **Option:(12) Host Name**.
If you use **NBNS** filter, you will find it under Additional records under **DESKTOP-TEYQ2NR<20>: type NB, class IN** with a name field that will say as shown in the screenshot Name: **DESKTOP-TEYQ2NR**.

![Infected Client host name](/assets/PCAP-images/dhcp-hostname.png)

![Infected Client nbns host name](/assets/PCAP-images/nbns-hostname.png)
  
**Step 4: Determine the Client’s Associated User Account**

Given that we already found the IP address, MAC address, and the hostname of the client, we are now looking for the user account name of the user who was using the infected Windows client.
In a network, there is a service that provides mutual authentication between services and users called **Kerberos**. In this case we will use the **Kerberos.CNameString** filter to search for the user account name. 
The filter showed **-cname**, which under **-cname** it showed **-cname-string**, and the string showed that the username is **brolf**.

![Infected Client user account](/assets/PCAP-images/useraccount.png)

**Step 5: Identify the Full Name of the Associated User**

The last piece of information that we are looking for is the full name for the username **brolf**. 
To find the full name you will click on **Find Packet** in Wireshark and type in **brolf** as shown below and click find. 
I continued going through the packets that are associated with brolf until I came across the packet with the **QueryuserInfo response**. 
After locating the packet, I examined the packet for the Full name field and found that the identified user is **Becka Rolf**.
 
![Infected Client Full Name](/assets/PCAP-images/FullName-1.png)

**Findings:**

The findings are shown below 
| **    Finding:   **     | **    Value:   **            |
|-------------------------|------------------------------|
| **    IP Address   **   | **    10.2.28.88   **        |
| **    MAC Address   **  | **    00:19:d1:b2:4d:ad   ** |
| **    Hostname   **     | **    DESKTOP-TEYQ2NR   **   |
| **    User Account   ** | **    brolf   **             |
| **    Full Name   **    | **    Becka Rolf   **        |

**Conclusion:**

Thank you to Brad Duncan on a fun and thought provoking pcap analysis to do an exercise on.
Doing a PCAP analysis has many useful purposes in a work environment, in this case we had used it to track down the infected client who was infected with the NetSupport Manager RAT.
Since we were able to track down the client, we can now remediate the threat on the infected machine. 

**References:**

Duncan, Brad. “2026-02-28 - TRAFFIC ANALYSIS EXERCISE: EASY AS 123.” Malware-Traffic-Analysis.Net, 28 Feb. 2026, www.malware-traffic-analysis.net/2026/02/28/index.html.
 
Duncan, Brad. “Unit 42 Wireshark Workshop Part 3: Host Identification  Unit 42 .” Youtube, 1 Oct. 2021, www.youtube.com/watch?v=S-ny315TOyk&t=1693s.
 
Sharpe, Richard, et al. “Chapter 1. Introduction.” Chapter 1. Introduction, www.wireshark.org/docs/wsug_html_chunked/ChapterIntroduction.html. Accessed 22 July 2026.
 
“NetBIOS/NBNS - Wireshark Wiki.” Wireshark, 8 Nov. 2020, wiki.wireshark.org/NetBIOS/NBNS.
 
Duncan, Brad. “Wireshark Tutorial: Identifying Hosts and Users.” Unit 42 Paloalto Networks, 10 Oct. 2023, unit42.paloaltonetworks.com/using-wireshark-identifying-hosts-and-users/.
 
“Kerberos Authentication Overview in Windows Server  Microsoft Learn.” Microsoft Windows-Server, 17 July 2025, learn.microsoft.com/en-us/windows-server/security/kerberos/kerberos-authentication-overview. 

“What Is a PCAP File?  Sysdig.” What Is a PCAP File?, 31 Mar. 2026, www.sysdig.com/learn-cloud-native/what-is-a-pcap-file.

“Kerberos - Wireshark Wiki.” Edited by Moshe Kaplan, Kerberos, 11 Sept. 2026, wiki.wireshark.org/Kerberos. 
