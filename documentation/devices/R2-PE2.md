# R2-PE2

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
| Ethernet1 | - | routed | - | 192.25.53.1/24 | default | 1500 | False | - | - |
| Ethernet2 | - | routed | - | 192.25.54.1/24 | default | 1500 | False | - | - |
| Ethernet3 | - | routed | - | 192.25.76.1/24 | default | 1500 | False | - | - |
| Ethernet4 | - | routed | - | 192.25.77.1/24 | default | 1500 | False | - | - |
| Ethernet5 | - | routed | - | 192.20.25.2/24 | default | 1500 | False | - | - |
| Ethernet6 | - | routed | - | 192.21.25.2/24 | default | 1500 | False | - | - |
| Ethernet7 | - | routed | - | 192.22.25.2/24 | default | 1500 | False | - | - |
| Ethernet8 | - | routed | - | 192.23.25.2/24 | default | 1500 | False | - | - |
| Ethernet9 | - | routed | - | 192.24.25.2/24 | default | 1500 | True | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 192.25.53.1/24
!
interface Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 192.25.54.1/24
!
interface Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 192.25.76.1/24
!
interface Ethernet4
   no shutdown
   mtu 1500
   no switchport
   ip address 192.25.77.1/24
!
interface Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 192.20.25.2/24
!
interface Ethernet6
   no shutdown
   mtu 1500
   no switchport
   ip address 192.21.25.2/24
!
interface Ethernet7
   no shutdown
   mtu 1500
   no switchport
   ip address 192.22.25.2/24
!
interface Ethernet8
   no shutdown
   mtu 1500
   no switchport
   ip address 192.23.25.2/24
!
interface Ethernet9
   shutdown
   mtu 1500
   no switchport
   ip address 192.24.25.2/24
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | R2-PE2_lo0 | default | 192.168.0.25/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | R2-PE2_lo0 | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description R2-PE2_lo0
   no shutdown
   ip address 192.168.0.25/32
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
| 65202 | 192.168.0.25 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 192.20.25.1 | 65220 | default | - | - | - | - | - | - | - | - | - |
| 192.21.25.1 | 65220 | default | - | - | - | - | - | - | - | - | - |
| 192.22.25.1 | 65222 | default | - | - | - | - | - | - | - | - | - |
| 192.23.25.1 | 65223 | default | - | - | - | - | - | - | - | - | - |
| 192.25.53.2 | 65201 | default | - | - | - | - | - | - | - | - | - |
| 192.25.54.2 | 65201 | default | - | - | - | - | - | - | - | - | - |
| 192.25.76.2 | 65003 | default | - | - | - | - | - | - | - | - | - |
| 192.25.77.2 | 65003 | default | - | - | - | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65202
   router-id 192.168.0.25
   neighbor 192.20.25.1 remote-as 65220
   neighbor 192.21.25.1 remote-as 65220
   neighbor 192.22.25.1 remote-as 65222
   neighbor 192.23.25.1 remote-as 65223
   neighbor 192.25.53.2 remote-as 65201
   neighbor 192.25.54.2 remote-as 65201
   neighbor 192.25.76.2 remote-as 65003
   neighbor 192.25.77.2 remote-as 65003
   !
   address-family ipv4
      network 192.168.0.25/32
```
