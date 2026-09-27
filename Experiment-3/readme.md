# Experiment 3: Basic Network Traffic Analysis with Wireshark

## Objective

To capture and analyze network packets using Wireshark and identify network traffic and plaintext information transmitted over insecure protocols in an isolated laboratory environment.

## Environment

- Kali Linux – Attacker/Analysis Machine
- Metasploitable 2 – Victim/Test Machine
- VirtualBox / VMware
- Host-Only Adapter or Internal Network
- Wireshark
- Nmap
- tcpdump
- tshark

## Network Configuration

Both Kali Linux and Metasploitable 2 were configured on an isolated Host-Only Adapter or Internal Network.

### IP Addresses Used

| Machine | Role | IP Address |
|---|---|---|
| Kali Linux | Attacker/Analysis | 192.168.247.129 |
| Metasploitable 2 | Victim/Test | 192.168.247.130 |

## Quick Pre-Checks

First, verify the network configuration of both virtual machines.

### On Kali Linux

```bash
ip a

### On Metasploitable 2

```bash
ifconfig

### Install Required Tools

Update the Kali Linux package list and install the required tools:

```bash
sudo apt update
sudo apt install nmap wireshark tcpdump tshark -y
```

### Start Wireshark

Launch Wireshark:

```bash
sudo wireshark
```

## Procedure

### 1. Verify Connectivity

Check whether Kali Linux can communicate with Metasploitable 2:

```bash
ping -c 3 192.168.247.130
```

A successful response confirms connectivity between the two machines.

### 2. Perform Quick Port/Service Scan

Use Nmap to identify open ports and services running on Metasploitable 2:

```bash
sudo nmap -sS -Pn 192.168.247.130
```

Example output:

```text
PORT     STATE  SERVICE
21/tcp   open   ftp
22/tcp   open   ssh
23/tcp   open   telnet
80/tcp   open   http
139/tcp  open   netbios-ssn
445/tcp  open   microsoft-ds
```

### 3. Start Wireshark Capture

Open Wireshark and select the network interface connected to the isolated lab network.

Common interfaces may include:

```text
eth0
ens33
```

Start the packet capture.

Use the following capture filter:

```text
host 192.168.247.130
```

This captures traffic involving the Metasploitable 2 machine.

### 4. Generate HTTP Traffic

While Wireshark is capturing packets, generate HTTP traffic from Kali Linux:

```bash
curl http://192.168.247.130/
```

### 5. Generate FTP Traffic

Connect to the FTP service running on the Metasploitable 2 test machine:

```bash
ftp 192.168.247.130
```

Use the authorized test credentials provided for the lab environment.

### 6. Generate Telnet Traffic

Connect to the Telnet service:

```bash
telnet 192.168.247.130
```

Use the authorized test credentials provided for the lab environment.

### 7. Analyze Captured Traffic

Use Wireshark display filters to identify specific network traffic.

#### Target Machine Traffic

```text
ip.addr == 192.168.247.130
```

#### FTP Requests

```text
ftp.request.command == "USER" || ftp.request.command == "PASS"
```

#### Telnet Traffic

```text
telnet
```

#### HTTP Traffic

```text
http
```

#### HTTP Authorization

```text
http.authorization
```

### 8. Follow TCP Stream

Select an FTP or Telnet packet in Wireshark.

Then select:

**Right-click → Follow → TCP Stream**

This displays the communication between the two endpoints as a complete stream.

In the isolated laboratory environment, this demonstrates how plaintext protocols can expose information during transmission.

### 9. Save the Packet Capture

Save the captured packets for documentation and further analysis.

Go to:

**File → Save As**

Save the file as:

```text
lab_capture.pcap
```

### 10. Export HTTP Objects

If HTTP objects are present in the capture, use:

**File → Export Objects → HTTP**

to examine relevant objects from the laboratory capture.

## Wireshark Display Filters

