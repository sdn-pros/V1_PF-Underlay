# ISP-1

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
| Ethernet1 | - | routed | - | 192.16.51.1/24 | default | 1500 | False | - | - |
| Ethernet2 | - | routed | - | 192.16.52.1/24 | default | 1500 | False | - | - |
| Ethernet3 | - | routed | - | 192.16.71.1/24 | default | 1500 | False | - | - |
| Ethernet4 | - | routed | - | 192.16.72.1/24 | default | 1500 | False | - | - |
| Ethernet5 | - | routed | - | 192.10.16.2/24 | default | 1500 | False | - | - |
| Ethernet6 | - | routed | - | 192.11.16.2/24 | default | 1500 | False | - | - |
| Ethernet7 | - | routed | - | 192.12.16.2/24 | default | 1500 | False | - | - |
| Ethernet8 | - | routed | - | 192.13.16.2/24 | default | 1500 | False | - | - |
| Ethernet9 | - | routed | - | 192.14.16.2/24 | default | 1500 | True | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 192.16.51.1/24
!
interface Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 192.16.52.1/24
!
interface Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 192.16.71.1/24
!
interface Ethernet4
   no shutdown
   mtu 1500
   no switchport
   ip address 192.16.72.1/24
!
interface Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 192.10.16.2/24
!
interface Ethernet6
   no shutdown
   mtu 1500
   no switchport
   ip address 192.11.16.2/24
!
interface Ethernet7
   no shutdown
   mtu 1500
   no switchport
   ip address 192.12.16.2/24
!
interface Ethernet8
   no shutdown
   mtu 1500
   no switchport
   ip address 192.13.16.2/24
!
interface Ethernet9
   shutdown
   mtu 1500
   no switchport
   ip address 192.14.16.2/24
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ISP_lo0 | default | 192.168.0.16/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ISP_lo0 | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ISP_lo0
   no shutdown
   ip address 192.168.0.16/32
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
| 65103 | 192.168.0.16 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 192.10.16.1 | 65110 | default | - | - | - | - | - | - | - | - | - |
| 192.11.16.1 | 65110 | default | - | - | - | - | - | - | - | - | - |
| 192.12.16.1 | 65112 | default | - | - | - | - | - | - | - | - | - |
| 192.13.16.1 | 65113 | default | - | - | - | - | - | - | - | - | - |
| 192.16.51.2 | 65101 | default | - | - | - | - | - | - | - | - | - |
| 192.16.52.2 | 65101 | default | - | - | - | - | - | - | - | - | - |
| 192.16.71.2 | 65000 | default | - | - | - | - | - | - | - | - | - |
| 192.16.72.2 | 65000 | default | - | - | - | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65103
   router-id 192.168.0.16
   neighbor 192.10.16.1 remote-as 65110
   neighbor 192.11.16.1 remote-as 65110
   neighbor 192.12.16.1 remote-as 65112
   neighbor 192.13.16.1 remote-as 65113
   neighbor 192.16.51.2 remote-as 65101
   neighbor 192.16.52.2 remote-as 65101
   neighbor 192.16.71.2 remote-as 65000
   neighbor 192.16.72.2 remote-as 65000
   !
   address-family ipv4
      network 192.168.0.16/32
      redistribute connected
```
