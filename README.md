# Azure Honeypot: Simulating Real-World Cyber Attacks
<img src="https://i.imgur.com/IY5sfCJ.png" >

## Introduction

 I am excited to introduce my latest project, which centers on constructing a honeypot in Azure to replicate real-world cyber attacks. This endeavor highlights my proficiency in Azure security, incident response, and environment hardening strategies. Through this project, I aim to demonstrate not only my technical abilities but also my commitment to enhancing cybersecurity defenses and readiness in today's digital landscape.

## Objective
The primary goal of this project was to [set up a virtual machine that was intentionally vulnerable](https://github.com/felixsalto1/Azure-VM-Config/blob/main/README.md) within the Azure enviorment to attract and analyze cyber attacks. This initiative enabled me to gain deeper insights into the tactics and techniques employed by attackers, thereby enhancing my understanding of cybersecurity threats. While also demonstrating my capability to promptly and efficiently respond to any identified issues, showcasing my proficiency in incident response and threat mitigation within cloud environments.

## Technologies, Regulations, and Azure Components Employed:

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault for Secure Secrets Management
- Azure Storage Account for Data Storage
- Microsoft Sentinel for Security Information and Event Management (SIEM)
- Microsoft Defender for Cloud to Protect Cloud Resources
- Windows Remote Desktop for Remote Access
- Command Line Interface (CLI) for System Management
- PowerShell for Automation and Configuration Management
- [NIST SP 800-53 Revision 5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final) for Security Controls
- [NIST SP 800-61 Revision 2](https://www.nist.gov/privacy-framework/nist-sp-800-61) for Incident Handling Guidance

## Methodology

- <b>*Creating the honeynet*</b>: I began by [running a vulnerable virtual machine](https://github.com/felixsalto1/Azure-VM-Config/blob/main/README.md) in Azure, simulating an insecure environment.

- <b>*Monitoring and analysis*</b>: Azure was configured to ingest log sources from various resources into a log analytics workspace. Microsoft Sentinel was then used to build attack maps, trigger alerts, and create incidents based on the collected data.

- <b>*Security metrics measurement*</b>: I observed the environment for 24 hours, recording key security metrics while it was insecure. This provided a baseline to compare against after implementing remediation measures.

- <b>*Incident response and remediation*</b>: After addressing the incidents and identifying vulnerabilities, I began the process of hardening the environment by applying security best practices and Azure-specific recommendations.

- <b>*Post-remediation analysis*</b>: I re-observed the environment for another 24 hours to measure security metrics again, comparing the results with the initial baseline.


## Architecture Prior to Implementing Hardening Measures and Security Controls
 <img src="https://i.imgur.com/BscJ0qj.png" >

<b>Before Hardening Measures and Security Controls:</b>

- In the "BEFORE" stage of the project, all resources were initially deployed with public exposure to the internet. This setup was intentionally insecure to attract potential cyber attackers and observe their tactics. The Virtual Machine had both their Network Security Groups (NSGs) and built-in firewalls wide open, allowing unrestricted access from any source. Additionally, all other resources, such as storage accounts and databases, were deployed with public endpoints visible to the internet, without utilizing any Private Endpoints for added security.

## Architecture After Implementing Hardening Measures and Security Controls
 <img src="https://i.imgur.com/GPs3liY.png" >
 
 <b>For the "AFTER" stage, I implemented a series of hardening measures and security controls to improve the environment's overall security posture. These improvements included:</b>

- <b>Network Security Groups (NSGs)</b>: I hardened the NSGs by blocking all inbound and outbound traffic, with the sole exception of my own public IP address. This ensured that only authorized traffic from a trusted source was allowed to access the virtual machines.

- <b>Built-in Firewalls</b>: I configured the built-in firewalls on the virtual machines to restrict access and protect the resources from unauthorized connections. This step involved fine-tuning the firewall rules based on the specific requirements of each VM, thereby minimizing the potential attack surface.

- <b>Private Endpoints</b>: To enhance the security of other Azure resources, I replaced the public endpoints with Private Endpoints. This ensured that access to sensitive resources, such as storage accounts and databases, was limited to the virtual network and not exposed to the public internet. As a result, these resources were protected from unauthorized access and potential attacks.

By comparing the security metrics before and after implementing these hardening measures and security controls, I was able to demonstrate the effectiveness of each step in improving the overall security posture of the Azure environment.

## Attack Maps Before Hardening / Security Controls
<br />


> <b>NOTE: The attack maps were generated by extracting data from a workbook utilizing pre-built [KQL .JSON](https://github.com/AmiliaSalva/Cloud-SOC-Project-Resources/blob/main/MS%20Sentinel%20Maps%20(JSON)/linux-ssh-auth-fail.json) map files. These files provided a structured representation of the attack patterns and their associated data, 
enabling the creation of visualizations that effectively illustrated the cyber threats and their impact on the system.</b>


 <br />
 <br />
 
- <b>This attack map demonstrates the consequences of leaving the Network Security Group (NSG) open, as it allowed for malicious traffic to flow unimpeded. This visualization underscores the importance of implementing proper security measures, such as restricting NSG rules, to prevent unauthorized access and minimize potential threats.</b>


<img src="https://i.imgur.com/HNBdFxc.png" >

 <br />
 <br />
 
 - <b>This attack map showcases numerous RDP and SMB failures, illustrating the persistent attempts by potential attackers to exploit these protocols. The visualization emphasizes the need for securing remote access and file sharing services to protect against unauthorized access and potential cyber threats.</b>
 
<img src="https://i.imgur.com/0q1hYJV.png" >

 <br />
 <br />

## Attack Maps After Hardening / Security Controls

> All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.

 <br />
 <br />
 
## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-04-11 18:06:00 PM
Stop Time 2024-04-12 18:06:00 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 21182
| SecurityAlert (Microsoft Defender for Cloud)            | 0
| SecurityIncident (Sentinel Incidents)        | 343
| NSG Inbound Malicious Flows Allowed | 969



## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-04-13 16:42
Stop Time	2024-03-15 16:42


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 783
| SecurityAlert (Microsoft Defender for Cloud)            | 0
| SecurityIncident (Sentinel Incidents)        | 0
| NSG Inbound Malicious Flows Allowed | 0

## Conclusion

In conclusion, I established a compact yet potent honeypot using Microsoft Azure's resilient cloud infrastructure. Leveraging Microsoft Sentinel, I configured alerts and incident generation based on ingested logs from implemented watch lists. Initial baseline metrics were established in the unprotected environment, prior to the introduction of any security measures. Subsequently, a series of security protocols were implemented to bolster the network against potential threats.

Comparing pre- and post-implementation metrics revealed a notable decrease in security events and incidents, underscoring the efficacy of the implemented security measures. It's worth noting that if the network's resources had been actively utilized by regular users, it's conceivable that a greater number of security events and alerts could have occurred within the 24-hour timeframe following the implementation of security controls.
