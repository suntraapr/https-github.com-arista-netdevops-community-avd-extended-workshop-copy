# ATD_FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| ATD_FABRIC | l3leaf | leaf1 | 192.168.0.12/24 | vEOS-lab | Provisioned | - |
| ATD_FABRIC | l3leaf | leaf2 | 192.168.0.13/24 | vEOS-lab | Provisioned | - |
| ATD_FABRIC | spine | spine1 | 192.168.0.10/24 | vEOS-lab | Provisioned | - |
| ATD_FABRIC | spine | spine2 | 192.168.0.11/24 | vEOS-lab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | leaf1 | Ethernet1 | mlag_peer | leaf2 | Ethernet1 |
| l3leaf | leaf1 | Ethernet2 | spine | spine1 | Ethernet2 |
| l3leaf | leaf1 | Ethernet3 | spine | spine2 | Ethernet2 |
| l3leaf | leaf1 | Ethernet6 | mlag_peer | leaf2 | Ethernet6 |
| l3leaf | leaf2 | Ethernet2 | spine | spine1 | Ethernet3 |
| l3leaf | leaf2 | Ethernet3 | spine | spine2 | Ethernet3 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.30.255.0/24 | 256 | 8 | 3.13 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| leaf1 | Ethernet2 | 172.30.255.1/31 | spine1 | Ethernet2 | 172.30.255.0/31 |
| leaf1 | Ethernet3 | 172.30.255.3/31 | spine2 | Ethernet2 | 172.30.255.2/31 |
| leaf2 | Ethernet2 | 172.30.255.5/31 | spine1 | Ethernet3 | 172.30.255.4/31 |
| leaf2 | Ethernet3 | 172.30.255.7/31 | spine2 | Ethernet3 | 172.30.255.6/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.0.255.0/24 | 256 | 4 | 1.57 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| ATD_FABRIC | leaf1 | 192.0.255.3/32 |
| ATD_FABRIC | leaf2 | 192.0.255.4/32 |
| ATD_FABRIC | spine1 | 192.0.255.1/32 |
| ATD_FABRIC | spine2 | 192.0.255.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.0.254.0/24 | 256 | 2 | 0.79 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| ATD_FABRIC | leaf1 | 192.0.254.3/32 |
| ATD_FABRIC | leaf2 | 192.0.254.3/32 |
