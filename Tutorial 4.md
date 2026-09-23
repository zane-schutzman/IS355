Week 4 - Tutorial 4

Task 1: View Routing Table

Evidence: Network Adapter

![Network Adapter](images/Netadapterphysical.png)

I used the following command to view my physical network adapters:

```powershell
Get-NetAdapter -Physical
```

My primary physical network adapter was **Wi-Fi**, with an interface index of **19**.

Evidence: Routing Table

![Routing Table](images/netroute.png)

I used the following command to view the routing table for my primary interface:

```powershell
Get-NetRoute -InterfaceIndex 19
```

How to Read Each Row

**Destination Prefix:** `255.255.255.255/32`  
**Next Hop:** `0.0.0.0`  
**Description:** This is the IPv4 limited broadcast address. It is used to send traffic to all devices on the local network.

**Destination Prefix:** `224.0.0.0/4`  
**Next Hop:** `0.0.0.0`  
**Description:** This is the IPv4 multicast range. It is used for sending traffic to groups of devices.

**Destination Prefix:** `10.233.159.255/32`  
**Next Hop:** `0.0.0.0`  
**Description:** This is the broadcast address for the local `10.233.128.0/19` network.

**Destination Prefix:** `10.233.134.17/32`  
**Next Hop:** `0.0.0.0`  
**Description:** This is a specific host route for one individual IP address.

**Destination Prefix:** `10.233.128.0/19`  
**Next Hop:** `0.0.0.0`  
**Description:** This represents the local network directly connected to my computer.

**Destination Prefix:** `0.0.0.0/0`  
**Next Hop:** `10.233.128.1`  
**Description:** This is the default route. It is used when there is no more specific route available.

The `/19` network covers the address range from `10.233.128.0` through `10.233.159.255`.


---

Task 2: Trace Path Through the Internet

Harvard University

![Harvard Traceroute](images/havardtrace.png)

I used the following command:

```powershell
tracert www.harvard.edu
```

The trace reached the destination in **15 hops**. The final three responses were approximately **9 ms, 6 ms, and 6 ms**, giving an approximate average RTT of **7 ms**.

Some of the network providers that appeared in the trace included **Zayo** and **Lumen**. Several router names included `bwi9`, `iad93`, and `wdc12`, which may indicate network locations in the Baltimore/Washington, D.C. area.

There were several `Request timed out` responses, but the trace still reached the final destination. This shows that some routers did not respond to traceroute requests even though traffic continued through the network.


Stanford University

![Stanford Traceroute](images/stanfordtrace.png)

I used the following command:

```powershell
tracert www.stanford.edu
```

The trace reached the destination in **17 hops**. The final responses were approximately **8 ms, 6 ms, and 11 ms**, giving an approximate average RTT of **8 ms**.

Zayo appeared in several of the early hops. The final hostname included `awsglobalaccelerator.com`, which indicates that the destination was reached through AWS Global Accelerator infrastructure.

There were many timeouts between the early Zayo hops and the final destination. However, the final hop responded, so the trace was successful.


Oxford University

![Oxford Traceroute](images/oxfordtrace.png)

I used the following command:

```powershell
tracert www.ox.ac.uk
```

The trace reached the destination in **13 hops**. The final responses were approximately **46 ms, 28 ms, and 7 ms**, giving an approximate average RTT of **27 ms**.

Zayo appeared in several of the hops. The destination resolved to `www.ox.ac.uk.cdn.cloudflare.net`, showing that the trace ended at Cloudflare infrastructure rather than necessarily reaching a physical server located at Oxford University.

There were several timeouts in the middle of the trace, but the destination was still reached successfully.


Traceroute Comparison

**Harvard**

Hops: **15**

Approximate Final RTT: **7 ms**

Network Providers/Infrastructure: **Zayo, Lumen**


**Stanford**

Hops: **17**

Approximate Final RTT: **8 ms**

Network Providers/Infrastructure: **Zayo, AWS Global Accelerator**


