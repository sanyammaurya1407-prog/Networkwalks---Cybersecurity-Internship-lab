# Cybersecurity Virtual Lab — Week 1
### Networkwalks Internship | Kali Linux & VirtualBox

## 1. Introduction

This project documents the initial setup of a virtual environment for cybersecurity learning and security testing. The environment uses Kali Linux running inside Oracle VirtualBox, with a dedicated virtual network for connectivity and future lab expansion.

The goal is to establish a reusable testing environment for practising network security, reconnaissance, vulnerability assessment, and other authorized security activities.

## 2. Project Goals

The setup was designed to achieve the following:

- Prepare VirtualBox for running security-focused virtual machines.
- Deploy Kali Linux as the primary testing system.
- Establish a dedicated virtual network for lab machines.
- Configure and inspect the Kali network settings.
- Test basic connectivity and name resolution.
- Save a baseline snapshot for recovery.
- Maintain documentation for future lab exercises.

## 3. Environment Details

| Item | Configuration |
|---|---|
| Host System | Windows 11 |
| Processor | Intel Core i5 |
| Host Memory | 8 GB RAM |
| Virtualization Platform | Oracle VirtualBox 7.2 |
| Guest System | Kali Linux 2026.2 |
| VM Memory | 2 GB RAM |
| Network Mode | NAT Network |
| Network Name | NatNetwork |
| IPv4 Subnet | 10.0.0.0/24 |
| Planned Kali Address | 10.0.0.2/24 |
| Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |

*These values describe the intended configuration. Actual network settings should be confirmed inside the VM.*

## 4. Implementation

### 4.1 Preparing the Virtualization Platform

Installed the required archive extraction utility and Oracle VirtualBox. This provided the tools needed to import and manage the Kali Linux virtual machine.

### 4.2 Building the Virtual Network

Created a VirtualBox NAT Network named `NatNetwork` using the `10.0.0.0/24` IPv4 range. DHCP was enabled and IPv6 was disabled for this lab configuration.

This network design supports communication between virtual machines connected to the same NAT Network and allows outbound connectivity through network address translation.

### 4.3 Deploying Kali Linux

Imported the Kali Linux virtual machine and allocated 2048 MB of memory. Its first network adapter was attached to `NatNetwork` using the Intel PRO/1000 MT Desktop adapter type.

A shared folder was also configured to simplify file exchange between the Windows host and the virtual machine.

### 4.4 Configuring Network Parameters

Reviewed the guest operating system's network configuration and documented the intended IPv4 address, subnet mask, gateway, and DNS server.

The planned configuration was:

- IPv4 address: `10.0.0.2`
- Subnet mask: `255.255.255.0`
- Default gateway: `10.0.0.1`
- DNS server: `8.8.8.8`

A consistent address simplifies troubleshooting and makes the environment easier to reference during later exercises.

### 4.5 Establishing a Recovery Point

Created a VirtualBox snapshot named `Kali - Network Setup` after the initial configuration.

This snapshot provides a baseline that can be restored if later experiments affect the guest operating system or its network settings.

## 5. Validation Checklist

The following commands can be used to evaluate the lab configuration.

| Verification | Command | Purpose |
|---|---|---|
| Inspect interfaces | `ip a` | Check assigned addresses |
| Test gateway reachability | `ping 10.0.0.1` | Verify local gateway connectivity |
| Test outbound connectivity | `ping 8.8.8.8` | Check IP connectivity, where permitted |
| Check DNS | `nslookup networkwalks.com` | Test name resolution |
| Check Nmap installation | `nmap --version` | Confirm tool availability |
| Test snapshot recovery | Restore snapshot, then run `ip a` | Check baseline restoration |

The results should be recorded after running the commands. Expected outcomes should not be treated as verified results until the tests have been performed.

## 6. Troubleshooting Notes

### Network Connectivity Issues

Manual IPv4 configuration can interfere with connectivity if the address, gateway, DNS, or NetworkManager settings are incorrect.

Before changing connection settings, identify the active connection and inspect its current configuration. A command used during this setup was:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

The connection name may differ between systems. This setting should not be treated as a universal networking fix; verify the actual cause of the issue first.

### Hardware Virtualization

The virtual machine initially encountered a virtualization-related startup issue. The resolution was to enable Intel VT-x in the system's BIOS/UEFI settings, save the changes, and restart the computer before launching the VM again.

## 7. Key Takeaways

This setup provided practical experience with:

- Virtual machine creation and management.
- VirtualBox NAT Network configuration.
- IPv4 addressing, gateway settings, and DNS.
- Basic network troubleshooting.
- Snapshot-based recovery.
- Maintaining technical documentation for repeatable lab work.

The environment can be extended with additional virtual machines to support controlled network analysis and authorized security-testing exercises.

## 8. Responsible Testing

The lab is intended for educational use and authorized security assessments.

- Test only systems you own or have permission to assess.
- Keep deliberately vulnerable systems within a controlled lab environment.
- Take recovery snapshots before major changes.
- Avoid exposing testing services to untrusted networks.
- Document test results accurately.

## 9. Reference Links

- 7-Zip: https://7-zip.org/download.html
- Oracle VirtualBox: https://virtualbox.org/wiki/Downloads
- Kali Linux: https://kali.org/get-kali

## Author

**Sanyam Maurya**

Cybersecurity Intern | VAPT | Web, API & Android Security

LinkedIn: https://linkedin.com/in/sanyammaurya

---

*Cybersecurity internship learning project — initial virtual lab preparation and network configuration.*
