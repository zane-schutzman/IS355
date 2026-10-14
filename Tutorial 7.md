# IS355 Tutorial 7 — Wireshark Packet Analysis

**Course:** IS355 — Networking and Cyber Security
**Student:** Zane Schutzman
**Date:** October 13, 2026

## Capture note

The capture used for the observed packet analysis was downloaded from a website, not supplied by the professor. The packets inspected and recorded were ICMP Frames 634 and 635. The `arp` display filter returned no packets. The details below distinguish what was observed in the capture from general protocol explanations. HTTP-specific packet values cannot be verified from the ICMP packets collected so far.

---

# Task 1 — Analyze a Ping Packet Capture

## 1(a). Inspect the packets

The capture contains ICMP Echo Request and Echo Reply packets. Frames 634 and 635 were inspected.

| Field                    | Frame 634 — Echo Request                    | Frame 635 — Echo Reply                      |
| ------------------------ | ------------------------------------------- | ------------------------------------------- |
| Frame size               | 45 bytes (360 bits)                         | 45 bytes (360 bits)                         |
| Ethernet source MAC      | `50:c7:09:1b:90:a0` (JuniperNetwo_1b:90:a0) | `00:16:3c:cb:72:42` (Rebox_cb:72:42)        |
| Ethernet destination MAC | `00:16:3c:cb:72:42` (Rebox_cb:72:42)        | `50:c7:09:1b:90:a0` (JuniperNetwo_1b:90:a0) |
| IPv4 source              | `43.134.41.39`                              | `203.161.44.208`                            |
| IPv4 destination         | `203.161.44.208`                            | `43.134.41.39`                              |
| Protocol                 | ICMP (1)                                    | ICMP (1)                                    |

The source and destination IP addresses reverse in the reply. The Ethernet source and destination MAC addresses also reverse between these two frames.

## 1(b). Network diagram with IP and MAC addresses

The following diagram represents the two endpoint address pairs shown in the capture. It should not be interpreted as proof that either endpoint is the student's own computer or that it shows the complete physical network.

```
Frame 634 — ICMP Echo Request
Endpoint A                                      Endpoint B
IP: 43.134.41.39  ----------------------------> IP: 203.161.44.208
MAC: 50:c7:09:1b:90:a0                          MAC: 00:16:3c:cb:72:42

Frame 635 — ICMP Echo Reply
Endpoint A                                      Endpoint B
IP: 43.134.41.39  <---------------------------- IP: 203.161.44.208
MAC: 50:c7:09:1b:90:a0                          MAC: 00:16:3c:cb:72:42
```

The MAC addresses above are the Ethernet addresses recorded in the two inspected frames. Ethernet addresses identify interfaces on the local link represented by each frame; they do not necessarily identify the ultimate remote host across every router.

## 1(c). Explain ARP, its sender, recipient, and purpose

Address Resolution Protocol (ARP) maps a local IPv4 address to a MAC address on an IPv4 Ethernet network.

- **ARP Request sender:** The device that needs to discover the MAC address associated with an IPv4 address.
- **ARP Request recipient:** The request is normally broadcast to devices on the local broadcast domain. It asks which device owns the target IPv4 address.
- **ARP Reply sender:** The device that owns the requested IPv4 address.
- **ARP Reply recipient:** The device that sent the request.
- **Purpose:** ARP allows a device to build or update its IP-to-MAC address mapping so it can send an Ethernet frame to the correct local interface.

**What this capture showed:** The `arp` display filter returned no packets. Therefore, the actual sender, recipient, addresses, and contents of a first ARP packet cannot be identified from this capture.

## 1(d). Diagram the first ARP packet and identify header/data sizes

No ARP packet was present in the inspected capture, so the following is a general Ethernet/IPv4 ARP format, not a packet measured from this capture.

| Field                          | Typical size |
| ------------------------------ | ------------ |
| Ethernet header                | 14 bytes     |
| ARP hardware type              | 2 bytes      |
| ARP protocol type              | 2 bytes      |
| Hardware address length        | 1 byte       |
| Protocol address length        | 1 byte       |
| ARP operation                  | 2 bytes      |
| Sender MAC address             | 6 bytes      |
| Sender IPv4 address            | 4 bytes      |
| Target MAC address             | 6 bytes      |
| Target IPv4 address            | 4 bytes      |
| **Total ARP message**          | **28 bytes** |
| **Ethernet frame without FCS** | **42 bytes** |

For a typical Ethernet/IPv4 ARP frame, the 14-byte Ethernet header is followed by the 28-byte ARP message. Ethernet FCS is 4 bytes where it is included in the frame representation, but Wireshark captures often do not include it. Since no ARP packet was captured here, no packet-specific footer, addresses, or byte values can be reported.

