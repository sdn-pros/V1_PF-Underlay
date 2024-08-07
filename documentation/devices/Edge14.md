# Edge14

## Table of Contents

- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VXLAN Interface](#vxlan-interface)
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
| Ethernet1 | - | routed | - | 172.16.14.254/24 | VRF_A | 1500 | False | - | - |
| Ethernet2 | - | routed | - | 192.14.15.1/24 | default | 1500 | False | - | - |
| Ethernet3 | - | routed | - | 192.14.16.1/24 | default | 1500 | False | - | - |
| Ethernet4 | - | routed | - | 192.14.51.1/24 | default | 1500 | False | - | - |
| Ethernet5 | - | routed | - | 192.14.52.1/24 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   no shutdown
   mtu 1500
   no switchport
   vrf VRF_A
   ip address 172.16.14.254/24
!
interface Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 192.14.15.1/24
!
interface Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 192.14.16.1/24
!
interface Ethernet4
   no shutdown
   mtu 1500
   no switchport
   ip address 192.14.51.1/24
!
interface Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 192.14.52.1/24
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | Edge-14_lo0 | default | 192.168.0.14/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | Edge-14_lo0 | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description Edge-14_lo0
   no shutdown
   ip address 192.168.0.14/32
```

### VXLAN Interface

#### VXLAN Interface Summary

| Setting | Value |
| ------- | ----- |
| Source Interface | Dps1 |
| UDP port | 4789 |

##### VRF to VNI and Multicast Group Mappings

| VRF | VNI | Multicast Group |
| ---- | --- | --------------- |
| default | 101 | - |
| VRF_A | 19 | - |

#### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   description VTEP_Interface
   vxlan source-interface Dps1
   vxlan udp-port 4789
   vxlan vrf default vni 101
   vxlan vrf VRF_A vni 19
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
| 65114 | 192.168.0.14 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 192.14.51.2 | 65101 | default | - | - | - | - | - | - | - | - | - |
| 192.14.52.2 | 65101 | default | - | - | - | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65114
   router-id 192.168.0.14
   neighbor 192.14.51.2 remote-as 65101
   neighbor 192.14.52.2 remote-as 65101
   !
   address-family ipv4
      network 192.168.0.14/32
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