**Oxford**

Hops: **13**

Approximate Final RTT: **27 ms**

Network Providers/Infrastructure: **Zayo, Cloudflare**

The number of hops does not directly determine the amount of delay. For example, Oxford had fewer hops than Stanford but had a higher average RTT. Delay can be affected by physical distance, routing paths, congestion, and the networks being used.


What I Learned from the International Destination

The Oxford traceroute showed that traffic can travel through multiple different networks before reaching a destination. It also showed that websites may use services such as Cloudflare, meaning the final IP address does not necessarily represent the physical location of the organization.

Compared with the Harvard and Stanford traces, the Oxford trace had a higher RTT. Distance between networks can contribute to higher latency, but routing, congestion, and the particular network infrastructure being used can also affect the result.


---

Task 3: IP Address Lookup

Loyola Network

![Loyola Network IP Lookup](images/phoneip.png)

I used an online IP lookup service to see what information could be identified about my network.

The results showed:

- **ISP:** Loyola University Maryland
- **Country:** United States
- **State/Region:** Maryland
- **City:** Baltimore
- **ASN:** 36413
- **Services:** None detected

I did not include my actual IP address because it is not necessary for the journal.


Second Network

![Second Network IP Lookup](images/whatsmyip.png)

I repeated the IP lookup using a second network through my phone.

The results showed:

- **ISP:** AT&T Enterprises LLC
- **Country:** United States
- **State/Region:** Virginia
- **City:** Richmond
- **ASN:** 7018
- **Services:** None detected


IP Lookup Comparison

**Loyola Network**

ISP: Loyola University Maryland

Country: United States

State/Region: Maryland

City: Baltimore

ASN: 36413


**Second Network**

ISP: AT&T Enterprises LLC

Country: United States

State/Region: Virginia

City: Richmond

ASN: 7018

The two networks produced different geographic information and different ISPs. This shows that IP addresses can be associated with different networks and approximate geographic locations.

IP geolocation is not necessarily an exact representation of where a device is physically located. The location shown can represent the location associated with the ISP, network, or IP address rather than the exact location of the device.


DB-IP Lite Database

![DB-IP Lite Database](images/dbiplite.png)

I also downloaded the **DB-IP Country Lite** database. The file I downloaded was named:

```text
dbip-country-lite-2026-09
```

The database contains IP address ranges and country information. It can be used to associate an IP address or IP range with a country.

This showed me that IP geolocation can be performed using databases that contain information about IP address ranges and their associated geographic information.


---

What I Learned

This tutorial helped me understand how computers determine where to send network traffic.

I learned how to:

- View my physical network adapter using PowerShell.
- Find the interface index for my network connection.
- View the routing table for a specific network interface.
- Understand destination prefixes and next hops.
- Use `tracert` to see the path traffic takes across the Internet.
- Compare the number of hops and response times for different destinations.
- Identify network providers from traceroute results.
- Understand that some routers may not respond to traceroute requests.
- Use an IP lookup service to identify information associated with an IP address.
- Understand that IP geolocation is approximate.
- Use a database such as DB-IP Lite to associate IP ranges with countries.


Challenges

One challenge was understanding the routing table because there were several different types of destination prefixes. I had to look at each row individually to understand what it represented.

Another challenge was interpreting traceroute results because some hops showed `Request timed out`. I learned that a timeout does not necessarily mean the connection failed because later hops can still respond.

The IP lookup also showed me that the location associated with an IP address is not always the exact physical location of the device.


Project Contribution

This tutorial gave me practical experience using PowerShell networking commands and understanding how network traffic moves between different networks. The routing table and traceroute exercises helped me better understand how devices communicate across local and external networks.


Reflection

Overall, this tutorial helped connect the networking concepts from class to real-world network activity. I was able to use PowerShell to examine my own network configuration, trace routes to different websites, and investigate how IP addresses can be associated with geographic locations and Internet service providers.