```
General Ethernet/IPv4 ARP frame (not observed in this capture)
+----------------------------+--------------------+
| Ethernet header            | 14 bytes           |
+----------------------------+--------------------+
| ARP message                | 28 bytes           |
|   Hardware type            | 2 bytes            |
|   Protocol type            | 2 bytes            |
|   Hardware address length  | 1 byte             |
|   Protocol address length  | 1 byte             |
|   Operation                | 2 bytes            |
|   Sender MAC               | 6 bytes            |
|   Sender IPv4              | 4 bytes            |
|   Target MAC               | 6 bytes            |
|   Target IPv4              | 4 bytes            |
+----------------------------+--------------------+
| Total, excluding FCS       | 42 bytes           |
+----------------------------+--------------------+
```

## 1(e). Explain the first two ICMP packets

### Frame 634 — ICMP Echo Request

| Field                | Observed value                                 |
| -------------------- | ---------------------------------------------- |
| Frame number         | 634                                            |
| Frame size           | 45 bytes on wire; 45 bytes captured (360 bits) |
| IPv4 source          | `43.134.41.39`                                 |
| IPv4 destination     | `203.161.44.208`                               |
| IPv4 header length   | 20 bytes (5 words)                             |
| IPv4 total length    | 31 bytes                                       |
| IPv4 protocol        | ICMP (1)                                       |
| ICMP type            | Echo (ping) request (8)                        |
| ICMP code            | 0                                              |
| ICMP checksum        | `0xaf18` (Wireshark marked it correct)         |
| ICMP identifier      | 5883 (`0x16fb`)                                |
| ICMP sequence number | 53693 (`0xd1bd`)                               |
| ICMP data            | `30 2e 30` (`302e30`), 3 bytes                 |

The Echo Request asks the destination to return an Echo Reply. Its 31-byte IPv4 packet consists of a 20-byte IPv4 header and an 11-byte ICMP message. The ICMP message consists of an 8-byte ICMP header and 3 bytes of data.

### Frame 635 — ICMP Echo Reply

| Field                | Observed value                                 |
| -------------------- | ---------------------------------------------- |
| Frame number         | 635                                            |
| Frame size           | 45 bytes on wire; 45 bytes captured (360 bits) |
| IPv4 source          | `203.161.44.208`                               |
| IPv4 destination     | `43.134.41.39`                                 |
| IPv4 protocol        | ICMP (1)                                       |
| ICMP type            | Echo (ping) reply (0)                          |
| ICMP code            | 0                                              |
| ICMP checksum        | `0xb718` (Wireshark marked it correct)         |
| ICMP identifier      | 5883 (`0x16fb`)                                |
| ICMP sequence number | 53693 (`0xd1bd`)                               |
| ICMP data            | `30 2e 30` (`302e30`), 3 bytes                 |

The Echo Reply returns from the destination to the original sender. The IP addresses reverse compared with Frame 634. The matching identifier and sequence number associate the reply with the request, and the 3-byte data payload is the same.

## 1(f). Diagram the first ICMP packet

```
Frame 634 — observed Ethernet II frame: 45 bytes
+------------------------------------------------+
| Ethernet II header                    14 bytes |
+------------------------------------------------+
| IPv4 header                           20 bytes |
| Source IP:      43.134.41.39                    |
| Destination IP: 203.161.44.208                  |
| Protocol: ICMP (1)                             |
+------------------------------------------------+
| ICMP Echo Request header                8 bytes|
| Type: 8 (Echo Request)                         |
| Code: 0                                        |
| Checksum: 0xaf18                               |
| Identifier: 5883 (0x16fb)                      |
| Sequence: 53693 (0xd1bd)                       |
+------------------------------------------------+
| ICMP data                              3 bytes |
| Hex: 30 2e 30                                  |
+------------------------------------------------+
IPv4 total length = 20 + 8 + 3 = 31 bytes
Frame size = 14 + 31 = 45 bytes
```

---

# Task 2 — Analyze HTTP Traffic

The packet-specific HTTP questions below cannot be answered accurately from Frames 634 and 635 because those are ICMP packets. No HTTP request, HTTP response, HTTP header, TCP handshake, or TCP acknowledgement details were collected from this capture. The answers below provide the protocol explanations where possible and identify exactly which observations are unavailable rather than inventing packet values.

## 2(a). What triggers the HTTP request, and what does it contain?

**Observed answer:** Not determinable from the ICMP packets inspected. Frames 634 and 635 contain ICMP Echo Request/Reply messages, not HTTP messages.