| Purpose | Filter |
|---|---|
| All traffic to/from target | `ip.addr == 192.168.247.130` |
| FTP USER/PASS requests | `ftp.request.command == "USER" || ftp.request.command == "PASS"` |
| Telnet traffic | `telnet` |
| HTTP traffic | `http` |
| HTTP Authorization | `http.authorization` |

## Screenshots

### 1. Network Configuration

Add a screenshot showing the IP addresses of Kali Linux and Metasploitable 2.

![Network Configuration](screenshots/network-configuration.png)

### 2. Connectivity Test

Add a screenshot showing the successful ping from Kali Linux to Metasploitable 2.

![Connectivity Test](screenshots/connectivity-test.png)

### 3. Nmap Scan

Add a screenshot showing the open ports and services discovered using Nmap.

![Nmap Scan](screenshots/nmap-scan.png)

### 4. Wireshark Packet Capture

Add a screenshot showing Wireshark capturing packets from the lab network.

![Wireshark Capture](screenshots/wireshark-capture.png)

### 5. Network Traffic Analysis

Add a screenshot showing the captured HTTP, FTP, or Telnet traffic.

![Network Traffic](screenshots/network-traffic.png)

### 6. Packet Analysis

Add a screenshot showing packet details or TCP Stream analysis.

![Packet Analysis](screenshots/packet-analysis.png)

## Result

Network traffic between Kali Linux and Metasploitable 2 was successfully captured and analyzed using Wireshark. Nmap was used to identify open ports and services, while HTTP, FTP, and Telnet traffic was generated and examined in the isolated laboratory environment.

The captured packets demonstrated how insecure protocols can transmit information without adequate encryption.

## Learning Outcomes

After completing this experiment, the following concepts were understood:

- Basic network packet capture
- Wireshark interface selection
- Network traffic analysis
- Nmap port and service scanning
- Wireshark capture and display filters
- TCP stream analysis
- HTTP traffic analysis
- FTP traffic analysis
- Telnet traffic analysis
- Security risks of plaintext protocols
- Importance of encrypted network communication

## Questions for Analysis

### 1. Why is packet capture useful in cybersecurity?

Packet capture allows security analysts to inspect network communication and identify unusual, suspicious, or potentially malicious traffic.

### 2. Why are FTP and Telnet considered insecure?

FTP and Telnet can transmit information without strong encryption, which may expose sensitive information to someone who can observe the network traffic.

### 3. What is the purpose of Wireshark filters?

Wireshark filters help analysts focus on specific packets or protocols instead of manually examining all captured traffic.

### 4. What is TCP Stream analysis?

TCP Stream analysis reconstructs the communication between two endpoints so that the exchanged data can be examined as a complete conversation.

### 5. What are secure alternatives to insecure protocols?

Examples include:

- SSH instead of Telnet
- SFTP instead of traditional FTP
- HTTPS instead of HTTP

## Ethical Consideration

This experiment was performed only in an isolated virtual laboratory using Metasploitable 2 as the intentionally vulnerable test machine.

Packet capture and network analysis should only be performed on systems and networks for which proper authorization has been obtained.

## Summary

In this experiment, an isolated cybersecurity laboratory was created using Kali Linux and Metasploitable 2. Nmap was used to identify open ports and running services, while Wireshark was used to capture and analyze network traffic.

HTTP, FTP, and Telnet traffic were generated and examined to understand how insecure protocols can expose information during transmission. The experiment demonstrated the importance of using secure protocols for protecting network communications.

## Conclusion

The experiment demonstrated the practical use of Wireshark for network traffic capture and analysis. By examining traffic between Kali Linux and Metasploitable 2, different protocols and communication patterns were identified.

The exercise provided practical knowledge of packet analysis and showed why encrypted protocols such as HTTPS, SSH, and SFTP should be preferred over insecure plaintext protocols.

## Disclaimer

This experiment was performed entirely within an isolated virtual laboratory environment for educational purposes. The techniques and tools described in this experiment should not be used against systems or networks without explicit authorization.
