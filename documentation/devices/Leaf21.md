# Leaf21

## Table of Contents

- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Router BGP](#router-bgp)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)

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
| Ethernet1 | - | routed | - | 172.16.21.254/24 | VRF_A | 1500 | False | - | - |
| Ethernet2 | - | routed | - | 192.20.33.2/24 | default | 1500 | False | - | - |
| Ethernet3 | - | routed | - | 192.21.33.2/24 | default | 1500 | False | - | - |
| Ethernet4 | - | routed | - | 192.22.33.2/24 | default | 1500 | True | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   no shutdown
   mtu 1500
   no switchport
   vrf VRF_A
   ip address 172.16.21.254/24
!
interface Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 192.20.33.2/24
!
interface Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 192.21.33.2/24
!
interface Ethernet4
   shutdown
   mtu 1500
   no switchport
   ip address 192.22.33.2/24
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | Leaf21_lo0 | default | 192.168.0.33/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | Leaf21_lo0 | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description Leaf21_lo0
   no shutdown
   ip address 192.168.0.33/32
```

## Routing

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| VRF_A | True |

#### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf VRF_A
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| VRF_A | false |

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65220 | 192.168.0.33 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 192.20.33.1 | 65220 | default | - | - | - | - | - | - | - | - | - |
| 192.21.33.1 | 65220 | default | - | - | - | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65220
   router-id 192.168.0.33
   neighbor 192.20.33.1 remote-as 65220
   neighbor 192.21.33.1 remote-as 65220
   !
   address-family ipv4
      network 192.168.0.33/32
      redistribute connected
```

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| VRF_A | enabled |

### VRF Instances Device Configuration

```eos
!
vrf instance VRF_A
```
