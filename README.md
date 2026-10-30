# Windows 10 Virtual Machine Setup & Network Connectivity Testing

## 📌 Project Overview

This project documents the installation and configuration of a Windows 10 virtual machine using Oracle VirtualBox.

The lab involved creating a Windows 10 virtual machine, allocating system resources, configuring its virtual network adapter, and establishing communication with an existing Kali Linux virtual machine.

Additional network connectivity tests were performed to verify internet access and communication between the two virtual machines. During testing, I encountered a connectivity issue caused by the Windows Defender Firewall blocking inbound ICMP traffic, which I resolved by creating a specific firewall rule.

## 🎯 Project Objectives

- Create and configure a Windows 10 virtual machine using VirtualBox.
- Install Windows 10 from an ISO image.
- Allocate appropriate hardware resources to the virtual machine.
- Configure the VM to use the same NAT Network as Kali Linux.
- Assign a static IP address to the Windows virtual machine.
- Test internet connectivity.
- Establish communication between Windows 10 and Kali Linux.
- Troubleshoot ICMP connectivity issues using Windows Firewall rules.

## 🛠️ Tools & Technologies

| Tool | Description |
|---|---|
| Ubuntu | Host operating system |
| Oracle VirtualBox | Virtualization platform |
| Windows 10 | Guest operating system |
| Kali Linux | Second virtual machine for network testing |
| NAT Network | Virtual networking |
| Windows Defender Firewall | Firewall configuration |
| ICMP / Ping | Network connectivity testing |

## 💻 Virtual Machine Configuration

The Windows 10 virtual machine was created with the following specifications:

| Component | Configuration |
|---|---|
| VM Name | Windows10-lab |
| Operating System | Microsoft Windows 10 (64-bit) |
| ISO Image | Windows 10 ISO |
| RAM | 4096 MB (4 GB) |
| Processors | 2 CPUs |
| Virtual Disk | 50 GB |
| Disk Format | VDI |
| Storage Allocation | Dynamically allocated |
| Video Memory | 128 MB |
| Network Adapter | NAT Network |

## ⚙️ Lab Implementation

### 1. Create the Windows 10 Virtual Machine

Opened Oracle VirtualBox and created a new virtual machine with the following configuration:

- **Name:** Windows10-lab
- **ISO Image:** Selected the Windows 10 ISO image.
- **Operating System Type:** Microsoft Windows.
- **Version:** Windows 10 (64-bit).
- Enabled **Skip Unattended Installation** to perform a manual Windows installation.

### 2. Allocate Hardware Resources

Configured the virtual machine resources as follows:

- RAM: 4096 MB.
- CPUs: 2.
- Virtual Hard Disk: 50 GB.
- Disk Type: VDI.
- Storage: Dynamically allocated.

### 3. Configure VirtualBox Settings

Before starting the virtual machine, I adjusted the following settings:

**System Settings**
- Set the boot order to prioritize Optical Drive.

**Display Settings**
- Video Memory: 128 MB.

**Network Settings**
- Attached the network adapter to the existing NAT Network.
- Used the same NAT Network as the Kali Linux virtual machine to enable communication between both systems.

### 4. Install Windows 10

Started the virtual machine and booted from the mounted Windows 10 ISO image.

Followed the Windows installation wizard to complete the operating system installation and initial configuration.

After installation, the virtual machine was ready for network configuration and connectivity testing.

### 5. Configure Windows Static IP Address

Configured a static IP address on the Windows 10 virtual machine to enable consistent communication with Kali Linux.

The network was configured within the same subnet as the Kali Linux virtual machine.

Example network configuration:

| Device | IP Address |
|---|---|
| Kali Linux | 10.0.0.2 |
| Windows 10 | 10.0.0.10 |
| Subnet | 255.255.255.0 |
| Network | 10.0.0.0/24 |

*Note: The Windows IP above represents the example configuration used for the lab. Replace it if your actual assigned address differs.*

### 6. Test Internet Connectivity

After configuring the Windows network settings, I opened Command Prompt and tested connectivity to Google's public DNS IP address.

