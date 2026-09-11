# Security Countermeasures & Infrastructure Hardening Framework

## Overview

This project presents a security countermeasures and infrastructure hardening framework that I developed to demonstrate how defensive controls can be selected, evaluated and applied across a fictional enterprise environment.

For this portfolio project, the environment is referred to as the Aegis Research Network.

The project considers security controls across Windows servers, Linux systems, desktop endpoints, public-facing web services, DNS infrastructure, proxy services and database systems.

Rather than simply identifying individual security controls, the project considers their purpose, limitations and how they contribute to a layered defence strategy.

---

## Project Aim

The aim of this project is to demonstrate how appropriate countermeasures can reduce the likelihood or impact of common attack techniques throughout a penetration testing lifecycle.

The framework considers:

- reconnaissance reduction
- authentication security
- least privilege
- operating system hardening
- patch and vulnerability management
- cryptographic protection
- DNS security
- network egress controls
- security logging and monitoring
- application security
- vulnerability-specific remediation

---

## Fictional Infrastructure

<img width="2788" height="1536" alt="BrownSystemInfrastructure" src="https://github.com/user-attachments/assets/3dd0601b-dab3-4876-a386-f0b314e44e73" />



The Aegis Research Network represents a mixed enterprise environment containing:

- Windows Server domain controllers
- Windows enterprise desktop systems
- Linux application servers
- public-facing web services
- DNS infrastructure
- proxy services
- database servers
- internal and DMZ network segments

The environment was designed to allow different defensive controls to be considered across multiple operating systems, services and attack scenarios.

---

# Reconnaissance Countermeasures

## Restrict DNS Zone Transfers

DNS zone transfers can provide valuable reconnaissance information, including hostnames, IP addresses and network structure.

Restricting zone transfers to authorised DNS servers reduces unnecessary disclosure of infrastructure information.

This does not prevent individual DNS queries or alternative reconnaissance techniques, so the control should form part of a wider layered defence strategy.

---

## Restrict ICMP Responses

ICMP echo requests can assist attackers with identifying active hosts during network reconnaissance.

Restricting unnecessary ICMP responses can make straightforward host discovery more difficult.

However, systems may still be discovered through TCP, UDP and alternative ICMP probes.

The control therefore reduces reconnaissance efficiency rather than making systems invisible.

---

# Authentication Security

## Password and Account Lockout Policies

Strong password policies and appropriately configured account-lockout controls can reduce the effectiveness of brute-force and password-guessing attacks.

Potential benefits include:

- reducing repeated authentication attempts
- increasing password complexity
- limiting automated password attacks
- protecting privileged accounts

Account lockout must be configured carefully because overly aggressive settings can create denial-of-service opportunities if attackers intentionally lock legitimate accounts.

---

## Multi-Factor Authentication

Multi-factor authentication provides additional protection when passwords are compromised.

MFA is particularly valuable for:

- privileged accounts
- administrative systems
- remote administration
- sensitive infrastructure

It should not be treated as a complete defence because attackers may still exploit vulnerable services, steal active sessions or abuse other authentication mechanisms.

---

# Linux Server Hardening

## Patch Management

Operating systems, kernels and installed applications should receive regular security updates.

Prompt patching reduces exposure to publicly known vulnerabilities that attackers may exploit to gain access or escalate privileges.

Updates should be tested where systems perform critical workloads because software changes may introduce compatibility or stability problems.

---

## Least Privilege and sudo Restrictions

Administrative privileges should be tightly controlled.

Standard users should receive only the permissions required for their role, while privileged activity should be limited and monitored.

Restricting sudo permissions can reduce the impact of a compromised standard account by limiting an attacker's ability to gain full administrative control.

---

# Endpoint Security

## Restrict Local Administrator Access

Ordinary desktop users should not routinely operate with local administrator privileges.

Restricting administrative permissions can reduce an attacker's ability to:

- install malicious software
- disable security controls
- modify system configurations
- establish persistence
- escalate a compromise

Least privilege should be combined with patching, endpoint protection and vulnerability management.

---

## Application Isolation and Sandboxing

Application sandboxing can restrict the resources and system functions available to an application.

This can reduce the impact of malicious code executed through compromised or vulnerable software.

Sandboxing is not a complete security boundary and should therefore complement other endpoint security measures.

---

# Cryptographic Security

## Secure TLS and HTTPS

Public-facing applications should protect sensitive network communications using HTTPS and appropriately configured TLS.

Secure TLS configuration helps protect:

- credentials
- session information
- personal information
- application data

Legacy protocols and weak cryptographic configurations should be disabled.

TLS protects information while it is being transmitted but does not protect data after the endpoint itself has been compromised.

---

## Key and Certificate Management

Cryptographic keys and certificates must be securely managed throughout their lifecycle.

Important controls include:

- restricted access to private keys
- secure key storage
- certificate renewal
- certificate inventories
- key replacement procedures
- monitoring of privileged access

