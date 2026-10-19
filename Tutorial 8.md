# IS355 Tutorial — Network Security Journal

**Course:** IS355 — Networking and Cyber Security  
**Student:** Zane Schutzman  
**Date:** October 19, 2026  
**Project:** Factory Network

---

## Task 1: CIA Protections

The CIA Triad consists of Confidentiality, Integrity, and Availability. Confidentiality means information is only accessible to authorized people. Integrity means data and systems remain accurate and are not changed without permission. Availability means systems and information can be accessed when they are needed.

### Asset 1: Factory Equipment and Industrial Control Systems

- **Protection:** Availability and Integrity
- **Reason:** Factory equipment needs to remain operational so production can continue. Unauthorized changes to equipment settings could damage machinery, create unsafe conditions, or interrupt manufacturing.

### Asset 2: Office Computers and Employee Data

- **Protection:** Confidentiality and Integrity
- **Reason:** Employee information and business documents should only be accessible to authorized employees. Unauthorized access could expose private information, while unauthorized changes could damage files or affect business decisions.

### Asset 3: Customer, Employee, and Business Records

- **Protection:** Confidentiality, Integrity, and Availability
- **Reason:** Business records may contain sensitive information that should only be viewed by authorized people. The information must remain accurate, and employees need access to it to perform their jobs.

### Asset 4: Security Cameras and Video Recordings

- **Protection:** Availability, Confidentiality, and Integrity
- **Reason:** Cameras and recordings need to be available when an incident occurs. Recordings should not be viewed by unauthorized people or deleted or altered because they may be needed for investigations.

### Asset 5: Network Equipment

- **Protection:** Availability, Integrity, and Confidentiality
- **Reason:** Routers, switches, and firewalls connect and protect the network. Unauthorized configuration changes could create security gaps or interrupt communication between devices. Network configuration information should be restricted to authorized administrators.

### Asset 6: Guest Wi-Fi and Guest Devices

- **Protection:** Confidentiality and Availability
- **Reason:** Guests should be able to access the internet without accessing factory equipment, company servers, or employee files. Guest activity should not interfere with the company's network performance.

### Asset 7: Backups and Recovery Copies

- **Protection:** Integrity, Confidentiality, and Availability
- **Reason:** Backups need to be protected from unauthorized access and modification. If data is lost because of equipment failure, an attack, or accidental deletion, usable backups allow the company to restore important systems and information.

### Asset 8: Network Administrator Accounts

- **Protection:** Confidentiality, Integrity, and Availability
- **Reason:** Administrator accounts can make important changes to the network. If attackers take control of these accounts, they could disable security controls, access sensitive data, or interrupt factory operations.

---

## Task 2: Threat Sources and Motivation

### Threat Source 1: Cybercriminals

- **Motivation:** To steal sensitive business information, demand ransom payments, or make money by selling stolen data.

### Threat Source 2: Malicious Insiders

- **Motivation:** A disgruntled or dishonest employee or contractor may want to steal information, damage systems, or disrupt factory operations.

### Threat Source 3: Competitors

- **Motivation:** To obtain confidential business information, production plans, customer information, or other information that could provide a competitive advantage.

### Threat Source 4: Unauthorized Network Users

- **Motivation:** To use the company's internet connection without permission or attempt to access devices and files they should not be able to reach.

### Threat Source 5: Opportunistic Attackers

- **Motivation:** To find and exploit systems with known vulnerabilities. These attackers may use automated tools to search for vulnerable devices connected to a network or exposed to the internet.

### Threat Source 6: Hacktivists

- **Motivation:** To disrupt company services, expose information, or damage public-facing systems to promote a political or social cause.

---

## Task 3: Explore Vulnerabilities

The following CVEs were published during the 12 months before October 19, 2026. Their CVSS Version 3.1 scores, descriptions, weaknesses, and affected products are based on the National Vulnerability Database (NVD) and vendor advisories.

**Important:** NVD and vendors sometimes assign different CVSS scores to the same vulnerability. The source of each score is identified below.

### CVE 1: Critical Severity — CVE-2026-26105

**CVE ID:** [CVE-2026-26105 — NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-26105)

**Date published:** March 10, 2026

**CVSS version 3.1 score:**
- NVD score: 9.3 — Critical
- Microsoft score: 8.1 — High

**CVE description:** Improper neutralization of input during web page generation, also known as cross-site scripting (XSS), in Microsoft Office SharePoint allows an unauthorized attacker to perform spoofing over a network.

**CIA impact according to the NVD CVSS vector:**
- **Confidentiality:** High
- **Integrity:** High
- **Availability:** None

**CWE:** CWE-79 — Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting').