Executed:

```cmd
ping 8.8.8.8
```

This test was used to verify external IP connectivity from the Windows virtual machine.

### 7. Test Connectivity Between Windows 10 and Kali Linux

The next step involved testing communication between both virtual machines.

**Test 1: Windows 10 to Kali Linux**

From Windows Command Prompt, executed:

```cmd
ping 10.0.0.2
```

This test checked whether Windows could communicate with the Kali Linux virtual machine.

**Test 2: Kali Linux to Windows 10**

From the Kali Linux terminal, executed:

```bash
ping 10.0.0.10
```

Initially, Kali Linux could not successfully ping the Windows virtual machine because Windows Defender Firewall was blocking inbound ICMP echo requests.

### 8. Troubleshoot Windows Firewall Blocking ICMP

To resolve the connectivity issue, I created a Windows Defender Firewall rule allowing inbound IPv4 ICMP echo requests.

Opened Command Prompt as Administrator and executed:

```cmd
netsh advfirewall firewall add rule name="ICMPv4" protocol=icmpv4:8,any dir=in action=allow
```

**Command breakdown:**

- `netsh advfirewall`: Accesses Windows Advanced Firewall configuration.
- `add rule`: Creates a new firewall rule.
- `name="ICMPv4"`: Assigns a name to the rule.
- `protocol=icmpv4:8,any`: Specifies IPv4 ICMP Echo Requests.
- `dir=in`: Applies the rule to inbound traffic.
- `action=allow`: Allows matching traffic.

After creating the rule, I repeated the ping test from Kali Linux to Windows 10.

This resolved the inbound ICMP connectivity issue.

## 📸 Screenshots & Lab Evidence

The following screenshots document the network connectivity tests performed during the lab.

### 1. Windows 10 Internet Connectivity Test

Testing external IP connectivity by pinging Google's public DNS address.

![Windows 10 Ping 8.8.8.8](https://github.com/Fybanet/NETWORKWALKS--Fybanet-B084-WK1-PMx-Windows10-Virtualbox-Setup/blob/main/Windows%208.8.8.8%20ping.png)

### 2. Windows 10 to Kali Linux Connectivity

Testing communication from the Windows 10 virtual machine to the Kali Linux virtual machine.

![Windows to Kali Ping](https://github.com/Fybanet/NETWORKWALKS--Fybanet-B084-WK1-PMx-Windows10-Virtualbox-Setup/blob/main/Windows%20kali%20ping.png)

### 3. Kali Linux to Windows 10 Connectivity

Testing communication from Kali Linux to the Windows 10 virtual machine after configuring the inbound ICMP firewall rule.

![Kali to Windows Ping](https://github.com/Fybanet/NETWORKWALKS--Fybanet-B084-WK1-PMx-Windows10-Virtualbox-Setup/blob/main/Kali%20windows%20ping.png)

## 📊 Results & Observations

The lab provided practical experience with Windows virtualization and communication between different operating systems.

The following tasks were completed:

- Successfully created and installed a Windows 10 virtual machine.
- Allocated and configured virtual hardware resources.
- Connected Windows 10 to the same NAT Network as Kali Linux.
- Configured static IP addressing.
- Tested external network connectivity using ICMP.
- Identified a Windows Defender Firewall restriction affecting inbound ping requests.
- Created a firewall rule to permit inbound IPv4 ICMP Echo Requests.
- Established bidirectional communication between Windows 10 and Kali Linux.

## 📚 Skills Acquired

- Windows 10 installation and configuration.
- Virtual machine deployment using Oracle VirtualBox.
- Virtual networking and NAT Network configuration.
- Static IP addressing and subnet configuration.
- Windows Defender Firewall management.
- Windows command-line administration.
- Linux-to-Windows network connectivity testing.
- ICMP troubleshooting and network diagnostics.



This repository documents my practical learning journey in virtualization, Windows administration, networking, and cybersecurity lab environments.

---

*Hands-on learning. Practical experience. Continuous improvement.*
