# IS355 Week 09 Tutorial — Cyber Security Management

**Course:** IS355 — Networking and Cyber Security  
**Student:** Zane Schutzman  
**Project:** iMessage Group Chat Network

---

## Task 1: Select Security Objectives

The following four security objectives are selected from the NIST Cybersecurity Framework (CSF). Two objectives belong to the Protect function, and two belong to the Detect function. Each objective comes from a different category within its function.

### Objective 1: Identity Management, Authentication, and Access Control

- **Function:** Protect (PR)
- **Category:** Identity Management, Authentication, and Access Control (PR.AA)
- **Sub-category:** PR.AA-05 — Access permissions, entitlements, and authorizations are defined in a policy, managed, enforced, and reviewed, and incorporate the principles of least privilege and separation of duties.

**Why it is important:**

This objective helps ensure that only authorized users can access the group's network resources and information. Access should be limited to what each user needs, reducing the risk of unauthorized access to private group information.

**Attack or vulnerability mitigated:**

Unauthorized access, such as an attacker gaining control of a group member's account and attempting to access private conversations or shared files.

### Objective 2: Data Security

- **Function:** Protect (PR)
- **Category:** Data Security (PR.DS)
- **Sub-category:** PR.DS-02 — The confidentiality, integrity, and availability of data-in-transit are protected.

**Why it is important:**

Messages and shared files must be protected while being transmitted between users' devices. This helps maintain the confidentiality of private conversations and prevents unauthorized changes to information.

**Attack or vulnerability mitigated:**

A man-in-the-middle attack, in which an attacker attempts to intercept or alter information traveling across a network.

### Objective 3: Continuous Monitoring

- **Function:** Detect (DE)
- **Category:** Continuous Monitoring (DE.CM)
- **Sub-category:** DE.CM-01 — Networks and network services are monitored to find potentially adverse events.

**Why it is important:**

Monitoring network activity can help identify unusual connections, suspicious traffic, and other behavior that could indicate a security threat to the group's network.

**Attack or vulnerability mitigated:**

Unauthorized network access or malicious network traffic that could indicate an attempted security breach.

### Objective 4: Adverse Event Analysis

- **Function:** Detect (DE)
- **Category:** Adverse Event Analysis (DE.AE)
- **Sub-category:** DE.AE-02 — Potentially adverse events are analyzed to better understand associated activities.

**Why it is important:**

Analyzing suspicious events helps determine whether unusual activity represents a genuine security threat. This allows the group to investigate potential incidents and respond appropriately.

**Attack or vulnerability mitigated:**

Repeated unauthorized login attempts or suspicious account activity that could indicate a brute-force attack or a compromised account.

---

## Task 2: Create Asset Inventory

The asset inventory identifies the important data, hardware, software, people, facilities, and network resources associated with the iMessage group chat network. The inventory includes identifying information and the protections needed to maintain security.

*Note: Identifiers and device details below are fictional examples for this project.*

### 2.1 Data Assets

| Asset ID | Asset Name | Description | Classification | Important Protections |
|---|---|---|---|---|
| D-001 | Group Messages | Messages exchanged between group members | Confidential | Confidentiality, Integrity |
| D-002 | Shared Files | Documents, images, and other files shared in the chat | Confidential | Confidentiality, Integrity, Availability |
| D-003 | Member Contact Information | Phone numbers and contact details of group members | Confidential | Confidentiality, Integrity |
| D-004 | Apple Account Credentials | Credentials used by members to access their Apple accounts | Restricted | Confidentiality, Integrity |
| D-005 | Group Member List | List of authorized group participants | Internal | Confidentiality, Integrity |
| D-006 | Network Configuration Information | Wi-Fi details and relevant network settings | Restricted | Confidentiality, Integrity, Availability |

**Data classification definitions:**

- **Public:** Information that can be shared openly.
- **Internal:** Information intended for group members or authorized users.
- **Confidential:** Private information that should only be accessible to authorized users.
- **Restricted:** Highly sensitive information requiring strict access controls.

The CIA protections mean confidentiality (preventing unauthorized disclosure), integrity (preventing unauthorized modification), and availability (ensuring authorized users can access information when needed).

### 2.2 Hardware Assets

