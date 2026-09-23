Week 4 - Tutorial 4

Task 1: View Routing Table

Evidence: Network Adapter

![Network Adapter](images/tut%204/Netadapterphysical.png)

I used the following command to view my physical network adapters:

    Get-NetAdapter -Physical

My primary physical network adapter was Wi-Fi, with an interface index of 19.

Evidence: Routing Table

![Routing Table](images/tut%204/netroute.png)

I used the following command to view the routing table for my primary interface:

    Get-NetRoute -InterfaceIndex 19

How to Read Each Row

255.255.255.255/32 — 0.0.0.0 — IPv4 limited broadcast address used to send traffic to all devices on the local network.

224.0.0.0/4 — 0.0.0.0 — IPv4 multicast range used to send traffic to groups of devices.

10.233.159.255/32 — 0.0.0.0 — Broadcast address for the local 10.233.128.0/19 network.

10.233.134.17/32 — 0.0.0.0 — Specific host route for one individual IP address.

10.233.128.0/19 — 0.0.0.0 — Local network directly connected to my computer.

0.0.0.0/0 — 10.233.128.1 — Default route used when there is no more specific route available.

The /19 network covers 10.233.128.0 through 10.233.159.255.


Task 2: Trace Path Through the Internet

Harvard University

![Harvard Traceroute](images/tut%204/havardtrace.png)

I used the following command:

    tracert www.harvard.edu

The trace reached the destination in 15 hops. The final three responses were approximately 9 ms, 6 ms, and 6 ms, giving an approximate average RTT of 7 ms.

The trace included network providers such as Zayo and Lumen. Router names included bwi9, iad93, and wdc12.

Several hops showed Request timed out, but the trace still reached the destination. This means some routers did not respond to traceroute requests even though traffic continued.

Stanford University

![Stanford Traceroute](images/tut%204/stanfordtrace.png)

I used the following command:

    tracert www.stanford.edu

The trace reached the destination in 17 hops. The final responses were approximately 8 ms, 6 ms, and 11 ms, giving an approximate average RTT of 8 ms.

Zayo appeared in several early hops. The final hostname included awsglobalaccelerator.com, indicating that the destination was reached through AWS Global Accelerator infrastructure.

There were many timeouts between the early Zayo hops and the final destination, but the final hop responded.

Oxford University

![Oxford Traceroute](images/tut%204/oxfordtrace.png)

I used the following command:

    tracert www.ox.ac.uk

The trace reached the destination in 13 hops. The final responses were approximately 46 ms, 28 ms, and 7 ms, giving an approximate average RTT of 27 ms.

Zayo appeared in several hops. The destination resolved to www.ox.ac.uk.cdn.cloudflare.net, showing that the trace ended at Cloudflare infrastructure rather than necessarily reaching a physical server at Oxford University.

Several hops timed out, but the destination was still reached successfully.

Traceroute Comparison

Harvard — 15 hops — approximately 7 ms — Zayo and Lumen

Stanford — 17 hops — approximately 8 ms — Zayo and AWS Global Accelerator

Oxford — 13 hops — approximately 27 ms — Zayo and Cloudflare

The number of hops does not directly determine delay. Oxford had fewer hops than Stanford but a higher RTT. Delay can be affected by physical distance, routing, congestion, and network infrastructure.

International Destination

The Oxford traceroute showed that traffic can travel through multiple networks before reaching a destination. It also showed that websites may use services such as Cloudflare, so the final IP address does not necessarily represent the physical location of the organization.

The Oxford trace had a higher RTT than the Harvard and Stanford traces. Distance can contribute to higher latency, but routing, congestion, and network infrastructure can also affect the result.


Task 3: IP Address Lookup

Loyola Network

![Loyola Network IP Lookup](images/tut%204/whatsmyip.png)

I used an online IP lookup service to see what information could be identified about my network.

The results showed:

ISP: Loyola University Maryland

Country: United States

State/Region: Maryland

City: Baltimore

ASN: 36413

Services: None detected

I did not include my actual IP address because it is not necessary for the journal.

Second Network

![Second Network IP Lookup](images/tut%204/phoneip.png)

I repeated the IP lookup using a second network through my phone.

The results showed:

ISP: AT&T Enterprises LLC

Country: United States

State/Region: Virginia

City: Richmond

ASN: 7018

Services: None detected

IP Lookup Comparison

Loyola Network:

ISP: Loyola University Maryland

Country: United States

State/Region: Maryland

City: Baltimore

ASN: 36413


Second Network:

ISP: AT&T Enterprises LLC

Country: United States

State/Region: Virginia

City: Richmond

ASN: 7018

The two networks produced different geographic information and different ISPs. This shows that IP addresses can be associated with different networks and approximate geographic locations.

IP geolocation is not necessarily an exact representation of where a device is physically located. The location shown can represent the location associated with the ISP, network, or IP address rather than the exact location of the device.

DB-IP Lite Database

![DB-IP Lite Database](images/tut%204/dbiplite.png)

I downloaded the DB-IP Country Lite database. The file was named:

    dbip-country-lite-2026-09

The database contains IP address ranges and country information. It can be used to associate an IP address or IP range with a country.


What I Learned

This tutorial helped me understand how computers determine where to send network traffic.

I learned how to:

View my physical network adapter using PowerShell.

Find the interface index for my network connection.

View and understand a routing table.

Understand destination prefixes and next hops.

Use tracert to see the path traffic takes across the Internet.

Compare hops and response times for different destinations.

Identify network providers from traceroute results.

Understand why some routers may not respond to traceroute requests.

Use an IP lookup service to identify information associated with an IP address.

Understand that IP geolocation is approximate.

Use DB-IP Lite to associate IP ranges with countries.


Challenges

One challenge was understanding the routing table because there were several different types of destination prefixes.

Another challenge was interpreting traceroute results because some hops showed Request timed out. I learned that a timeout does not necessarily mean the connection failed because later hops can still respond.

The IP lookup also showed me that the location associated with an IP address is not always the exact physical location of the device.


Project Contribution

This tutorial gave me practical experience using PowerShell networking commands and understanding how network traffic moves between different networks. The routing table and traceroute exercises helped me better understand how devices communicate across local and external networks.


Reflection

Overall, this tutorial helped connect the networking concepts from class to real-world network activity. I was able to use PowerShell to examine my network configuration, trace routes to different websites, and investigate how IP addresses can be associated with geographic locations and Internet service providers.
