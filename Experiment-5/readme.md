# ARP Spoofing and Man-in-the-Middle (MITM) Attack Analysis

## Overview

This experiment demonstrates ARP spoofing and Man-in-the-Middle (MITM) concepts in a controlled virtual lab environment. Kali Linux is used to perform ARP spoofing, while Wireshark is used to capture and analyze network traffic exchanged between the target system and the gateway.

The experiment also uses Damn Vulnerable Web Application (DVWA) to observe HTTP requests and understand the security risks associated with transmitting data over unencrypted HTTP connections.

## Objectives

- Understand the working of the Address Resolution Protocol (ARP).
- Study ARP spoofing and its role in MITM attacks.
- Configure IPv4 packet forwarding in Kali Linux.
- Generate and analyze ICMP and HTTP traffic.
- Capture network packets using Wireshark.
- Understand how unencrypted HTTP traffic can expose sensitive information.
- Identify preventive measures against ARP spoofing.

## Lab Environment

| Component | Description |
|---|---|
| Attacker system | Kali Linux |
| Target web application | DVWA |
| Target/server environment | Metasploitable |
| Packet analyzer | Wireshark |
| ARP spoofing tool | arpspoof |
| Traffic testing tool | ping and curl |
| Network interface | eth0 / eth1, depending on the VM configuration |
| Network | Isolated virtual lab network |

## Network Configuration

The screenshots show the following IP addresses:

| System | IP Address |
|---|---|
| Gateway | `192.168.1.1` |
| DVWA web server | `192.168.1.100` |
| Kali Linux interface | `192.168.1.10` |
| Kali Linux second interface | `192.168.159.14` |
| Additional observed host | `192.168.1.101` |

**Note:** The addresses above are taken from the lab screenshots. Confirm the actual gateway, target, and interface addresses in your own VM configuration before repeating the experiment.

## Tools and Technologies

- Kali Linux
- Metasploitable
- Damn Vulnerable Web Application (DVWA)
- Wireshark
- arpspoof
- ICMP
- ARP
- HTTP
- TCP/IP networking

## Procedure

### Step 1: Access DVWA

Open the DVWA web application in the browser using the target server's IP address:

`http://192.168.1.100/dvwa/`

The DVWA home page confirms that the vulnerable web application is accessible from the lab system.

### Step 2: Verify Network Connectivity

Check connectivity between the Kali Linux system, target server, and gateway.

```bash
ping -c 4 192.168.1.100
ping -c 4 192.168.1.1
```

The screenshots show successful ping responses with zero packet loss for these connectivity tests.

### Step 3: Enable IPv4 Packet Forwarding

IPv4 forwarding allows a Linux system to route packets between network interfaces.

Enable it temporarily with:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

Alternatively, use:

```bash
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```

Verify the setting:

```bash
cat /proc/sys/net/ipv4/ip_forward
```

A value of `1` indicates that IPv4 forwarding is enabled.

### Step 4: Observe ARP Spoofing

In the authorized virtual lab, `arpspoof` was used to send forged ARP replies involving the target and gateway.

Example command shown in the experiment:

```bash
sudo arpspoof -i eth0 -t 192.168.1.100 192.168.1.1
```

The command generates forged ARP replies associating the gateway's IP address with the attacker's MAC address.

The reverse direction was also tested:

```bash
sudo arpspoof -i eth0 -t 192.168.1.1 192.168.1.100
```

These commands should only be tested on systems and networks for which explicit authorization has been obtained.

### Step 5: Capture Traffic Using Wireshark

Start Wireshark on the appropriate lab network interface and begin packet capture.

Use the following display filter to inspect packets involving the DVWA server and HTTP traffic:

```text
ip.addr == 192.168.1.100 && http
```

To focus on packets involving the server regardless of protocol, use:

```text
ip.addr == 192.168.1.100
```

To inspect ARP traffic, use:

```text
arp
```

To inspect ICMP traffic, use:

```text
icmp
```

The captured traffic includes HTTP requests, server responses, ICMP messages, and ARP-related network activity.

### Step 6: Analyze HTTP Requests

The Wireshark capture shows a request similar to:

```text
POST /dvwa/login.php HTTP/1.1
```

The packet details identify HTTP form data encoded as:

```text
application/x-www-form-urlencoded
```

The response sequence includes HTTP status codes such as `302 Found` and `200 OK`.

This demonstrates how HTTP requests and responses can be inspected when traffic is unencrypted. Actual form fields and sensitive values should only be examined within the authorized lab.

### Step 7: Observe Network Behavior

During testing, Wireshark displayed ICMP echo requests, echo replies, TCP SYN packets, retransmissions, and ICMP redirect messages.

These observations help illustrate network communication and the effects that incorrect routing, interface configuration, or ARP manipulation can have on traffic.

## Observations

1. The DVWA application was accessible through the browser over HTTP.
2. ICMP connectivity tests to the gateway and target server completed successfully.
3. IPv4 forwarding was enabled on the Kali Linux system.
4. The `arpspoof` tool generated repeated forged ARP replies.
5. Wireshark captured HTTP requests and responses involving the DVWA server.
6. The capture included a POST request to the DVWA login endpoint.
7. ICMP redirect messages, TCP SYN packets, and retransmissions were also observed.
8. The experiment demonstrated why ARP trust and unencrypted HTTP communication can introduce security risks.

**Important:** Packet capture and forged ARP replies alone do not prove that all traffic successfully passed through the attacker. A complete MITM demonstration would require additional verification of packet forwarding and traffic flow.

## Security Risks

- **ARP spoofing:** Can redirect local network traffic to an unauthorized system.
- **Man-in-the-Middle attacks:** May allow an attacker to observe or manipulate traffic when other protections are absent.
- **Unencrypted HTTP:** Does not provide transport encryption and may expose transmitted data.
- **Traffic manipulation:** Improper routing or forwarding may disrupt normal network communication.

## Preventive Measures

- Use HTTPS with valid TLS certificates instead of unencrypted HTTP.
- Enable Dynamic ARP Inspection (DAI) on supported managed switches.
- Use DHCP snooping and appropriate network access controls.
- Apply static ARP entries only where operationally appropriate.
- Monitor unusual ARP changes and unexpected ICMP redirect messages.
- Isolate vulnerable applications such as DVWA from production networks.
- Keep operating systems, network equipment, and applications updated.

## Result

The experiment demonstrated the basic operation of ARP spoofing in a virtual lab and the use of Wireshark to analyze ICMP, TCP, ARP-related activity, and HTTP requests. It also highlighted the security weaknesses of unencrypted HTTP communication and the importance of network monitoring and defensive controls.

## Ethical Considerations

This experiment is intended strictly for educational purposes in an isolated virtual lab. ARP spoofing and traffic interception must only be performed on systems and networks for which explicit authorization has been granted.