| Asset ID | Asset Name | Description | Identifier | Important Protections |
|---|---|---|---|---|
| H-001 | Member Smartphone 1 | Smartphone used to access iMessage | DEV-IPH-001 | Screen lock, device encryption |
| H-002 | Member Smartphone 2 | Smartphone used to access iMessage | DEV-IPH-002 | Screen lock, device encryption |
| H-003 | Member Laptop | Laptop used to access files and network resources | DEV-LAP-001 | Updates, endpoint protection |
| H-004 | Wireless Router | Provides local wireless network connectivity | DEV-RTR-001 | Secure administration, firmware updates |
| H-005 | Wireless Access Point | Provides wireless access to the network | DEV-AP-001 | Strong authentication, secure configuration |

### 2.3 Software Assets

| Asset ID | Asset Name | Description | Version or Identifier | Important Protections |
|---|---|---|---|---|
| S-001 | Apple Messages | Application used for group messaging | Current supported version | Software updates, account security |
| S-002 | iOS | Operating system on member smartphones | Current supported version | Security patches, device encryption |
| S-003 | macOS | Operating system on compatible Apple computers | Current supported version | Security patches, access controls |
| S-004 | Device Security Software | Built-in security and protection features | Vendor-supported version | Malware protection, threat detection |
| S-005 | Router Firmware | Software controlling the wireless router | Current supported version | Firmware updates, secure configuration |

### 2.4 People Assets

| Asset ID | Asset Name | Role | Identifier | Important Protections |
|---|---|---|---|---|
| P-001 | Group Administrator | Manages group membership and settings where applicable | USER-001 | Strong authentication, restricted privileges |
| P-002 | Group Member 1 | Sends and receives group messages | USER-002 | Account security, security awareness |
| P-003 | Group Member 2 | Sends and receives group messages | USER-003 | Account security, security awareness |
| P-004 | Group Member 3 | Sends and receives group messages | USER-004 | Account security, security awareness |
| P-005 | Network Administrator | Maintains the local network and router | USER-005 | Strong authentication, limited administrative access |

### 2.5 Facilities Assets

| Asset ID | Asset Name | Description | Identifier | Important Protections |
|---|---|---|---|---|
| F-001 | Primary Work Location | Location where a member accesses the network | SITE-001 | Physical access controls |
| F-002 | Home Network Area | Area containing the wireless router and network equipment | SITE-002 | Restricted physical access |
| F-003 | Device Storage Area | Location where devices are stored when not in use | SITE-003 | Secure storage, theft prevention |
| F-004 | Charging Area | Location where member devices are charged | SITE-004 | Physical security, protection from tampering |

### 2.6 Network Assets

| Asset ID | Asset Name | Description | Identifier | Important Protections |
|---|---|---|---|---|
| N-001 | Wireless Local Area Network | Local Wi-Fi network used by member devices | NET-WIFI-001 | WPA2-AES or WPA3, strong password |
| N-002 | Internet Connection | Connection providing access to internet services | NET-WAN-001 | Router firewall, secure configuration |
| N-003 | Router Management Interface | Interface used to configure the router | NET-MGMT-001 | Strong administrator password, restricted access |
| N-004 | DNS Service | Resolves domain names to IP addresses | NET-DNS-001 | Trusted DNS configuration, monitoring |
| N-005 | iMessage Communication Service | Apple's messaging service used to deliver messages | NET-IMSG-001 | Account protection, encryption, software updates |

---

## Task 4: Conduct a Risk Analysis

The risk analysis will be completed separately using the risk assessment template spreadsheet provided for the project. It does not need to be included in the individual journal.

The analysis should consider the assets listed in Task 2 and identify relevant threats, vulnerabilities, likelihood, impact, existing protections, and recommended treatments using the spreadsheet's required format.

Potential risks to consider include:

1. Unauthorized access to a group member's Apple account.
2. Loss or theft of a smartphone containing private information.
3. Exposure of sensitive information through a compromised device.
4. Unauthorized access to the wireless network.
5. Outdated software containing exploitable vulnerabilities.
6. Phishing attacks targeting group members.

**Completion note:** Complete the risk assessment in the provided spreadsheet and include it in the project submission as instructed by the course requirements.