To answer this from the required HTTP capture, identify the HTTP request frame and record the user action or page behavior that triggers it, the HTTP method (such as `GET` or `POST`), the requested resource, and any relevant query parameters or request body.

## 2(b). What triggers the HTTP response, and what does it contain?

**Observed answer:** Not determinable from the inspected ICMP packets. No HTTP response status line or response headers were recorded.

In an HTTP exchange, the server's response is associated with the request and contains a status code and phrase (for example, a successful response or an error), along with headers and potentially a response body. The exact frame, status code, and content must be read from the HTTP capture.

## 2(c). What are the five address values requested?

**Observed answer:** The five HTTP-related address values cannot be identified from the available ICMP observations because the exact HTTP packet fields have not been collected. The observed addresses available for Task 1 are:

- Frame 634 IPv4 source: `43.134.41.39`
- Frame 634 IPv4 destination: `203.161.44.208`
- Frame 634 Ethernet source MAC: `50:c7:09:1b:90:a0`
- Frame 634 Ethernet destination MAC: `00:16:3c:cb:72:42`
- Frame 635 reverses those source and destination values.

These are the five address values currently supported by the inspected packets; they should not be substituted for any different five values specifically requested in the HTTP question.

## 2(d). What request is associated with the date/time button, and why is it made?

**Observed answer:** The relevant HTTP request and timestamp were not recorded in Frames 634 or 635. The date/time button's request cannot be identified from the ICMP packets.

To determine this, inspect the HTTP capture immediately after activating the button, identify the new request, and record its frame number, timestamp, method, URI, and any query parameters. The request's purpose should be explained from those observed fields and the page behavior, not guessed.

## 2(e). What is the HTTP Referrer field, and how is it used?

The HTTP request header is spelled `Referer`. It can indicate the page URL from which the browser navigated to the requested resource. A website may use it for navigation context, analytics, or related behavior. It may be absent or limited depending on the browser's referrer policy.

**Value in this capture:** Not recorded; the ICMP frames do not contain an HTTP `Referer` header.

## 2(f). What browser is being used, and what version?

HTTP requests may include a `User-Agent` header with browser and operating-system information. The exact browser and version should be reported from that header.

**Observed answer:** No HTTP `User-Agent` header was collected, so the browser and version cannot be determined from the available packets.

## 2(g). What HTTP version and transport protocol are used?

**Observed answer:** The HTTP version cannot be determined from the ICMP frames. The inspected packets use **ICMP over IPv4**, not HTTP. HTTP/1.x commonly runs over TCP, but the transport protocol for the assignment's HTTP request must be confirmed from that request's packet details.

## 2(h). Which packets establish the connection, and what are their times?

**Observed answer:** No TCP connection handshake packets or timestamps were recorded for an HTTP flow. Therefore, the SYN, SYN-ACK, and final ACK frame numbers and times cannot be stated.

For a typical TCP three-way handshake, the client sends SYN, the server returns SYN-ACK, and the client sends ACK. The actual frame numbers and time differences must be read from the HTTP flow in Wireshark.

## 2(i). Which acknowledgements are sent, and what do they show?

**Observed answer:** The TCP acknowledgement frame numbers, sequence numbers, acknowledgement numbers, and timing were not collected. ICMP Frames 634 and 635 do not provide the TCP acknowledgement evidence required by this question.

TCP acknowledgements indicate the next byte expected by the receiving side and help confirm that bytes have been received. The specific acknowledgement values and timing must be recorded from the corresponding TCP packets.

## HTTP request packet diagram

A packet-specific HTTP request diagram cannot be completed accurately without an HTTP request frame. The diagram below is a template for the required structure, not a claim about an observed packet.

```
HTTP request frame: size not collected
+-----------------------------------------------+
| Ethernet header: size/value not collected     |
+-----------------------------------------------+
| IPv4 header: size/total length not collected  |
| Source/destination IP: not collected          |
+-----------------------------------------------+
| TCP header: size/ports not collected          |
+-----------------------------------------------+
| HTTP request and data: size not collected     |
| Method, URI, headers: not collected           |
+-----------------------------------------------+
```

The required PNG and editable `.drawio` diagram should be created from the actual HTTP request packet once that packet has been inspected.

---

# Task 3 — Optional Packet Structure Exercise

## 3.1. Observed endpoint table

| Endpoint   | IPv4 address     | Ethernet MAC address | Evidence                              |
| ---------- | ---------------- | -------------------- | ------------------------------------- |
| Endpoint A | `43.134.41.39`   | `50:c7:09:1b:90:a0`  | Frame 634 Ethernet II and IPv4 fields |
| Endpoint B | `203.161.44.208` | `00:16:3c:cb:72:42`  | Frame 634 Ethernet II and IPv4 fields |

