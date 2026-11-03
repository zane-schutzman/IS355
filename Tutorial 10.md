# Week 10 - Tutorial 10: Cyber Security Controls

## Task 1 - Essential Eight Mitigation Strategies

The Essential Eight is a set of cybersecurity strategies designed to protect organizations from common cyber threats. For my project, I selected four strategies that would help protect the company's online shopping platform, customer information, employee accounts, and business systems.

### 1. Application Control

**Group:** Prevent Malware Delivery and Execution

**Description:**

Application control prevents unauthorized or unapproved software from running on company computers and servers. This helps reduce the risk of malware being installed or executed.

**How I would apply it to my project:**

The company would configure its employee computers and servers to only allow approved applications to run. For example, employees who access the customer database would only be able to use authorized business applications. If an employee accidentally downloads an unauthorized program containing malware, application control could prevent that program from running.

**Assets Protected:**
- Employee computers
- Company servers
- Customer database
- Online shopping platform

**Why I selected it:**

I selected application control because malware could allow attackers to access company systems and customer information. Restricting which applications can run would help prevent unauthorized software from compromising the company's systems.

### 2. Patch Applications

**Group:** Prevent Malware Delivery and Execution

**Description:**

Patching applications involves regularly updating software to fix security vulnerabilities. Attackers often take advantage of outdated software to gain unauthorized access to systems.

**How I would apply it to my project:**

The company would regularly update its website software, database applications, web browsers, and other business applications. For example, if a security vulnerability is discovered in the software running the online shopping platform, the company would install the latest security update to prevent attackers from exploiting that vulnerability.

**Assets Protected:**
- Online shopping website
- Database software
- Employee computers
- Company servers

**Why I selected it:**

I selected patch applications because outdated software can create security weaknesses that attackers can exploit. Keeping applications updated would reduce the risk of someone gaining access to customer information through a known vulnerability.

### 3. Multi-Factor Authentication (MFA)

**Group:** Limit the Extent of Cyber Security Incidents

**Description:**

Multi-factor authentication requires users to provide more than one form of verification before accessing an account. This provides additional protection if a password is stolen or compromised.

**How I would apply it to my project:**

The company would require employees and administrators to use multi-factor authentication when accessing important systems, especially the customer database and website management accounts. For example, an administrator would enter their password and then approve a login request through an authentication application. Even if an attacker obtained the administrator's password, they would still need the second verification method.

**Assets Protected:**
- Administrator accounts
- Employee accounts
- Customer database
- Website management system

**Why I selected it:**

I selected MFA because compromised accounts can allow attackers to access sensitive company information. This is especially important for administrator accounts because they have greater access to company systems. MFA would make it harder for attackers to access these accounts using stolen passwords.

### 4. Regular Backups

**Group:** Recover Data and System Availability

**Description:**

Regular backups involve creating copies of important information and storing them so they can be restored if data is lost, damaged, or encrypted by ransomware.

**How I would apply it to my project:**

The company would regularly back up its customer database, website files, and important business records. Backups would be stored separately from the main systems and protected from unauthorized access. The company would also test its backups to make sure information can be restored if a ransomware attack or system failure occurs.

**Assets Protected:**
- Customer database
- Website files
- Business records
- Company servers

**Why I selected it:**

I selected regular backups because losing customer information or access to the online shopping platform could seriously affect the business. Having separate backups would allow the company to restore important information and continue operating after a cyberattack.

### Reasons for Selecting These Four Strategies

I selected these four Essential Eight strategies because they address some of the biggest security risks facing my project. Application control and patching help prevent malware and attacks that exploit outdated software. Multi-factor authentication helps protect employee and administrator accounts from unauthorized access. Regular backups help the company recover important information if an attack or system failure occurs.

The other four strategies are also useful, but I did not prioritize them for this selection:

- **Configure Microsoft Office Macro Settings:** This would help prevent malicious macros from running in Office documents. However, protecting the online shopping platform and customer database was a higher priority for my project.
- **User Application Hardening:** This reduces vulnerabilities in applications such as web browsers. It is useful, but I prioritized application control and patching as broader protections.
- **Restrict Administrative Privileges:** This limits the actions users can perform on company systems. It is important, but I prioritized MFA to address the risk of compromised administrator credentials.
- **Patch Operating Systems:** This protects computers and servers from vulnerabilities in outdated operating systems. It remains important, but I prioritized application patching for the software used by the online shopping platform.

These strategies would work together to reduce the chances of a cyberattack and limit the damage if an incident occurs.

---

## Task 2 - NIST SP 800-53 Security Controls

