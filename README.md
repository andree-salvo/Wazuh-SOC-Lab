# Wazuh SOC Lab – SIEM Deployment and Endpoint Monitoring

## Lab Documentation

The following write-ups document each phase of my Wazuh SOC Lab, including implementation steps, supporting evidence, results, and lessons learned.

- **Phase 1:** [Lab Setup and Network Connectivity](Documentation/01-Lab-Setup.md)
- **Phase 2:** [Windows Agent Deployment and Event Collection](Documentation/02-Windows-Agent-Deployment.md)
- **Phase 3:** Security Event Simulation *(Planned)*
- **Phase 4:** Alert Investigation *(Planned)*
- **Phase 5:** MITRE ATT&CK Mapping *(Planned)*

## Project Overview

This project focuses on building a hands-on Security Operations Center (SOC) lab using **Wazuh**, an open-source Security Information and Event Management (SIEM) and security monitoring platform.

The purpose of the lab is to gain practical experience deploying a SIEM solution, configuring endpoint monitoring, establishing communication between systems, collecting security logs, and developing foundational security monitoring and threat investigation skills.

The lab consists of a physical Ubuntu laptop running the Wazuh server and a separate computer hosting Windows 10 and Kali Linux virtual machines through Oracle VirtualBox.

The Windows 10 virtual machine serves as a monitored endpoint, while Kali Linux is designated for controlled security testing within the lab environment.

The broader project will involve generating simulated security events, investigating alerts, identifying indicators of compromise (IOCs), and mapping observed activity to the MITRE ATT&CK framework.

**Current Progress:** Lab infrastructure configuration, network connectivity validation, Windows agent deployment, and initial event collection completed.

---

## 1. Project Objectives

The primary objective of this project is to develop practical skills in SIEM deployment, endpoint monitoring, and SOC infrastructure management.

Specific objectives include:

- Deploy and configure a centralized Wazuh SIEM environment.
- Establish network communication between physical and virtual systems.
- Install and configure a Wazuh agent on a Windows 10 endpoint.
- Validate agent connectivity and confirm successful log collection.
- Use the Wazuh dashboard to observe security events and endpoint activity.
- Prepare a controlled environment for future security simulations and incident investigations.
- Develop documentation practices for recording security events, findings, and technical evidence.

These objectives reflect common responsibilities in security operations, including maintaining monitoring infrastructure, collecting endpoint telemetry, and investigating potentially suspicious activity.

## 2. Tools and Technologies Used

| Tool / Technology | Purpose |
|---|---|
| Wazuh | Centralized SIEM platform for security monitoring, log collection, and alert analysis |
| Ubuntu Linux | Operating system hosting the Wazuh server components |
| Windows 10 | Monitored endpoint for collecting Windows security and system events |
| Kali Linux | Dedicated virtual machine for future controlled security testing |
| Oracle VirtualBox | Virtualization platform used to host the Windows and Kali Linux VMs |
| Wazuh Agent | Endpoint software responsible for forwarding monitored event data to the Wazuh server |
| Wazuh Dashboard | Web interface for monitoring agent status, viewing events, and performing security investigations |
| ICMP / Ping | Network troubleshooting utility used to validate connectivity between lab systems |

## 3. Lab Architecture and Environment

### Infrastructure Design

The SOC lab uses a combination of physical hardware and virtual machines to simulate a small security monitoring environment.

Rather than hosting all components on a single computer, the Wazuh server runs on a dedicated physical Ubuntu laptop. The Windows 10 and Kali Linux virtual machines run on a separate computer using VirtualBox.

This configuration provides a centralized monitoring server that communicates with endpoints across the local network.

| System | Role | Environment |
|---|---|---|
| Ubuntu Laptop | Wazuh server | Physical hardware |
| Windows 10 VM | Monitored endpoint | VirtualBox |
| Kali Linux VM | Security testing system | VirtualBox |

### Wazuh Server Components

The Ubuntu laptop hosts the following Wazuh components:

- **Wazuh Manager:** Receives and processes information from monitored endpoints.
- **Wazuh Indexer:** Stores and indexes security event data for searching and analysis.
- **Wazuh Dashboard:** Provides a browser-based interface for viewing monitored endpoints and investigating events.

### Network Configuration

The lab systems communicate over the same local network.