These are endpoint addresses from the downloaded capture. The capture does not establish that either endpoint is the student's own computer or show the complete physical topology.

## 3.2. ICMP/IP packet across networks and router MAC addresses

The observed packet gives the source/destination IP and Ethernet MAC addresses for the recorded Ethernet frame. It does not, by itself, reveal every router interface or every Ethernet header along the entire end-to-end path. If the assignment asks for MAC addresses at a router or on multiple LANs, those values must be observed from packets on the corresponding links or supported by the provided routing/network information.

**Observed packet directions:**

- Frame 634: `43.134.41.39` → `203.161.44.208`
- Frame 635: `203.161.44.208` → `43.134.41.39`

## 3.3. Routing tables

**Observed answer:** No routing-table output was collected as part of the Wireshark packet inspection described here. The routing tables required by this optional task cannot be reconstructed reliably from the two ICMP frames alone. Add the routing-table output from the relevant devices if completing this optional task.

## 3.4. Required optional-task files

If this optional task is required, include:

- A network diagram image and its editable `.drawio` source.
- The routing tables requested by the instructor.
- An ICMP/IP packet diagram image and its editable `.drawio` source.

Only label values as observed when they have actually been collected.

---

# Task 4 — Traffic Analysis

The assignment directs students to [Malware Traffic Analysis](https://www.malware-traffic-analysis.net/) and its [Bluesky profile](https://bsky.app).

**Status based on the work recorded here:** A Task 4 malware-traffic capture has not been analyzed in the observations available for this report. The inspected Frames 634 and 635 are ICMP packets and do not provide enough evidence to identify malware-related behavior.

To complete the analysis, use the capture specified by the instructor or the selected exercise from the assigned source. Record the capture name/date, filters used, relevant frame numbers and timestamps, source/destination addresses, protocols, and the packet evidence supporting each conclusion. Do not claim that traffic is malicious based only on a display-filter label or an IP address.

---

# GitHub Submission Checklist

- Record Frame 634 ICMP Echo Request details.
- Record Frame 635 ICMP Echo Reply details.
- Record the observed Ethernet MAC and IPv4 addresses.
- Test the `arp` filter and record that no ARP packets appeared.
- Explain ARP and provide a general ARP layout while noting it was not captured.
- Explain and diagram the observed ICMP request.
- Capture and add Wireshark screenshots of Frames 634 and 635.
- Inspect the HTTP capture and replace the unavailable HTTP-specific findings with observed values.
- Create the HTTP request packet diagram as PNG and include its `.drawio` source.
- Complete Task 3's diagrams/routing tables if the optional task is required.
- Complete Task 4 with evidence from the assigned traffic-analysis capture.
- Verify all image links and file paths on GitHub.

## Suggested repository structure

```
IS355/
└── Tutorial7/
    ├── Tutorial 7.md
    ├── images/
    │   └── tut7/
    │       ├── frame634-icmp-request.png
    │       ├── frame635-icmp-reply.png
    │       ├── http-request-diagram.png
    │       ├── network-diagram.png
    │       └── icmp-ip-diagram.png
    └── diagrams/
        └── tut7/
            ├── http-request-diagram.drawio
            ├── network-diagram.drawio
            └── icmp-ip-diagram.drawio
```

## What I Learned

ICMP Echo Requests and Echo Replies can test reachability between IP endpoints. In the observed pair, the reply reverses the IP and Ethernet source/destination addresses. The matching ICMP identifier and sequence number help associate the reply with the request. The IPv4 total length includes the IPv4 header and its payload; the observed 31-byte IPv4 packet plus a 14-byte Ethernet header accounts for the 45-byte frame.

ARP resolves a local IPv4 address to a MAC address, but the downloaded capture contained no ARP packets. This is why protocol explanations must be distinguished from packet evidence actually present in a capture.

## Challenges

The downloaded capture did not show ARP packets, and the packet details collected for this report were ICMP rather than HTTP. Therefore, the HTTP request/response values, browser header, TCP handshake, acknowledgement timing, and HTTP packet diagram could not be verified. These values must come from the appropriate HTTP-containing capture rather than being guessed.

## Reflection

Wireshark allows packet inspection at Ethernet, IP, and transport/protocol layers. Comparing a request and reply shows how addresses and protocol fields change during communication. A reliable packet analysis records frame numbers and field values directly from the capture and clearly identifies information that the capture does not provide.
