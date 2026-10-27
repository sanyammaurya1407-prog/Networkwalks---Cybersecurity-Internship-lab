# NETWORKWALKS-WK1-CYBERSECURITY-LAB-SETUP

An isolated virtual cybersecurity lab built using VirtualBox and Kali Linux for cybersecurity learning, network analysis, and authorized penetration-testing practice.

**Technologies:** Kali Linux · VirtualBox · Linux · Virtual Networking · Nmap

---

## Project Overview

This project focuses on setting up a virtual cybersecurity laboratory using Oracle VirtualBox and Kali Linux.

The purpose of this lab is to create a controlled environment where cybersecurity tools, network reconnaissance, port scanning, vulnerability assessment, packet analysis, and other security-testing activities can be practised safely.

The lab uses a dedicated VirtualBox NAT Network, allowing additional virtual machines to be connected for authorized security testing and future cybersecurity exercises.

## Objectives

The main objectives of this project are to:

- Install and configure Oracle VirtualBox.
- Import and configure Kali Linux as a virtual machine.
- Create a dedicated NAT Network for the cybersecurity lab.
- Configure Kali Linux network connectivity.
- Assign a consistent IPv4 address to the Kali VM.
- Verify gateway connectivity and DNS resolution.
- Create a clean VirtualBox snapshot for recovery.
- Document the setup process and troubleshooting steps.
- Prepare the environment for future cybersecurity projects.

## Purpose of the Lab

The laboratory provides a controlled environment for cybersecurity learning and authorized security testing.

It can be used for:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web application security testing
- Penetration-testing practice
- Security-tool experimentation
- Multi-VM cybersecurity exercises

**Important:** Use this laboratory only on systems you own or have explicit permission to test. Keep vulnerable target machines isolated from untrusted networks.

---

## Lab Configuration

| Component | Configuration |
|---|---|
| Host Operating System | Windows 11 |
| Host RAM | 8 GB |
| Processor | Intel Core i5 |
| Hypervisor | Oracle VirtualBox 7.2 |
| Security Operating System | Kali Linux 2026.2 |
| Kali VM RAM | 2048 MB |
| Virtual Network | NAT Network |
| Network Name | NatNetwork |
| Network Address | 10.0.0.0/24 |
| Kali IP Address | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |

*Note: These are the documented lab settings. Actual connectivity depends on the VirtualBox network and Kali Linux configuration.*

---

## Lab Setup Procedure

### Step 1: Install 7-Zip

Installed 7-Zip to extract the downloaded Kali Linux virtual-machine package when distributed as a `.7z` archive.

**Tool:** 7-Zip

### Step 2: Install VirtualBox

Installed Oracle VirtualBox to create and manage virtual machines for cybersecurity practice.

### Step 3: Create a NAT Network

Created a dedicated NAT Network in VirtualBox with the following configuration:

- **Network Name:** NatNetwork
- **IPv4 Prefix:** 10.0.0.0/24
- **DHCP:** Enabled
- **IPv6:** Disabled

A NAT Network allows multiple connected virtual machines to communicate with one another while providing outbound network connectivity.

**Screenshot:** `Screenshot-2026-10-26-112620.png`

### Step 4: Import Kali Linux

Downloaded Kali Linux from the official Kali Linux website and imported the virtual machine into VirtualBox.

Configured the VM network adapter:

- **Adapter:** Adapter 1
- **Attached To:** NAT Network
- **Network:** NatNetwork
- **Adapter Type:** Intel PRO/1000 MT Desktop
- **Allocated RAM:** 2048 MB

A shared folder was also configured to transfer required files between the Windows host and Kali Linux.

**Screenshot:** `Screenshot_2026-10-26_06_03_45.png`

### Step 5: Configure Kali Linux Networking

Checked and configured the IPv4 network settings for the Kali Linux VM.

| Setting | Value |
|---|---|
| IP Address | 10.0.0.2 |
| Subnet Mask | 255.255.255.0 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |

