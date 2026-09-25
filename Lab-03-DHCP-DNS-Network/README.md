# Lab-03: DHCP & DNS Network

## 📌 About This Lab

This is my third Cisco Packet Tracer networking lab, focused on configuring **DHCP (Dynamic Host Configuration Protocol)** and **DNS (Domain Name System)**.

In this lab, I configured a Cisco router to assign IP addresses automatically to PCs using DHCP and a dedicated server to provide DNS services for name resolution.

## 🎯 Objectives

* Understand DHCP and its working process.
* Configure a DHCP pool on a Cisco router.
* Assign IP addresses automatically to PCs.
* Configure a static IP address on a server.
* Enable and configure DNS services.
* Understand DNS records and name resolution.
* Test connectivity using `ping` and verify configurations using Cisco IOS commands.

## 🖥️ Network Topology

**Devices used:**

* 1 × Cisco Router (R1)
* 1 × Cisco Switch (SW1)
* 2 × Pcs (PC0, PC1)
* 1 × Server (DHCP/DNS lab server; DNS service enabled)
* Copper straight-through cables

### Network Diagram

```text
                 ┌─────────────────┐
                 │    Router R1    │
                 │  192.168.10.1   │
                 │   DHCP Server   │
                 └────────┬────────┘
                          │
                          │
                 ┌────────┴────────┐
                 │    Switch SW1   │
                 └───┬────┬────┬───┘
                     │    │    │
                ┌────┘    │    └────┐
                │         │         │
           ┌────┴───┐ ┌───┴────┐ ┌──┴────────┐
           │  PC0   │ │  PC1   │ │  Server   │
           │  DHCP  │ │  DHCP  │ │  DNS      │
           └────────┘ └────────┘ └───────────┘
```

## 🌐 IP Addressing Table

| Device | Interface | IP Address      | Configuration |
| ------ | --------- | --------------- | ------------- |
| R1     | G0/0      | 192.168.10.1    | Static        |
| Server | NIC       | 192.168.10.2    | Static        |
| PC0    | NIC       | 192.168.10.100* | DHCP          |
| PC1    | NIC       | 192.168.10.101* | DHCP          |

*Example DHCP addresses. The actual addresses may differ depending on the lease order and available addresses.*

**Subnet Mask:** `255.255.255.0`
**Default Gateway:** `192.168.10.1`
**DNS Server:** `192.168.10.2`
**Network:** `192.168.10.0/24`

## ⚙️ Configuration

### 1. Router Configuration

Configure the router interface and enable it:

```cisco
enable
configure terminal

interface gigabitEthernet 0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit
```

### 2. Configure DHCP

Exclude the IP addresses reserved for network devices:

```cisco
ip dhcp excluded-address 192.168.10.1 192.168.10.99
```

Create a DHCP pool and configure the network settings:

```cisco
ip dhcp pool OFFICE-LAN
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 192.168.10.2
exit

end
write memory
```

### 3. Server Configuration

Open **Server → Desktop → IP Configuration** and select Static.

| Setting         | Value         |
| --------------- | ------------- |
| IP Address      | 192.168.10.2  |
| Subnet Mask     | 255.255.255.0 |
| Default Gateway | 192.168.10.1  |
| DNS Server      | 192.168.10.2  |

### 4. DNS Configuration

1. Open **Server → Services → DNS**.
2. Set DNS to **ON**.
3. Add the following DNS record:

| Field   | Value                                   |
| ------- | --------------------------------------- |
| Name    | [www.lab3.local](http://www.lab3.local) |
| Type    | A Record                                |
| Address | 192.168.10.2                            |

4. Click **Add** to save the DNS record.

This record maps the domain name `www.lab3.local` to the server's IP address.

### 5. PC Configuration

For both PC0 and PC1:

1. Open the PC.
2. Select **Desktop → IP Configuration**.
3. Select **DHCP**.
4. Verify that the PC receives its IP address, subnet mask, default gateway, and DNS server automatically.

## 🧪 Testing and Verification

### Check IP Configuration

On each PC, open Command Prompt:

```text
ipconfig
```

Verify the IP address, subnet mask, default gateway, and DNS server.

### Test Router Connectivity

```text
ping 192.168.10.1
```

### Test Server Connectivity

```text
ping 192.168.10.2
```

### Test PC-to-PC Connectivity

```text
ping 192.168.10.101
```

Use the actual IP address assigned to PC1 if it differs from the example.

### Test DNS Name Resolution

```text
ping www.lab3.local
```

The PC should resolve the name to `192.168.10.2` and attempt to ping that address.

### Verify DHCP on the Router

```cisco
show ip dhcp binding
show ip dhcp pool
show ip interface brief
show running-config
```

These commands help verify the DHCP leases, pool configuration, router interface status, and running configuration.

## 📚 Key Concepts Learned

### DHCP

Automatically assigns IP addresses and other network settings to clients, reducing manual configuration.

### DHCP Pool

Defines the network and configuration information that the router provides to DHCP clients.

### Automatic IP Addressing

Allows PCs to receive their network settings automatically without manually entering each value.

### DNS

Translates human-readable domain names into IP addresses using DNS records.

### Name Resolution

The process of finding an IP address associated with a domain name, such as `www.lab3.local`.

## 📝 Important Notes

* The router provides DHCP services in this lab.
* The server provides DNS services.
* The server uses a static IP address so that clients can consistently reach it.
* PCs use DHCP to receive their network settings.
* A successful ping to the server by IP address confirms IP connectivity, while a successful ping using its DNS name also tests name resolution.
* The first ping may time out while ARP or DNS resolution takes place. Retry if necessary.

## 📂 Repository Files

```text
Lab-03-DHCP-DNS-Network/
│
├── README.md
├── topology.png
├── DHCP-DNS-Network.pkt
└── configuration.txt
```

## 🏁 Conclusion

This lab demonstrates how to configure DHCP on a Cisco router and DNS on a dedicated server using Cisco Packet Tracer. It provides practical experience with automatic IP addressing, DNS records, name resolution, and basic network connectivity testing.

**Lab:** 03
**Topic:** DHCP & DNS Network
**Tool:** Cisco Packet Tracer
**Level:** Beginner / CCNA Fundamentals

