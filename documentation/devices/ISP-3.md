# ISP-3

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
| Ethernet1 | - | routed | - | 192.51.75.2/24 | default | 1500 | False | - | - |
| Ethernet2 | - | routed | - | 192.52.75.2/24 | default | 1500 | False | - | - |
| Ethernet3 | - | routed | - | 192.54.75.2/24 | default | 1500 | False | - | - |
| Ethernet4 | - | routed | - | 192.53.75.2/24 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 192.51.75.2/24
!
interface Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 192.52.75.2/24
!
interface Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 192.54.75.2/24
!
interface Ethernet4
   no shutdown
   mtu 1500
   no switchport
   ip address 192.53.75.2/24
!
interface Ethernet5
   shutdown
   mtu 1500
   no switchport
!
interface Ethernet6
   shutdown
   mtu 1500
   no switchport
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ISP-3_lo0 | default | 192.168.0.75/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ISP-3_lo0 | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ISP-3_lo0
   no shutdown
   ip address 192.168.0.75/32
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
| 65002 | 192.168.0.75 |

#### Router BGP Peer Groups

##### REGION1

| Settings | Value |
| -------- | ----- |
| Remote AS | 65101 |

##### REGION2

| Settings | Value |
| -------- | ----- |
| Remote AS | 65201 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 192.51.75.1 | Inherited from peer group REGION1 | default | - | - | - | - | - | - | - | - | - |
| 192.52.75.1 | Inherited from peer group REGION1 | default | - | - | - | - | - | - | - | - | - |
| 192.53.75.1 | Inherited from peer group REGION2 | default | - | - | - | - | - | - | - | - | - |
| 192.54.75.1 | Inherited from peer group REGION2 | default | - | - | - | - | - | - | - | - | - |

#### Router BGP VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| default | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65002
   router-id 192.168.0.75
   neighbor REGION1 peer group
   neighbor REGION1 remote-as 65101
   neighbor REGION2 peer group
   neighbor REGION2 remote-as 65201
   !
   address-family ipv4
      network 192.168.0.75/32
   !
   vrf default
      neighbor 192.51.75.1 peer group REGION1
      neighbor 192.52.75.1 peer group REGION1
      neighbor 192.53.75.1 peer group REGION2
      neighbor 192.54.75.1 peer group REGION2
```
