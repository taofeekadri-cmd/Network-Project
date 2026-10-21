# Network Communication and Interdepartmental Connectivity Project

This project demonstrates the design and configuration of a multi-department network using **Cisco Packet Tracer**. It focuses on connecting the IT, Marketing, and HR departments through a central router, configuring IP addressing and DHCP services, and exploring network access control using Access Control Lists (ACLs).

## Table of Contents

- [Project Overview](#project-overview)
- [Network Topology](#network-topology)
- [Tools and Technologies](#tools-and-technologies)
- [Configuration Steps](#configuration-steps)
- [Results and Findings](#results-and-findings)
- [Author](#author)

## Project Overview

The purpose of this project is to design and simulate a network that supports communication between three organisational departments: **IT, Marketing, and HR**.

The project aims to:

- Design a network topology connecting multiple departmental LANs through a central router.
- Configure IP addressing and default gateways for separate network subnets.
- Set up a server to provide Dynamic Host Configuration Protocol (DHCP) and Domain Name System (DNS) services.
- Assign IP addresses automatically to client devices.
- Explore router configuration and Access Control Lists (ACLs) for controlling network traffic.
- Identify configuration errors and understand the importance of validating network commands.

## Network Topology

The network was designed in Cisco Packet Tracer using a **central router connected to three departmental switches**, with end devices connected to each switch.

### Network Components

- **Central router:** Connects the three departmental networks and provides the configured gateway addresses.
- **IT Department:** Contains two PCs and a server.
- **Marketing Department:** Contains two PCs connected to a departmental switch.
- **HR Department:** Contains two PCs connected to a departmental switch.
- **Server:** Configured with a static IP address and intended to provide DHCP and DNS services.
- **Switches:** Provide connectivity between departmental end devices and the router.

### IP Addressing Scheme

The topology uses three separate IPv4 subnets.

| Department | Network Address   | Default Gateway | Example Client IP |
| ---------- | ----------------- | --------------- | ----------------- |
| IT         | `192.168.10.0/24` | `192.168.10.1`  | `192.168.10.11`   |
| Marketing  | `192.168.20.0/24` | `192.168.20.1`  | `192.168.20.10`   |
| HR         | `192.168.30.0/24` | `192.168.30.1`  | `192.168.30.10`   |

**Subnet mask:** `255.255.255.0`

### Server Configuration

The server configuration shown in the project includes:

- **Server IP address:** `192.168.10.2`
- **Subnet mask:** `255.255.255.0`
- **Default gateway:** `192.168.10.1`
- **DNS server address:** `192.168.10.3`
- **DHCP pool name:** `serverPool`
- **DHCP starting IP address:** `192.168.10.10`
- **Maximum DHCP users:** `246`

The documented DHCP pool uses the IT subnet. Although the server configuration includes a DNS address, the document does not show a complete DNS service configuration or confirm successful name resolution.

## Tools and Technologies

- **Cisco Packet Tracer** – Network design, simulation, and device configuration.
- **Cisco router** – Routing between departmental networks.
- **Cisco switches** – Local network connectivity.
- **Server-PT** – DHCP and DNS service configuration.
- **PC-PT** – Client devices for network configuration and testing.
- **IPv4 addressing and subnetting** – Logical network segmentation.
- **DHCP** – Automatic IP address assignment to clients.
- **DNS** – Domain name resolution configuration.
- **Cisco IOS CLI** – Router configuration and ACL command practice.
- **Access Control Lists (ACLs)** – Exploration of IP traffic filtering.

## Configuration Steps

1. **Design the network topology.**

   - Open Cisco Packet Tracer.
   - Add a central router, three departmental switches, a server, and six PCs.
   - Arrange the devices into IT, Marketing, and HR departmental networks.
   - Connect the router to each departmental switch and connect the end devices to their respective switches.

2. **Define the IP addressing scheme.**

   - Allocate `192.168.10.0/24` to the IT department.
   - Allocate `192.168.20.0/24` to the Marketing department.
   - Allocate `192.168.30.0/24` to the HR department.
   - Use the first address shown in each subnet as its default gateway.

3. **Configure the central router.**

   - Access the router CLI.

   - Enter privileged EXEC mode:

     ```text
     enable
     ```

   - Enter global configuration mode:

     ```text
     configure terminal
     ```

   - Configure the router interfaces with the appropriate gateway addresses for the three subnets, ensuring that the interface names match the actual router model.

   - Enable the interfaces and verify their operational status.

4. **Configure the server.**

   - Open the server's configuration window.
   - Assign the static IP address `192.168.10.2`.
   - Set the subnet mask to `255.255.255.0`.
   - Set the default gateway to `192.168.10.1`.
   - Configure the DNS server address as `192.168.10.3`, as recorded in the project.

5. **Configure the DHCP service.**

   - Open the server's **Services > DHCP** section.
   - Create a DHCP pool named `serverPool`.
   - Set the default gateway to `192.168.10.1`.
   - Enter `192.168.10.3` as the DNS server.
   - Set the starting IP address to `192.168.10.10`.
   - Set the subnet mask to `255.255.255.0`.
   - Set the maximum number of users to `246`.
   - Save the configuration.

6. **Configure client devices.**

   - Open each PC's IP configuration settings.
   - Select DHCP where automatic addressing is required.
   - Verify the assigned IP address, subnet mask, default gateway, and DNS server.
   - For clients in the Marketing and HR subnets, ensure the DHCP configuration supports their respective networks before expecting successful automatic addressing.

7. **Explore Access Control Lists.**

   - Access the router CLI and enter global configuration mode.
   - Attempt to create an extended ACL to filter traffic between network subnets.
   - Review the syntax errors recorded in the project and correct the command structure before applying the ACL.

   The following is an example of valid Cisco IOS syntax for denying traffic from the Marketing subnet to the IT subnet:

   ```text
   access-list 100 deny ip 192.168.20.0 0.0.0.255 192.168.10.0 0.0.0.255
   ```

   An appropriate permit rule and application of the ACL to the correct interface and direction would also be required to implement the intended traffic policy. This example is a corrected configuration example, not a confirmed successful configuration from the submitted project.

8. **Test and troubleshoot the network.**

   - Check router interface status and IP addressing.
   - Confirm that clients receive valid DHCP leases.
   - Use `ping` to test connectivity between devices and their default gateways.
   - Test communication between subnets where routing is configured.
   - Review CLI error messages and verify ACL syntax before testing traffic restrictions.

## Results and Findings

The project demonstrates the design of a segmented network for three organisational departments and documents several device configuration activities.

### Results Achieved or Documented

- **Network segmentation:** Three departmental IPv4 subnets were represented in the topology.
- **Centralised connectivity:** The router was positioned to connect the IT, Marketing, and HR networks.
- **Server addressing:** The server was configured with the static address `192.168.10.2`.
- **DHCP configuration:** A DHCP pool named `serverPool` was created for the IT subnet.
- **Client addressing:** The screenshots show DHCP configuration on client devices, with successful DHCP request messages displayed for some clients.
- **Router command practice:** ACL configuration was attempted, providing an opportunity to identify and troubleshoot Cisco IOS syntax errors.

### Findings and Lessons Learned

- **DHCP scope design matters:** Each subnet needs an appropriate DHCP scope and default gateway if clients in all three departments are to obtain addresses automatically from the server.
- **Inter-subnet communication requires routing:** Router interfaces and gateway settings must be configured correctly for devices in different subnets to communicate.
- **ACL syntax must be accurate:** The submitted CLI screenshot shows invalid-input errors during ACL configuration. The intended access-control policy therefore requires correction and verification.
- **Configuration must be validated:** A configured IP address or DHCP pool alone does not prove end-to-end connectivity. Testing with `ping`, checking interface status, and reviewing client settings are essential.
- **DNS requires separate verification:** The configured DNS address should be checked against the actual DNS server configuration before relying on name resolution.

**Overall conclusion:** The project provides a practical introduction to network topology design, IPv4 subnetting, server configuration, DHCP, routing concepts, and ACL troubleshooting in Cisco Packet Tracer. The submitted evidence documents the network design and configuration attempts; complete interdepartmental connectivity and successful ACL enforcement would need to be confirmed through additional testing.

## Author

**Taofeek Abdulkadir**

- **GitHub:** [https://github.com/taofeekadri-cmd/Network-Project/edit/main/README.md](https://github.com/taofeekadri-cmd/Network-Project/edit/main/README.md)
- **LinkedIn&#x20;**&#x77;ww\.linkedin.com/in/taofeek-abdulkadir-08a439b4
- **Email:** taofeekadri@gmail.com