NIST SP 800-53 provides a catalog of security controls that organizations can use to protect their information systems. I selected six base controls from five different control families that are relevant to my project.

### 1. AC-2 - Account Management

**Family:** Access Control

**Description:**

Account Management focuses on creating, managing, monitoring, and removing user accounts within an organization.

**Why it is important:**

The company needs to control who can access its systems and customer information. If employee accounts are not properly managed, former employees or unauthorized users could continue accessing company systems.

**How I would apply it to my project:**

The company would create individual accounts for employees and administrators. When an employee leaves the company, their account would be disabled or removed. The company would also regularly review active accounts to identify accounts that are no longer needed.

**Assets Protected:**
- Employee accounts
- Administrator accounts
- Customer database
- Company systems

### 2. AC-6 - Least Privilege

**Family:** Access Control

**Description:**

Least privilege means users should only receive the permissions necessary to complete their assigned responsibilities.

**Why it is important:**

Giving employees unnecessary access increases the risk of information being changed, stolen, or deleted. Limiting permissions reduces the amount of damage an attacker could cause if an employee account is compromised.

**How I would apply it to my project:**

Customer service employees would only be able to view the customer orders and shipping information needed for their jobs. They would not have permission to change administrator settings or access sensitive database management functions. Only authorized administrators would receive those permissions.

**Assets Protected:**
- Customer information
- Customer database
- Administrator settings
- Business systems

### 3. IA-2 - Identification and Authentication

**Family:** Identification and Authentication

**Description:**

Identification and Authentication requires users to identify themselves and prove their identity before accessing company systems.

**Why it is important:**

The company needs to make sure that people accessing its systems are authorized users. Without proper authentication, attackers could gain access using stolen or guessed credentials.

**How I would apply it to my project:**

Employees and administrators would use individual usernames and passwords to access company systems. Multi-factor authentication would also be required for important accounts. For example, an administrator would need to enter a password and approve a second verification request before accessing the customer database.

**Assets Protected:**
- Employee accounts
- Administrator accounts
- Customer database
- Website management system

### 4. AU-2 - Event Logging

**Family:** Audit and Accountability

**Description:**

Event Logging involves identifying the types of activities that need to be recorded by an organization's information systems.

**Why it is important:**

Recording system activities helps the company identify suspicious behavior and investigate security incidents. Without logs, it could be difficult to determine how an attacker accessed the system or what information they viewed or changed.

**How I would apply it to my project:**

The company would record important activities, including successful and failed login attempts, administrator access, changes to customer records, and database activity. If an unauthorized user accessed the customer database, administrators could review the logs to investigate what happened.

**Assets Protected:**
- Customer database
- Administrator accounts
- Website management system
- Company servers

### 5. CM-6 - Configuration Settings

**Family:** Configuration Management

**Description:**

Configuration Settings involves establishing and maintaining secure settings for company information systems.

**Why it is important:**

Incorrect system configurations can create security vulnerabilities. For example, leaving unnecessary services enabled or allowing unrestricted access to servers could make it easier for attackers to compromise company systems.

**How I would apply it to my project:**

The company would configure its web servers and database servers using approved security settings. Unnecessary services would be disabled, administrative access would be restricted, and default passwords would be changed. The company would also regularly review its configurations to make sure systems remain secure.

**Assets Protected:**
- Web servers
- Database servers
- Online shopping platform
- Company network

### 6. CP-9 - System Backup

**Family:** Contingency Planning

**Description:**

System Backup involves creating and maintaining backups of important information and system data.

**Why it is important:**

A cyberattack, hardware failure, or ransomware infection could result in the loss of important company information. Backups allow the company to restore its systems and continue operating.

**How I would apply it to my project:**

The company would regularly back up its customer database, website files, and important business records. Backup copies would be stored separately from the main network and protected from unauthorized access. The company would also test its backups to make sure information can be successfully restored after an incident.

**Assets Protected:**
- Customer database
- Website files
- Business records
- Company servers

---

## Summary

The Essential Eight and NIST SP 800-53 controls provide different ways to improve the security of my project. The Essential Eight strategies focus on preventing malware, limiting security incidents, and recovering information after an attack. The NIST controls provide more specific requirements for managing accounts, limiting permissions, verifying identities, recording system activity, configuring systems securely, and backing up information.

By implementing these controls, the company would be better prepared to protect customer information, prevent unauthorized access, identify suspicious activity, and recover from cyber incidents.

Together, these controls would help protect the online shopping platform and reduce the potential impact of a cybersecurity attack.