Reference: [CWE-79 — MITRE](https://cwe.mitre.org/data/definitions/79.html)

**Company:** Microsoft.

**Product affected:** Microsoft SharePoint Server, a collaboration platform organizations use to share documents, manage content, and support team workflows. Affected products include SharePoint Enterprise Server 2016, SharePoint Server 2019, and SharePoint Server Subscription Edition in vulnerable versions.

**Simple explanation:** Cross-site scripting happens when an application does not properly handle input that becomes part of a web page. An attacker may be able to introduce harmful content that causes a user to see misleading information or interact with the application in an unsafe way. This can affect the confidentiality and integrity of information.

**Detection and mitigation:**
1. Check whether the organization uses an affected version of SharePoint Server.
2. Review Microsoft's security advisory for the vulnerability.
3. Install the applicable Microsoft security updates.
4. Verify that the installed version meets Microsoft's fixed-version requirements.
5. Continue monitoring SharePoint systems and applying future security updates.

Microsoft's listed fixed build thresholds include:
- SharePoint Enterprise Server 2016: 16.0.5543.1000
- SharePoint Server 2019: 16.0.10417.20102
- SharePoint Server Subscription Edition: 16.0.19725.20076

**References:**
- [NVD vulnerability record](https://nvd.nist.gov/vuln/detail/CVE-2026-26105)
- [Microsoft Security Update Guide](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-26105)

### CVE 2: High Severity — CVE-2026-50478

**CVE ID:** [CVE-2026-50478 — NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-50478)

**Date published:** July 14, 2026

**CVSS version 3.1 score:** 7.8 — High, according to Microsoft.

**CVE description:** A use-after-free vulnerability in the Windows Kernel allows an authorized attacker to elevate privileges locally.

**CIA impact according to the CVSS vector:**
- **Confidentiality:** High
- **Integrity:** High
- **Availability:** High

**CWE:** CWE-416 — Use After Free.

Reference: [CWE-416 — MITRE](https://cwe.mitre.org/data/definitions/416.html)

**Company:** Microsoft.

**Product affected:** Microsoft Windows, including affected Windows client and Windows Server versions listed in the NVD entry. The Windows Kernel is a core component of the operating system that manages system resources and provides essential services to applications.

**Simple explanation:** A use-after-free vulnerability occurs when software continues to use a section of memory after that memory has been released. Under certain conditions, an attacker who already has local access to the computer could exploit the error to gain higher privileges. This could allow the attacker to access information, modify system data, or interfere with system operation.

**Detection and mitigation:**
1. Identify which Windows versions are installed on company computers and servers.
2. Compare those versions with the affected versions in the NVD and Microsoft advisory.
3. Install the appropriate Microsoft security updates.
4. Limit administrator privileges and restrict unnecessary local access.
5. Verify that updates were installed successfully and monitor for unusual privilege changes.

**References:**
- [NVD vulnerability record](https://nvd.nist.gov/vuln/detail/CVE-2026-50478)
- [Microsoft Security Update Guide](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2026-50478)

### CVE 3: Medium Severity — CVE-2026-18671

**CVE ID:** [CVE-2026-18671 — NVD](https://nvd.nist.gov/vuln/detail/CVE-2026-18671)

**Date published:** August 13, 2026

**CVSS version 3.1 score:**
- NVD score: 5.3 — Medium
- IBM score: 6.5 — Medium

**CVE description:** IBM i could allow an attacker to cause a NetServer server thread exception because of an integer overflow during bounds checking in request processing. This could cause a temporary denial of service.

**CIA impact according to the NVD CVSS vector:**
- **Confidentiality:** None
- **Integrity:** None
- **Availability:** Low

**CWE:** CWE-190 — Integer Overflow or Wraparound.

Reference: [CWE-190 — MITRE](https://cwe.mitre.org/data/definitions/190.html)

**Company:** IBM.

**Product affected:** IBM i versions 7.3, 7.4, 7.5, and 7.6. IBM i is an operating system used on IBM Power Systems. NetServer provides network file and print-sharing services for clients.

**Simple explanation:** An integer overflow can occur when a number exceeds the range that a program can safely store. If the software does not correctly check the value, processing a request may cause a server thread to fail. The main stated impact of this vulnerability is a temporary interruption of service.

**Detection and mitigation:**
1. Determine whether the organization uses an affected IBM i version.
2. Review IBM's security bulletin for the correct fix.
3. Apply the appropriate Program Temporary Fix (PTF) for the installed IBM i version.
4. Monitor NetServer and system logs for unexpected thread exceptions or service interruptions.
5. Follow IBM's instructions for testing and applying the fix.

IBM lists the following fixes in its advisory:
- IBM i 7.6: PTF MJ10939
- IBM i 7.5: PTF MJ10938
- IBM i 7.4: PTF MJ10937
- IBM i 7.3: PTF MJ10936

**References:**
- [NVD vulnerability record](https://nvd.nist.gov/vuln/detail/CVE-2026-18671)
- [IBM Security Bulletin for IBM i NetServer](https://www.ibm.com/support/pages/node/7283573)

### Comparison of the Three Vulnerabilities

| Severity | CVE ID | CVSS 3.1 score used | Main issue |
|---|---|---:|---|
| Critical (NVD) | CVE-2026-26105 | 9.3 | Cross-site scripting in SharePoint |
| High | CVE-2026-50478 | 7.8 | Windows Kernel use-after-free |
| Medium (NVD) | CVE-2026-18671 | 5.3 | Integer overflow in IBM i NetServer |

These examples show that vulnerabilities can affect different parts of an organization's technology. A web application vulnerability may threaten the confidentiality and integrity of information, a kernel vulnerability may allow privilege escalation, and a server-processing vulnerability may interrupt service availability.

---

## Task 4: Vulnerability Disclosures

Vulnerability disclosure is the process of reporting a security weakness to the organization responsible for the affected product and deciding when information about the weakness should become public. Coordinated vulnerability disclosure aims to give the vendor time to investigate the issue and prepare a fix before full technical details are released.

I think a vendor may need time before publicly disclosing a vulnerability because it needs to confirm that the report is accurate, understand which products and versions are affected, develop and test a patch, and prepare instructions for customers. Releasing technical details too early could give attackers information they could use before users have a way to protect themselves.

However, keeping a vulnerability secret indefinitely can also be dangerous. Customers may remain exposed without knowing about the risk, and security professionals may be unable to take appropriate precautions.

I think around 90 days is a reasonable general starting point for coordinated disclosure, provided that the researcher and vendor communicate during that period. The appropriate timeline depends on the severity of the vulnerability, how easily it can be exploited, whether attackers are already using it, and how difficult it is to develop a safe fix. A serious vulnerability that is actively being exploited may require faster action.

If a vendor does not respond within a reasonable period, I do not think a researcher should immediately publish every technical detail or a working exploit. The researcher should make reasonable attempts to contact the vendor, document the timeline, and consider contacting a coordination organization or appropriate third party.

If the vendor continues to ignore the report, a carefully limited public disclosure may eventually be justified to alert affected users and encourage a fix. The researcher should consider the potential harm to users, legal obligations, and any applicable bug bounty program rules before publishing.

Bug bounty programs can encourage responsible reporting by providing a clear process for security researchers to report vulnerabilities and sometimes receive rewards for valid findings. Organizations should respond professionally, explain their timelines, and treat good-faith reports seriously.

Overall, I believe coordinated disclosure is usually the best approach because it balances public safety, the vendor's opportunity to fix the problem, and the public's need to know about security risks.

**References:**
- [OWASP Vulnerability Disclosure Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerability_Disclosure_Cheat_Sheet.html)
- [Microsoft Security Response Center — Coordinated Vulnerability Disclosure](https://www.microsoft.com/en-us/msrc/cvd)
- [CERT/CC Vulnerability Disclosure Policy](https://resources.sei.cmu.edu/library/asset-view.cfm?assetid=503330)
- [Broadcom Vulnerability Management](https://www.broadcom.com/support/security-center/vulnerability-management)
- [MITRE CVE Researcher Reservation Guidelines](https://cve.mitre.org/cve/researcher_reservation_guidelines)

---

## Task 5: Find OWASP Top 10 Vulnerabilities

### What Is the Purpose of the OWASP Top 10?

The OWASP Top 10 is an awareness document that identifies major security risks for web applications. It helps developers, security professionals, and organizations understand common and important categories of web application risk so they can prioritize security work.

The OWASP Top 10 is a starting point for improving application security. It is not a complete list of every possible vulnerability, and following it alone does not guarantee that an application is secure.

### OWASP Top 10:2025 Categories

The official OWASP Top 10:2025 contains the following categories:

1. **A01:2025 — Broken Access Control**
2. **A02:2025 — Security Misconfiguration**
3. **A03:2025 — Software Supply Chain Failures**
4. **A04:2025 — Cryptographic Failures**
5. **A05:2025 — Injection**
6. **A06:2025 — Insecure Design**
7. **A07:2025 — Authentication Failures**
8. **A08:2025 — Software or Data Integrity Failures**
9. **A09:2025 — Security Logging and Alerting Failures**
10. **A10:2025 — Mishandling of Exceptional Conditions**

### Why Is the OWASP Top 10 Important for Web Application Developers and Security Professionals?

I think the OWASP Top 10 is important because it gives developers and security professionals a common starting point for identifying and discussing serious web application risks. Developers can use it during design, coding, and testing to consider issues such as access controls, authentication, secure configuration, and input validation before they become security incidents.

Security professionals can use the list to guide code reviews, risk assessments, penetration tests, and discussions about which problems should be fixed first. It also helps teams communicate security risks using consistent terminology.

However, organizations should not assume that addressing only these ten categories makes an application completely secure. They still need threat modeling, secure development practices, security testing, monitoring, patching, and controls suited to their own systems.

Overall, the OWASP Top 10 is valuable because it raises awareness and helps teams prioritize important web application security risks. Using it alongside other security practices can help reduce vulnerabilities and protect users and business information.

**Reference:** [Official OWASP Top 10:2025](https://top10.owasp.org/2025/)

---

## Additional Sources

- [National Vulnerability Database (NVD)](https://nvd.nist.gov/)
- [MITRE Common Weakness Enumeration (CWE)](https://cwe.mitre.org/)
- [OWASP Top 10:2025](https://top10.owasp.org/2025/)
- [OWASP Vulnerability Disclosure Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerability_Disclosure_Cheat_Sheet.html)
