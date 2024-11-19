# Multi-Site Networking Project: Fall 2024

## Overview

This project involves designing and implementing a secure, scalable, and efficient multi-location network for an organization spanning five global sites: Boston, Mumbai, New York, London, and Germany. The architecture leverages advanced features such as **OSPF**, **HSRP**, **Rapid STP**, **DNS**, **ACL**, **LACP**, and **VPN Tunneling** to ensure optimal connectivity and robust network performance.

---

## Network Design

### Subnetting

The `192.168.0.0/16` address space is divided to meet departmental and geographical requirements:

#### Boston (Headquarters) - Subnet: `192.168.0.0/24`
- **HR Department:** `192.168.0.0/27`  
  - Range: `192.168.0.1 - 192.168.0.30`  
  - Subnet Mask: `255.255.255.224`
- **Tech Department:** `192.168.0.32/27`  
  - Range: `192.168.0.33 - 192.168.0.62`  
  - Subnet Mask: `255.255.255.224`
- **Finance Department:** `192.168.0.64/27`  
  - Range: `192.168.0.65 - 192.168.0.94`  
  - Subnet Mask: `255.255.255.224`

#### Mumbai (Headquarters) - Subnet: `192.168.1.0/24`
- **HR Department:** `192.168.1.0/27`  
  - Range: `192.168.1.1 - 192.168.1.30`  
  - Subnet Mask: `255.255.255.224`
- **Tech Department:** `192.168.1.32/27`  
  - Range: `192.168.1.33 - 192.168.1.62`  
  - Subnet Mask: `255.255.255.224`
- **Finance Department:** `192.168.1.64/27`  
  - Range: `192.168.1.65 - 192.168.1.94`  
  - Subnet Mask: `255.255.255.224`

#### London (Regional Office) - Subnet: `192.168.2.0/24`
- **HR Department:** `192.168.2.0/27`  
  - Range: `192.168.2.1 - 192.168.2.30`  
  - Subnet Mask: `255.255.255.224`
- **Tech Department:** `192.168.2.32/27`  
  - Range: `192.168.2.33 - 192.168.2.62`  
  - Subnet Mask: `255.255.255.224`

#### New York (Regional Office) - Subnet: `192.168.3.0/24`
- **General Purpose:** Used for general office purposes.  
  - Range: `192.168.3.1 - 192.168.3.254`  
  - Subnet Mask: `255.255.255.0`

#### Germany (Regional Office) - Subnet: `192.168.4.0/24`
- **General Purpose:** Used for general office purposes.  
  - Range: `192.168.4.1 - 192.168.4.254`  
  - Subnet Mask: `255.255.255.0`

---

## Key Features

### **OSPF (Open Shortest Path First)**
- **Area Designation:**
  - Boston: Area 1  
  - Mumbai: Area 2  
  - London: Area 3  
  - New York: Area 4  
  - Germany: Area 5  
  - Backbone: Area 0 (connects all areas)
- **Manual Router IDs:** Assigned to all routers for clear identification.
- **Point-to-Point Links:** Configured without DR/BDR to enhance efficiency for specific connections.
- **Inter-Area Routing:** Backbone ensures smooth traffic flow between areas.

### **HSRP (Hot Standby Router Protocol)**
- Implemented in Boston and Mumbai headquarters for gateway redundancy.
- **Timers:**
  - Hello Timer: 2 seconds  
  - Hold Timer: 6 seconds
- Provides seamless failover between active and standby routers.

### **Rapid Spanning Tree Protocol (RSTP)**
- Enabled in all regional offices to prevent loops and ensure quick recovery.
- **BPDU Guard and PortFast:** Configured on host-facing ports to secure and speed up the network.
- **Redundancy:** Rapid failover of blocked ports during topology changes.

### **ACL (Access Control List)**
- Finance department access is restricted to enhance security:
  - Finance can access all departments, but no other department can access Finance.
- Extended ACLs are applied to filter traffic based on source and destination IPs and protocols.

### **LACP (Link Aggregation Control Protocol)**
- Configured in New York for bandwidth and redundancy:
  - Combines multiple physical links into a logical channel.
  - Enhances network performance and ensures traffic continuity in case of link failure.

### **VPN Tunneling**
- VPN implemented between Boston and Mumbai HQs:
  - Subnet: `192.168.6.0/30`
  - Ensures secure and encrypted communication between headquarters.
  - Provides reliable connectivity for inter-office operations.

### **DNS Configuration**
- Centralized DNS server located in Boston.
- Resolves hostnames for all routers, enabling hostname-based communication (e.g., `ping BOR1` instead of using IP).

### **SSH for Secure Management**
- SSH is configured on all routers for secure remote management.
- Ensures encrypted communication, enhancing administrative security.

---

## Testing and Validation

1. **VLAN Testing:**
   - Validate inter-departmental VLAN isolation.
   - Test trunk configurations and DHCP assignment.

2. **Routing Testing:**
   - Verify OSPF area configurations.
   - Test inter-area connectivity through the Backbone (Area 0).

3. **HSRP Testing:**
   - Simulate primary router failure and verify seamless switch to standby router.

4. **Redundancy Testing:**
   - Test RSTP functionality by disabling active ports and observing failover to blocked ports.

5. **DNS and SSH Testing:**
   - Use DNS to resolve router hostnames.
   - Validate secure login to routers via SSH.

6. **ACL Testing:**
   - Verify that Finance departments are isolated and can only be accessed as per policy.

7. **LACP and VPN Testing:**
   - Ensure proper traffic flow and redundancy using LACP.
   - Test secure communication between HQs via VPN.

---

## Concepts Learned

- Subnetting and VLAN configurations for efficient IP management.
- Advanced routing with OSPF, including area concepts and redundancy.
- Configuring secure and redundant network infrastructure using HSRP, RSTP, EtherChannel, and ACLs.
- Securing administrative access with SSH and enhancing DNS usability.
- Establishing secure inter-office communication using VPN tunneling.

---

## Conclusion

This project demonstrates a robust, multi-location network design optimized for scalability, security, and efficiency. It ensures seamless interconnectivity across all locations while addressing departmental isolation and redundancy. By integrating advanced protocols like OSPF, HSRP, RSTP, ACL, LACP, and VPN, the network achieves high reliability and performance.