| System | IP Address | Connectivity |
|---|---|---|
| Wazuh Server | 10.0.0.X | Reachable |
| Windows 10 VM | 10.0.0.X | Connected to Wazuh server |
| Kali Linux VM | 10.0.0.X | Connected to lab network |

*IP addresses are represented with placeholders in the public documentation.*

---

## 4. Implementation – Phase 1: Infrastructure Setup and Network Validation

### What I Did

I configured a dedicated Ubuntu laptop to host the Wazuh SIEM infrastructure and used a separate computer running Oracle VirtualBox to host Windows 10 and Kali Linux virtual machines.

After establishing the lab environment, I verified network connectivity between the physical server and both virtual machines.

The following connectivity tests were performed:

1. Tested communication from the Windows 10 virtual machine to the Ubuntu Wazuh server using the `ping` command.
2. Tested communication from the Kali Linux virtual machine to the Wazuh server using the `ping` command.
3. Opened the Wazuh web interface from a browser on the separate PC.
4. Confirmed that the Wazuh login page and dashboard were accessible through the server's local network address.

### Why I Did It

Reliable network communication is essential for centralized security monitoring.

Before deploying and managing endpoint agents, I needed to verify that the Wazuh server was accessible from other lab systems.

Validating connectivity also helped establish a working foundation for endpoint telemetry collection, dashboard access, and future security testing.

### Results and Findings

All initial connectivity tests were successful.

| Validation Test | Result |
|---|---|
| Windows 10 VM to Wazuh server | Successful |
| Kali Linux VM to Wazuh server | Successful |
| Wazuh web interface accessibility | Successful |
| Wazuh dashboard accessibility | Successful |

The results confirmed that the virtual machines could communicate with the physical Wazuh server and that the dashboard was accessible remotely over the local network.

### Supporting Evidence

**Windows 10 VM – Network Connectivity**

