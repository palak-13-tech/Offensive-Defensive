# Experiment 2: Simulated Ethical Hacking with Metasploit

## Objective

To perform a safe exploitation exercise on a virtual machine using Metasploit and understand the basic stages of ethical hacking.

## Environment

- Kali Linux (Attacker)
- Metasploitable 2 (Victim/Test)
- VirtualBox or VMware
- Host-Only Adapter or Internal Network

## Procedure

### 1. Configure Virtual Machines

Install Kali Linux and Metasploitable 2, configure both machines with a Host-Only Adapter or Internal Network, and boot them.

### 2. Verify Network Connectivity

Check the IP address of Metasploitable 2 and verify connectivity from Kali Linux.

```bash
ifconfig
ping <Metasploitable_IP>