Weak key management can undermine otherwise strong cryptographic systems.

---

# DNS Security

## DNSSEC

Domain Name System Security Extensions provide mechanisms for verifying the authenticity and integrity of DNS information.

DNSSEC can help protect against attacks where forged DNS information is introduced into the name-resolution process.

DNSSEC does not encrypt DNS traffic and requires appropriate key management and configuration.

---

## Restrict Recursive DNS

Internet-facing authoritative DNS servers should not provide unrestricted recursive resolution where it is unnecessary.

Separating authoritative and recursive DNS services reduces exposure and limits opportunities for DNS cache-related attacks.

Internal recursive resolution can instead be restricted to trusted clients.

---

# Command-and-Control and Data Exfiltration

## Network Egress Filtering

Outbound network traffic should be restricted according to legitimate business requirements.

A deny-by-default and permit-by-exception approach can reduce opportunities for compromised systems to:

- connect to command-and-control infrastructure
- communicate over unnecessary ports
- access malicious destinations
- exfiltrate sensitive information

Attackers may attempt to hide malicious traffic within commonly permitted services such as HTTPS, so egress filtering should be combined with monitoring.

---

## Centralised Proxy Logging

Proxy logs can provide important visibility into outbound communications.

Monitoring may identify:

- unusual destinations
- repeated connections
- unexpected user-agent strings
- command-and-control beaconing
- unusual transfer volumes
- potential data exfiltration

Centralised logging is primarily a detective control, so effective alerting and incident-response processes are also required.

---

# Vulnerability-Specific Countermeasures

## SQL Injection

Applications should use parameterised queries or prepared statements rather than dynamically constructing SQL commands from user input.

Separating user-supplied values from the SQL command structure reduces the likelihood that malicious input will be interpreted as executable SQL.

Additional controls can include:

- server-side input validation
- least-privileged database accounts
- secure application development
- vulnerability testing
- appropriate error handling

---

## Stack-Based Buffer Overflow

Memory corruption vulnerabilities should primarily be addressed by removing or correcting the vulnerable software.

Defensive measures include:

- applying vendor security updates
- maintaining current software versions
- vulnerability management
- restricting unnecessary network exposure
- least privilege
- modern operating-system exploit protections

Correcting the vulnerable code removes the underlying weakness rather than relying solely on compensating controls.

---

## Broken Access Control

Applications should enforce authorisation on the server for every request involving protected resources or functionality.

Applications should never assume that a user is authorised simply because they can access or modify a URL, parameter or object identifier.

Controls should include:

- server-side authorisation
- role-based access control
- least privilege
- secure session management
- access-control testing
- logging of denied requests

---

# Layered Defence

One of the main conclusions from developing this project is that individual countermeasures rarely provide complete protection.

For example:

Password controls do not prevent exploitation of vulnerable software.

MFA does not prevent every form of session compromise.

TLS does not protect information once the server itself has been compromised.

Egress filtering may not identify command-and-control traffic hidden within authorised protocols.

Security controls are therefore most effective when combined as part of a defence-in-depth strategy.

---

# Preventative and Detective Controls

The framework includes both preventative and detective security measures.

Preventative controls attempt to stop or limit an attack.

Examples include:

- least privilege
- MFA
- patch management
- DNS restrictions
- parameterised SQL queries
- egress filtering

Detective controls help identify suspicious activity that has already begun.

Examples include:

- centralised logging
- proxy monitoring
- authentication monitoring
- suspicious connection analysis
- security alerting

Combining both types of control provides stronger protection than relying exclusively on either approach.

---

# Skills Demonstrated

This project demonstrates my understanding of:

- security countermeasure selection
- defence in depth
- reconnaissance mitigation
- Windows security
- Linux hardening
- Active Directory security
- authentication controls
- multi-factor authentication
- least privilege
- patch management
- endpoint hardening
- TLS and cryptography
- key management
- DNS security
- DNSSEC
- network egress filtering
- security logging and monitoring
- command-and-control detection
- data-exfiltration mitigation
- SQL injection prevention
- buffer-overflow mitigation
- access-control security
- vulnerability remediation
- critical evaluation of security controls

---

# Project Reflection

Developing this project strengthened my understanding that identifying a security control is only part of defensive security.

A countermeasure must also be appropriate for the system being protected, realistically deployable and evaluated against the attack technique it is intended to mitigate.

Most controls also have limitations.

Understanding these limitations is important because it prevents individual security technologies from being treated as complete solutions.

The project reinforced the importance of defence in depth, where preventative, detective and corrective controls operate together to reduce both the likelihood and potential impact of compromise.

It also strengthened my understanding of the relationship between penetration testing and defensive security.

A penetration tester should not only be capable of identifying and exploiting weaknesses but should also understand how those weaknesses can be effectively mitigated and how recommended controls may affect the organisation operating them.