![Windows 10 VM ping to Wazuh server](https://github.com/andree-salvo/Wazuh-Soc-SIEM-Lab/raw/main/Screenshots/screenshots-01-windows-ping-wazuh.png)

**Kali Linux – Network Connectivity**

![Kali Linux VM ping to Wazuh server](https://github.com/andree-salvo/Wazuh-Soc-SIEM-Lab/raw/main/Screenshots/screenshot-03-kali-ping-wazuh.png)

**Wazuh Login Page**

![Wazuh login page](https://github.com/andree-salvo/Wazuh-Soc-SIEM-Lab/raw/main/Screenshots/screenshot-04-login-page.png)

**Wazuh Dashboard Access**

![Wazuh dashboard](https://github.com/andree-salvo/Wazuh-Soc-SIEM-Lab/raw/main/Screenshots/screenshot-05-Wazuh-dashboard-access.png)

### What I Learned

This phase strengthened my understanding of:

- Configuring a security lab using physical and virtual infrastructure.
- Establishing communication between systems on a local network.
- Using ICMP connectivity tests to verify network reachability.
- Accessing a centralized SIEM dashboard from another computer.
- Understanding how SIEM components and monitored endpoints interact in a distributed environment.

---

## 5. Implementation – Phase 2: Windows 10 Wazuh Agent Deployment

### What I Did

I installed and configured the Wazuh agent on the Windows 10 virtual machine to enable centralized monitoring through the Ubuntu Wazuh server.

After configuring the endpoint agent, I used the Wazuh dashboard to verify its registration and operational status.

I also accessed the Threat Hunting section to confirm that Windows event data was being received by the SIEM.

The implementation involved:

1. Installing the Wazuh agent on the Windows 10 virtual machine.
2. Configuring the agent to communicate with the Wazuh server.
3. Verifying that the endpoint appeared in the Wazuh agent inventory.
4. Confirming that the agent reported an active status.
5. Reviewing the endpoint's details in the Wazuh dashboard.
6. Examining the Threat Hunting interface to verify the presence of Windows event data.

### Why I Did It

A centralized SIEM requires endpoint telemetry to provide visibility into activity occurring across monitored systems.

Deploying the Wazuh agent allowed the Windows 10 virtual machine to communicate monitored events to the Wazuh infrastructure.

This was an important step toward developing a functioning SOC environment capable of supporting event investigation and security analysis.

The deployment also provided hands-on experience with endpoint onboarding, agent management, and log collection verification.

### Windows Endpoint Configuration

| Configuration | Value |
|---|---|
| Endpoint | Windows 10 VM |
| Monitoring Solution | Wazuh Agent |
| Agent Status | Active |
| Centralized Server | Ubuntu Wazuh Server |
| Communication | Local Network |
| Event Visibility | Confirmed in Wazuh Threat Hunting |

### Results and Findings

The Windows 10 endpoint was successfully integrated into the Wazuh monitoring environment.

The following results were observed:

- The Windows 10 endpoint appeared in the Wazuh dashboard.
- The Wazuh agent reported an active status.
- Agent details were accessible from the management interface.
- Windows event records were visible within the Threat Hunting section.

These results confirmed that the endpoint had established communication with the Wazuh server and that event telemetry was being collected and made available for analysis.

### Supporting Evidence

**Windows 10 Agent – Active Status**

![Windows 10 Wazuh agent active](https://github.com/andree-salvo/Wazuh-Soc-SIEM-Lab/raw/main/Screenshots/windows10-agent-active.png)

**Windows Agent Details**

![Windows Wazuh agent details](https://github.com/andree-salvo/Wazuh-Soc-SIEM-Lab/raw/main/Screenshots/windows-agent-details.png)

**Windows Event Collection – Threat Hunting**

![Windows events in Wazuh](https://github.com/andree-salvo/Wazuh-Soc-SIEM-Lab/raw/main/Screenshots/windows-10-agent-events.png)

### What I Learned

This phase provided practical experience with:

- Installing and configuring endpoint monitoring agents.
- Connecting Windows endpoints to a centralized SIEM platform.
- Verifying successful endpoint registration and communication.
- Monitoring agent health and operational status.
- Locating collected event data within the Wazuh dashboard.
- Understanding the importance of endpoint telemetry for security monitoring and incident investigation.

---

## 6. Overall Project Results

The completed phases established the foundation for a centralized SOC monitoring environment.

| Project Milestone | Status |
|---|---|
| Wazuh server environment established | Completed |
| Windows 10 and Kali Linux VMs configured | Completed |
| Network connectivity validated | Completed |
| Wazuh dashboard access verified | Completed |
| Windows 10 Wazuh agent installed | Completed |
| Windows endpoint agent status verified | Completed |
| Windows event collection confirmed | Completed |
| Security event simulation | Planned |
| Alert investigation and IOC documentation | Planned |
| MITRE ATT&CK mapping | Planned |

The environment now provides centralized visibility into monitored Windows endpoint activity and is prepared for additional security monitoring exercises.

## 7. Skills Demonstrated

This project demonstrates foundational skills relevant to cybersecurity and IT operations.

**Security Monitoring and SIEM Administration**
- Wazuh deployment and administration
- Endpoint onboarding and agent management
- Centralized security event collection
- SIEM dashboard navigation
- Initial event visibility validation

**Systems and Network Administration**
- Ubuntu Linux server environment management
- Windows endpoint configuration
- Virtual machine administration using VirtualBox
- Local network connectivity validation
- Basic network troubleshooting

**Technical Documentation**
- Recording infrastructure configurations
- Documenting implementation procedures
- Capturing screenshots as technical evidence
- Validating system functionality
- Reporting implementation results

## 8. Next Steps

The next stages of the project are intended to expand the lab from basic infrastructure and endpoint monitoring into security detection and investigation exercises.

Planned activities include:

1. Generate controlled security events within the lab environment.
2. Review Wazuh alerts and investigate relevant event details.
3. Identify and document indicators of compromise where applicable.
4. Map observed behavior to relevant MITRE ATT&CK techniques.
5. Document investigation procedures, evidence, findings, and lessons learned.

These activities will build upon the existing SIEM infrastructure to develop practical threat detection and incident analysis skills.

## 9. Conclusion

This project provided hands-on experience building the foundation of a Security Operations Center environment using Wazuh.

By deploying a centralized SIEM server on Ubuntu, configuring virtualized Windows and Kali Linux systems, validating network communication, and integrating a Windows 10 endpoint with Wazuh, I established a functional environment for centralized endpoint monitoring.

The successful collection of Windows event data demonstrated the ability to configure and validate the essential components of a SIEM-based monitoring environment.

Through this work, I developed practical experience with SIEM infrastructure, network connectivity, endpoint agent deployment, event collection, and technical documentation.

The environment also provides a foundation for further learning in security alert investigation, threat detection, and incident response.
