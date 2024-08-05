# Edge12

## Table of Contents

- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [IP Routing](#ip-routing)
  - [Router BGP](#router-bgp)

## Spanning Tree

### Spanning Tree Summary

STP mode: **mstp**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | - | routed | - | 192.12.32.1/24 | default | 1500 | False | - | - |
| Ethernet2 | - | routed | - | 192.12.15.1/24 | default | 1500 | False | - | - |
| Ethernet3 | - | routed | - | 192.12.16.1/24 | default | 1500 | False | - | - |
| Ethernet4 | - | routed | - | 192.12.31.1/24 | default | 1500 | True | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 192.12.32.1/24
!
interface Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 192.12.15.1/24
!
interface Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 192.12.16.1/24
!
interface Ethernet4
   shutdown
   mtu 1500
   no switchport
   ip address 192.12.31.1/24
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | Edge-12_lo0 | default | 192.168.0.12/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | Edge-12_lo0 | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description Edge-12_lo0
   no shutdown
   ip address 192.168.0.12/32
```

## Routing

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |

#### IP Routing Device Configuration

```eos
!
ip routing
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65112 | 192.168.0.12 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 192.12.15.2 | 65102 | default | - | - | - | - | - | - | - | - | - |
| 192.12.16.2 | 65103 | default | - | - | - | - | - | - | - | - | - |
| 192.12.32.2 | 65112 | default | - | - | - | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65112
   router-id 192.168.0.12
   neighbor 192.12.15.2 remote-as 65102
   neighbor 192.12.16.2 remote-as 65103
   neighbor 192.12.32.2 remote-as 65112
   !
   address-family ipv4
      network 192.168.0.12/32
```
