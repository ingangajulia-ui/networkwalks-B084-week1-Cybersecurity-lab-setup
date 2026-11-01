# NetworkWalks B084 – Week 1: Cybersecurity Lab Setup

A hands-on cybersecurity lab project focused on setting up and configuring a Kali Linux virtual machine using Oracle VirtualBox.

## Project Overview

This project involved building a functional cybersecurity lab environment using Kali Linux as the guest operating system and Windows as the host.

The setup included configuring virtual networking, assigning a static IP address, establishing internet connectivity, verifying DNS resolution, and enabling file sharing and integration between the host and guest systems.

## Project Objectives

- Set up a Kali Linux virtual machine using Oracle VirtualBox.
- Configure a VirtualBox NAT Network.
- Assign Kali Linux a static IPv4 address.
- Configure the default gateway and DNS servers.
- Test network and internet connectivity.
- Verify DNS resolution.
- Enable bidirectional clipboard sharing.
- Enable drag-and-drop functionality.
- Configure a shared folder between Windows and Kali Linux.

## Lab Environment

| Component | Configuration |
|---|---|
| Host Operating System | Windows |
| Virtualization Software | Oracle VirtualBox 7.2.10 |
| Guest Operating System | Kali Linux |
| NAT Network | CyberLab |
| Network Type | NAT Network |
| Subnet | 10.0.0.0/24 |
| Kali Linux IP Address | 10.0.0.2 |
| Default Gateway | 10.0.0.1 |
| Primary DNS | 1.1.1.1 |
| Secondary DNS | 8.8.8.8 |
| DHCP | Disabled |

## Network Architecture

```text
             Internet
                 |
          VirtualBox NAT
                 |
          CyberLab Network
             10.0.0.0/24
                 |
          Gateway: 10.0.0.1
                 |
          Kali Linux VM
             10.0.0.2
                 |
          Windows Host
```

## Network Configuration

A NAT Network named `CyberLab` was created in Oracle VirtualBox with DHCP disabled.

Kali Linux was configured with a static IPv4 address using NetworkManager.

The following commands were used:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.addresses 10.0.0.2/24
sudo nmcli connection modify "Wired connection 1" ipv4.gateway 10.0.0.1
sudo nmcli connection modify "Wired connection 1" ipv4.dns "1.1.1.1 8.8.8.8"
sudo nmcli connection modify "Wired connection 1" ipv4.method manual
sudo nmcli connection up "Wired connection 1"
```

## Verification Commands

The following commands were used to verify the network configuration and connectivity.

**Check the network interface:**

```bash
ip addr show eth0
```

**Check the routing table:**

```bash
ip route
```

**Test gateway connectivity:**

```bash
ping -c 4 10.0.0.1
```

**Test internet connectivity:**

```bash
ping -c 4 1.1.1.1
```

**Test DNS resolution:**

```bash
ping -c 4 google.com
```

**Verify shared folder mounting:**

```bash
mount | grep vboxsf
```

## Test Results

| Test | Result |
|---|---|
| Static IP configuration | Successful |
| Gateway connectivity | 0% packet loss |
| Internet connectivity to 1.1.1.1 | 25% packet loss |
| DNS resolution | Successful |
| Shared folder mounting | Successful |
| Bidirectional clipboard | Successful |
| Windows-to-Kali drag-and-drop | Successful |

## Shared Folder Configuration

The Windows Downloads folder was configured as a VirtualBox shared folder and mounted in Kali Linux at:

```text
/media/sf_Downloads
```

The VirtualBox shared filesystem driver (`vboxsf`) was verified.

## VirtualBox Integration

VirtualBox Guest Additions drivers were present and loaded.

The following integration features were enabled and tested:

- Bidirectional clipboard sharing.
- Drag-and-drop from Windows to Kali Linux.

## Skills Demonstrated

- Kali Linux fundamentals
- Linux command-line administration
- Oracle VirtualBox configuration
- IPv4 addressing and subnetting
- NAT networking
- Static IP configuration
- DNS resolution and troubleshooting
- Network connectivity testing
- Virtual machine integration and file sharing

## Learning Outcomes

This project strengthened my practical understanding of Linux networking, virtualization, IP addressing, and network troubleshooting.

It also provided hands-on experience configuring and validating communication between a host operating system and a virtual machine.

## Security Note

This lab was configured for educational purposes. Any future security testing will be conducted only against systems for which authorization has been granted.
