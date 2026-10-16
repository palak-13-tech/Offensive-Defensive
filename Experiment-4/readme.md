Experiment 4: Firewall Configuration and Intrusion Detection Using pfSense and Snort
Overview
This experiment demonstrates how to configure basic firewall rules using pfSense and enable Snort IDS to monitor network traffic and detect suspicious activity in a controlled virtual lab environment.

Objective
Configure basic firewall rules using pfSense.
Install and enable Snort Intrusion Detection System (IDS).
Generate test network traffic and observe traffic filtering.
Analyze firewall logs and Snort alerts to understand network security monitoring.
Tools and Technologies
pfSense – Firewall and router software.
Snort IDS – Network intrusion detection tool.
Kali Linux – Test traffic generation and security testing.
Metasploitable 2 – Intentionally vulnerable target machine.
Oracle VirtualBox – Virtual lab environment.
Lab Setup
The experiment uses three virtual machines:

Component	Purpose
pfSense	Firewall and network traffic management
Kali Linux	Test traffic generation
Metasploitable 2	Vulnerable target for lab testing
All testing is performed within an isolated virtual network.

Procedure
Download the pfSense ISO and create a virtual machine in VirtualBox.
Install pfSense and configure its WAN and LAN interfaces.
Connect Kali Linux and Metasploitable 2 to the isolated lab network.
Access the pfSense web interface and configure basic firewall rules.
Install Snort and enable it on the required network interface.
Generate test network traffic from Kali Linux within the lab.
Examine firewall logs and Snort alerts to observe traffic filtering and suspicious activity detection.
Expected Observations
Firewall rules allow or block traffic according to their configuration.
Snort generates alerts when traffic matches configured detection rules.
Logs help identify traffic patterns and investigate suspicious activity.
Result
The experiment demonstrates the configuration of firewall rules in pfSense and the use of Snort IDS for network traffic monitoring and suspicious activity detection.

Security Note
All testing should be conducted in an authorized, isolated lab environment. Do not scan or test systems without permission.

Conclusion
This experiment provides practical understanding of firewall configuration, intrusion detection, and the importance of monitoring network traffic to improve network security.
