# CCNA Lab 02 — VLAN and Inter-VLAN Routing

## 📌 Overview

This lab demonstrates how to configure VLANs on a Cisco switch and enable communication between different VLANs using Inter-VLAN Routing with Router-on-a-Stick.

## 🎯 Objectives

* Understand VLANs
* Create VLAN 10 and VLAN 20
* Assign switch ports to VLANs
* Configure access ports
* Configure trunking
* Configure Router-on-a-Stick
* Configure router sub-interfaces
* Configure default gateways
* Test communication between different VLANs
* Practice basic network troubleshooting

## 🖥️ Devices Used

* 1 × Cisco Router 2911
* 1 × Cisco Switch 2960
* 2 × PCs
* 2 × Laptos
* Copper Straight-Through cables

## 🔹 VLAN Configuration

### VLAN 10 — STAFF

* Fa0/1 → PC0
* Fa0/2 → PC1
* Network: 192.168.10.0/24
* Gateway: 192.168.10.1

### VLAN 20 — STUDENT

* Fa0/3 → PC2
* Fa0/4 → PC3
* Network: 192.168.20.0/24
* Gateway: 192.168.20.1

## 🔗 Trunk Configuration

SW1 Fa0/24 is configured as a trunk port.

The trunk carries traffic for:

* VLAN 10
* VLAN 20

The trunk connects:

R1 G0/0 ↔ SW1 Fa0/24

## 🚀 Inter-VLAN Routing

Router-on-a-Stick is used to route traffic between VLAN 10 and VLAN 20.

### R1 Sub-Interfaces

text
G0/0.10 → VLAN 10 → 192.168.10.1
G0/0.20 → VLAN 20 → 192.168.20.1


## 🧪 Testing

### Same VLAN Test

PC0 → PC1

text
ping 192.168.10.11


Result: Successful

### Inter-VLAN Test

PC0 → PC2

text
ping 192.168.20.10


Result: Successful

This confirms that Inter-VLAN Routing is working.

## 🔍 Verification Commands

### Switch

cisco
show vlan brief
show interfaces trunk
show running-config
show interfaces status
show mac address-table


### Router

cisco
show ip interface brief
show ip route
show running-config
show arp

## 🧠 Key Concepts Learned

### VLAN

VLAN divides a physical switch into separate logical networks.

### Access Port

An access port normally belongs to one VLAN and connects to end devices such as PCs.

### Trunk Port

A trunk port carries traffic from multiple VLANs between network devices.

### Inter-VLAN Routing

Inter-VLAN Routing allows devices in different VLANs to communicate through a Layer 3 device such as a router.

### Router-on-a-Stick

Router-on-a-Stick uses one physical router interface with multiple sub-interfaces to provide routing between VLANs.



## 👨‍💻 Author

Bibek Bahadur Mahata

BIM Graduate | Aspiring Network Engineer
