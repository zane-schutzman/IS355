# Week 4 - Tutorial 4

## Task 1: View Routing Table

For this task, I used Windows PowerShell to identify my physical network adapter and then viewed the routing table for my primary network interface.

### Evidence: Network Adapter

![Network Adapter](https://github.com/zane-schutzman/IS355/raw/main/images/tut%204/Netadapterphysical.png)

I used the following command to view my physical network adapters:

```powershell
Get-NetAdapter -Physical
```

### My Results

My computer showed the following physical network adapter:

* **Name:** Wi-Fi
* **Interface Description:** Intel(R) Wi-Fi 6E AX211 160MHz
* **Interface Index:** 19
* **Status:** Up

The Wi-Fi adapter was the active physical network connection on my computer.

### Evidence: Routing Table

![Routing Table](https://github.com/zane-schutzman/IS355/raw/main/images/tut%204/netroute.png)

I used the following command to view the routing table for my Wi-Fi adapter:

```powershell
Get-NetRoute -InterfaceIndex 19
```

### My Routing Table Results

The routing table contained the following routes:

```text
ifIndex    DestinationPrefix       NextHop
19         255.255.255.255/32      0.0.0.0
19         224.0.0.0/4             0.0.0.0
19         10.233.159.255/32       0.0.0.0
19         10.233.134.17/32        0.0.0.0
19         10.233.128.0/19         0.0.0.0
19         0.0.0.0/0               10.233.128.1
```

### Description of Each Routing Table Row

**Row 1 — 255.255.255.255/32**

This is the IPv4 limited broadcast address. It is used to send traffic to all devices on the local network.

**Row 2 — 224.0.0.0/4**

This is the IPv4 multicast address range. Multicast allows traffic to be sent to a group of devices instead of one specific device.

**Row 3 — 10.233.159.255/32**

This is the broadcast address for my local `10.233.128.0/19` network.

**Row 4 — 10.233.134.17/32**

This is a specific host route for the individual IP address `10.233.134.17`.

**Row 5 — 10.233.128.0/19**

This represents my directly connected local network. Devices within this network can be reached directly through my Wi-Fi interface.

**Row 6 — 0.0.0.0/0**

This is the default route. When my computer needs to send traffic to a destination that does not have a more specific route, it sends the traffic to the next-hop address `10.233.128.1`.

### What I Learned

I learned that a routing table tells my computer how to send network traffic to different destinations.

I learned that the `DestinationPrefix` identifies a destination network or address, while the `NextHop` identifies where traffic should be sent next.

I also learned that `0.0.0.0/0` is the default route. This route is used when there is not a more specific route available.

My computer's active Wi-Fi interface had an InterfaceIndex of 19, which I used with the `Get-NetRoute` command to view the routes associated with that network adapter.

---

# Task 2: Trace Path Through the Internet

For this task, I used the PowerShell `tracert` command to examine the path that network traffic takes from my computer to different Internet destinations.

I tested three different university websites:

* Harvard University
* Stanford University
* University of Oxford

The Oxford website was used as my international destination.

---

## Harvard Traceroute

### Evidence: Harvard Traceroute

![Harvard Traceroute](https://github.com/zane-schutzman/IS355/raw/main/images/tut%204/havardtrace.png)

I used:

```powershell
tracert www.harvard.edu
```

The destination resolved to:

```text
harvard-edu.go-vip.net [192.0.66.20]
```

### Harvard Results

**Number of hops:** 15

**Final round-trip times:** 6 ms, 6 ms, and 9 ms

**Approximate average final delay:** 7 ms

Several network providers could be identified from the traceroute.

Hops 4 through 6 included routers with `zayo.com` in their hostnames, identifying **Zayo** as one of the network providers involved.

Hop 10 included:

```text
lumen.tech
```

which identifies **Lumen**.

Some router names also contained identifiers such as `bwi9` and `iad93`. These names may suggest locations associated with the Baltimore/Washington and Washington/Dulles areas, although router hostnames do not guarantee the exact physical location of a router.

Several hops returned `Request timed out`. However, the traceroute continued and eventually reached the destination at hop 15. Therefore, the timeouts did not prevent the traffic from reaching Harvard.

---

## Stanford Traceroute

### Evidence: Stanford Traceroute

![Stanford Traceroute](https://github.com/zane-schutzman/IS355/raw/main/images/tut%204/stanfordtrace.png)

I used:

```powershell
tracert www.stanford.edu
```

The destination resolved to:

```text
stanford.netlifyglobalcdn.com [3.33.186.135]
```

### Stanford Results

**Number of hops:** 17

**Final round-trip times:** 8 ms, 6 ms, and 11 ms

**Approximate average final delay:** 8 ms

Hops 4 through 6 again showed routers associated with Zayo.

The final hop showed:

```text
awsglobalaccelerator.com [3.33.186.135]
```

This identifies infrastructure associated with **AWS Global Accelerator**.

There were many `Request timed out` results between hops 7 and 16. However, the final hop responded successfully, showing that the traffic was still able to reach the destination.

The Stanford route took 17 hops compared with 15 hops for Harvard. However, the final round-trip delays were still relatively similar.

---

## International Traceroute — University of Oxford

### Evidence: Oxford Traceroute

![Oxford Traceroute](https://github.com/zane-schutzman/IS355/raw/main/images/tut%204/oxfordtrace.png)

I used:

```powershell
tracert www.ox.ac.uk
```

The destination resolved to:

```text
www.ox.ac.uk.cdn.cloudflare.net [104.20.34.13]
```

### Oxford Results

**Number of hops:** 13

**Final round-trip times:** 46 ms, 28 ms, and 7 ms

**Approximate average final delay:** 27 ms

Several hops contained `zayo.com` in their hostnames, showing that Zayo was involved in the route.

The route also contained several IP addresses without descriptive hostnames.

Hops 6 through 9 returned:

```text
Request timed out.
```

However, the trace continued and reached the destination at hop 13.

### Important Observation About the Oxford Trace

The Oxford website resolved to:

```text
www.ox.ac.uk.cdn.cloudflare.net
```

This indicates that the website was using Cloudflare infrastructure.

Therefore, the traceroute does not prove that the final server was physically located at the University of Oxford in the United Kingdom. The trace ended at the Cloudflare address `104.20.34.13`.

This was important because it showed me that a website's domain name does not necessarily mean that the traceroute will end at a physical server located at that organization's location.

---

## Traceroute Comparison

| Destination | Number of Hops | Final Round-Trip Times | Approximate Average | Identifiable Networks        |
| ----------- | -------------: | ---------------------- | ------------------: | ---------------------------- |
| Harvard     |             15 | 6–9 ms                 |                7 ms | Zayo, Lumen                  |
| Stanford    |             17 | 6–11 ms                |                8 ms | Zayo, AWS Global Accelerator |
| Oxford      |             13 | 7–46 ms                |               27 ms | Zayo, Cloudflare             |

### International Traceroute Discussion

The traceroute to the University of Oxford website reached the destination after 13 hops. The final hop had round-trip times ranging from 7 to 46 milliseconds, with an average of approximately 27 milliseconds.

The route traveled through multiple networks and routers. Zayo was identifiable from several router hostnames along the route. Some router names also appeared to contain location-related abbreviations, although these names cannot be used as definitive proof of the physical location of the routers.

The Oxford website resolved to Cloudflare infrastructure rather than directly identifying a physical University of Oxford server. This means that the traceroute showed the network path to the Cloudflare infrastructure serving the website rather than necessarily showing the complete physical path to an Oxford University server.

The traceroute also showed several intermediate routers that did not respond to the traceroute requests. These appeared as `Request timed out`. However, later routers responded and the destination was reached successfully.

Internet delay can be affected by several factors. These include the physical distance that traffic travels, the number of routers involved, network congestion, and the routing decisions made by Internet networks. Communication within a local network generally involves fewer intermediate devices and shorter distances, while communication across the Internet can involve many different networks and routers.

### What I Learned

I learned that `tracert` can be used to see the sequence of network hops between my computer and an Internet destination.

I also learned that different destinations can have different routes even when they are being accessed from the same computer.

Harvard took 15 hops, Stanford took 17 hops, and Oxford took 13 hops. The number of hops did not directly correspond to the final delay because the destinations had different routes and network conditions.

I learned that router names can sometimes provide clues about network providers and possible locations. For example, several of my traces contained Zayo routers.

I also learned that some routers do not respond to traceroute requests. A `Request timed out` message does not necessarily mean that the connection has failed because later routers can still respond and the destination can still be reached.

The international traceroute also demonstrated that a website may use a content delivery or network provider such as Cloudflare, meaning that the final IP address may not represent the physical location of the organization hosting the website.

---

# Task 3: IP Address Lookup

For this task, I used an online IP address lookup tool to examine the network and approximate geographic information associated with two different Internet connections.

## Loyola Network IP Lookup

### Evidence: What Is My IP

![Loyola Network IP Lookup](https://github.com/zane-schutzman/IS355/raw/main/images/tut%204/whatsmyip.png)

The first test was performed using the Loyola University Maryland network.

### Loyola Network Results

**ISP:** Loyola University Maryland

**Country:** United States

**State/Region:** Maryland

**City:** Baltimore

**ASN:** 36413

**Services:** None detected

The lookup identified the network as belonging to Loyola University Maryland and associated it with Baltimore, Maryland.

The lookup did not necessarily identify my exact physical location. Instead, the geographic information represents the location associated with the IP address and network provider.

Because the ISP was identified as Loyola University Maryland, the location may represent the university's network location rather than the exact location of my individual computer.

---

## Second Network IP Lookup

### Evidence: Second Network

![Second Network IP Lookup](https://github.com/zane-schutzman/IS355/raw/main/images/tut%204/phoneip.png)

I then performed the same test using a second network.

### Second Network Results

**ISP:** AT&T Enterprises LLC

**Country:** United States

**State/Region:** Virginia

**City:** Richmond

**ASN:** 7018

**Services:** None detected

The second network was associated with AT&T Enterprises LLC and the lookup identified the IP as being associated with Richmond, Virginia.

### Comparison of the Two Networks

| Information  | Loyola Network             | Second Network       |
| ------------ | -------------------------- | -------------------- |
| ISP          | Loyola University Maryland | AT&T Enterprises LLC |
| Country      | United States              | United States        |
| State/Region | Maryland                   | Virginia             |
| City         | Baltimore                  | Richmond             |
| ASN          | 36413                      | 7018                 |
| Services     | None detected              | None detected        |

The results demonstrate that the public IP address and network information change when using different networks.

The Loyola network was associated with Baltimore, Maryland, while the AT&T network was associated with Richmond, Virginia.

This demonstrates that IP geolocation does not necessarily identify the exact physical location of a person or computer. The location can instead represent the geographic location associated with the ISP or its network infrastructure.

---

## IP Geolocation Database

### Evidence: DB-IP Lite Database

![DB-IP Lite Database](https://github.com/zane-schutzman/IS355/raw/main/images/tut%204/dbiplite.png)

I downloaded the DB-IP Country Lite database for September 2026. The downloaded database was named:

```text
dbip-country-lite-2026-09
```

I opened the database in order to explore how IP address information can be associated with geographic information.

The database contains IP address ranges and country information. It can be used to associate an IP address or IP address range with a country.

The database demonstrates how IP geolocation databases organize Internet address ranges and associate them with geographic locations.

### What I Learned

I learned that an IP address can provide information about the network being used and an approximate geographic location.

I also learned that the public IP address seen by a website is associated with the Internet connection or network rather than necessarily identifying an individual computer's exact physical location.

The two network tests showed this clearly. The Loyola network was associated with Baltimore, Maryland, while the AT&T network was associated with Richmond, Virginia.

The IP lookup was therefore useful for identifying the ISP and an approximate geographic location, but it was not necessarily an exact representation of where the computer or person was physically located.

The DB-IP database also helped demonstrate how IP addresses can be organized into ranges and associated with countries.

---

# What I Learned

This tutorial helped me understand how computers determine where network traffic should go and how traffic travels across the Internet.

In Task 1, I learned how to use PowerShell to view my computer's network adapter and routing table. My active Wi-Fi adapter had an InterfaceIndex of 19. I learned that the routing table contains different routes for local networks, multicast traffic, broadcast traffic, specific hosts, and the default route.

In Task 2, I learned how to use `tracert` to investigate the network paths to Harvard, Stanford, and Oxford. I learned that Internet traffic can travel through multiple routers and network providers before reaching a destination.

I also learned that different destinations can have different numbers of hops and different delays. My Harvard trace used 15 hops, my Stanford trace used 17 hops, and my Oxford trace used 13 hops.

I learned that router names can sometimes provide clues about network providers and possible locations. For example, several of my traces contained Zayo routers.

I also learned that some routers do not respond to traceroute requests. A `Request timed out` message does not necessarily mean that the connection has failed. Later routers can still respond and the destination can still be reached.

In Task 3, I learned that IP geolocation can provide information about the ISP and an approximate geographic location associated with an IP address. My two network tests produced different ISPs and different geographic locations.

Finally, I learned that IP geolocation should not automatically be treated as an exact physical location. The location may represent the network or ISP infrastructure associated with the IP address.

---

# Challenges

One challenge during this tutorial was understanding the routing table. At first, the different destination prefixes were difficult to interpret because they use CIDR notation.

I learned that the `/19` in `10.233.128.0/19` represents the network prefix and that `0.0.0.0/0` represents the default route.

Another challenge was understanding the traceroute results. Some hops displayed `Request timed out`, which could initially appear to mean that the connection had stopped. However, I learned that routers can be configured not to respond to traceroute requests while continuing to forward traffic.

Another challenge was identifying the network providers and possible locations from router hostnames. Names such as `zayo.com`, `lumen.tech`, and `awsglobalaccelerator.com` provided useful information about the networks involved, but router names do not always prove the exact physical location of a device.

The Oxford traceroute was also interesting because the website resolved to Cloudflare infrastructure. This made it important to distinguish between the website's organization and the actual network endpoint shown by the traceroute.

For the IP lookup task, another challenge was understanding why the geographic location did not necessarily represent the exact physical location of the computer. Comparing two different networks helped demonstrate that the location associated with an IP can change depending on the network being used.

---

# Project Contribution

My main contribution during this tutorial was documenting my network configuration and investigating how my computer communicates across the Internet.

I used PowerShell to identify my physical Wi-Fi adapter and view its routing table. I then used `tracert` to investigate the network paths to Harvard, Stanford, and Oxford.

I also compared IP geolocation information from two different networks and explored the DB-IP Country Lite database.

I documented my work with screenshots and organized the evidence in the `images/tut 4` directory of my GitHub repository.

---

# Reflection

This tutorial gave me a better understanding of how my computer communicates with other devices and networks across the Internet.

The routing table activity helped me understand that my computer does not simply send all Internet traffic directly to its final destination. Instead, it uses routing information to determine where different types of traffic should be sent.

The traceroute activity helped me visualize the path that Internet traffic takes. Seeing the different hops, network providers, delays, and timeouts made the routing process easier to understand.

The IP lookup activity also showed me that an IP address can provide useful information about a network while still not identifying the exact physical location of a computer.

Overall, Tutorial 4 helped me connect the concepts from the networking lectures to actual network information from my own computer. I used PowerShell, routing tables, traceroute, IP geolocation, and an IP database to investigate how devices communicate across local networks and the Internet.