A consistent IP address makes it easier to document the lab and reference the Kali VM during future exercises.

**Screenshot:** `Screenshot_2026-10-26_06_46_37.png`

### Step 6: Create a Clean VM Snapshot

Created a VirtualBox snapshot after completing the initial network configuration.

**Snapshot Name:** `Kali - Network Setup`

The snapshot provides a known-good recovery point. It can be restored if a future experiment changes or damages the VM configuration.

---

## Lab Verification

The following checks can be used to verify the setup.

| Test | Command | Expected Result |
|---|---|---|
| Check IP address | `ip a` | Correct Kali IP displayed |
| Check gateway | `ping 10.0.0.1` | Successful replies |
| Check Internet connectivity | `ping 8.8.8.8` | Successful replies, if outbound access is available |
| Check DNS resolution | `nslookup networkwalks.com` | Domain resolves |
| Verify Nmap | `nmap --version` | Nmap version displayed |
| Verify snapshot | Restore snapshot and run `ip a` | Baseline configuration restored |

### Example Network Settings

```text
IP Address: 10.0.0.2/24
Gateway:    10.0.0.1
DNS:        8.8.8.8
```

*Record actual command outputs and screenshots when performing these checks; expected results are not a substitute for verification evidence.*

---

## Problems Encountered and Solutions

### Problem 1: Internet Connectivity After Static IP Configuration

After manually configuring IPv4 settings, Internet connectivity may fail depending on the Kali Linux and NetworkManager configuration.

One workaround documented during this lab was:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

The network connection was then restarted or the system rebooted, and connectivity was tested again.

**Important:** Connection names may differ. Identify the actual connection name before modifying its settings.

### Problem 2: VirtualBox VT-x / Virtualization Error

The virtual machine initially failed to start because hardware virtualization was disabled in the system firmware.

The issue was resolved by:

1. Restarting the computer.
2. Entering the BIOS/UEFI settings.
3. Enabling Intel VT-x or hardware virtualization.
4. Saving the configuration.
5. Restarting the computer.
6. Starting the Kali Linux VM again.

After enabling virtualization, the VM started successfully.

---

## What I Learned

Through this project, I gained practical experience with the following concepts.

### 1. NAT vs. NAT Network

A standard VirtualBox NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple connected virtual machines to communicate with one another while providing network address translation for outbound connectivity. This makes it useful for a multi-machine cybersecurity lab.

### 2. Virtual Machine Networking

Learned how virtual network adapters connect virtual machines to different network types and how network settings affect connectivity between virtual machines and external networks.

### 3. Static IP Configuration

Learned how to configure and verify IPv4 addresses, subnet masks, gateways, and DNS settings in Kali Linux.

### 4. Virtual Machine Snapshots

Learned the importance of creating a clean snapshot before performing experimental or potentially disruptive activities.

### 5. Technical Documentation

Learned how to document setup procedures, commands, configuration details, screenshots, troubleshooting steps, and verification results in a structured format.

---

## Security and Ethical Use

This laboratory is intended for educational purposes and authorized security testing.

- Test only systems you own or have explicit permission to assess.
- Keep vulnerable target machines separated from untrusted networks.
- Take snapshots before risky experiments.
- Avoid exposing lab services publicly.
- Document findings and testing activities responsibly.

---

## Tools and Resources

- **7-Zip:** https://7-zip.org/download.html
- **Oracle VirtualBox:** https://virtualbox.org/wiki/Downloads
- **Kali Linux:** https://kali.org/get-kali

## Author

**Sanyam Maurya**

Cybersecurity Intern | VAPT | Web, API & Android Security

- **LinkedIn:** https://linkedin.com/in/sanyammaurya
- **GitHub:** Add your GitHub profile URL here.

---

*Part of my cybersecurity internship learning journey at Networkwalks. This project documents the initial virtual lab setup and prepares the environment for future authorized security-testing exercises.*
