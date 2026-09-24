
# CCNA Lab 01 — Small-Office-LANs


Project Name:
Small Office LAN

Lab Number:
Lab-01

Purpose:
This lab demonstrates how to build and configure a basic Small Office Local Area Network (LAN) using Cisco Packet Tracer.

The main purpose of this lab is to understand how PCs, switches, and routers communicate within a network.

TOPOLOGY

Devices Used:

1 Cisco Router
1 Cisco Switch
4 PCs
Ethernet cables

Basic topology:

PC0 ----
PC1 -----
SW1 -------- R1
PC2 -----/
PC3 ----/


NETWORK INFORMATION

Network Address:
192.168.1.0/24

Subnet Mask:
255.255.255.0

Default Gateway:
192.168.1.1

Example IP Addresses:

Router:
192.168.1.1

PC0:
192.168.1.10

PC1:
192.168.1.11

PC2:
192.168.1.12

PC3:
192.168.1.13

TESTING

After configuring the devices, connectivity can be tested using the ping command.

Example:

PC0 > ping 192.168.1.11

PC0 > ping 192.168.1.12

PC0 > ping 192.168.1.13

PC0 > ping 192.168.1.14

If the replies are successful, the LAN is working correctly.
