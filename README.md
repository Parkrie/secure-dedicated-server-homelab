# secure-dedicated-server-homelab
Deploying and troubleshooting a self-hosted dedicated server in a segmented homelab using Proxmox, VLANs, firewall rules, and secure port forwarding.
# Secure Dedicated Game Server Deployment in a Segmented Homelab

## Overview

This project documents the deployment and troubleshooting of a self-hosted dedicated game server inside a virtualized homelab environment.

The objective was to allow external players to connect to a locally hosted server while maintaining strong networking and cybersecurity practices.

The environment was intentionally segmented to minimize risk when exposing services to the internet.

Key objectives included:

- Deploying a dedicated server inside a Proxmox virtual machine
- Using VLAN-based network segmentation
- Configuring secure port forwarding
- Troubleshooting connectivity issues across network boundaries
- Applying least-privilege firewall rules

---

## Technologies Used

- Proxmox VE
- Ubuntu Linux
- Virtual Machines
- VLAN Network Segmentation
- Windows Firewall (client-side troubleshooting)
- Router Port Forwarding (NAT)
- Dedicated Game Server Software
- Network Troubleshooting Tools

---

## Environment Design

The dedicated server was deployed inside a segmented homelab network.

Example logical architecture:

Internet  
↓  
Router / Firewall  
↓  
Server VLAN  
↓  
Proxmox Host  
↓  
Ubuntu VM  
↓  
Dedicated Game Server  

The purpose of segmentation was to isolate the externally exposed service from the primary LAN.

This design prevents an internet-facing service from having direct access to internal systems.

## Logical Architecture

The following diagram shows the simplified logical architecture used in the deployment.

![Network Architecture](images/network-diagram.png)

---

## VM Deployment

The server was deployed inside an **Ubuntu virtual machine running on Proxmox**.

Deployment steps included:

- Creating the VM inside Proxmox
- Assigning CPU, memory, and storage resources
- Connecting the VM to a segmented VLAN
- Installing and configuring the dedicated server software on Ubuntu

Using a VM provides several operational advantages:

- Isolation from the host system
- Snapshot capability for rollback
- Easier rebuild and maintenance
- Ability to quickly redeploy if compromised

---

## Initial Connectivity Testing

After deployment, connectivity tests were performed between systems.

Testing included:

- PC → VM ping tests
- VM → PC ping tests
- Server port checks

Initial results showed:

- The PC could ping the VM
- The VM could not ping the PC

This indicated that network routing and VLAN configuration were functioning, but something was preventing responses from the client machine.

---

## Firewall Troubleshooting

Further investigation revealed that the issue was caused by **Windows Firewall rules on the client system** blocking inbound traffic.

The Windows machine was not allowing ICMP echo responses by default.

After enabling the appropriate inbound rule for ICMP echo requests, bidirectional connectivity was established between the client and the VM.

This step allowed further troubleshooting of the game server connection.

Security considerations included:

- Enabling only the necessary inbound rule
- Restricting rules to the private network profile
- Avoiding overly permissive firewall configurations

---

## Router Port Forwarding

To allow external players to join the server, a port forward was configured on the router.

Example traffic flow:

Internet  
↓  
Router Port Forward  
↓  
Server VLAN  
↓  
Ubuntu Game Server VM

Security precautions included:

- Forwarding only the required service port
- Avoiding exposure of unnecessary services
- Keeping internal addressing private

---

## Security Observations

After exposing the service externally, intrusion detection alerts began appearing from external IP addresses attempting to connect to the forwarded port.

This behavior is normal when exposing services to the public internet.

Automated scanners routinely probe open ports looking for vulnerable services.

This reinforces the importance of:

- Minimizing exposed services
- Applying strict firewall rules
- Monitoring IDS/IPS alerts
- Segmenting externally exposed systems

---

## Troubleshooting Methodology

Connectivity issues were resolved by systematically isolating each layer of the network stack.

The process involved validating:

1. VM networking configuration
2. VLAN routing
3. Client firewall behavior
4. Router NAT and port forwarding

Breaking the problem down by network layer made it possible to identify the root cause efficiently.

---

## Lessons Learned

Key lessons from this project include:

- The importance of network segmentation
- Applying least-privilege firewall configurations
- Understanding NAT and port forwarding
- Monitoring exposed services for scanning activity
- Using structured troubleshooting processes

---

## Future Improvements

Potential improvements to this environment include:

- Reverse proxy or gateway access control
- VPN-based remote access instead of open port forwarding
- Centralized logging and monitoring
- Containerized server deployments

---

## Why This Project Matters

This project demonstrates hands-on experience with:

- Virtualization
- Linux server administration
- Network segmentation
- Firewall configuration
- Secure service exposure
- Network troubleshooting
- Cybersecurity awareness

These skills directly translate to roles in systems administration, networking, and cybersecurity.
