# Edge22

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
| Ethernet1 | - | routed | - | 192.22.34.1/24 | default | 1500 | False | - | - |
| Ethernet2 | - | routed | - | 192.22.25.1/24 | default | 1500 | False | - | - |
| Ethernet3 | - | routed | - | 192.22.26.1/24 | default | 1500 | False | - | - |
| Ethernet4 | - | routed | - | 192.22.33.1/24 | default | 1500 | True | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 192.22.34.1/24
!
interface Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 192.22.25.1/24
!
interface Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 192.22.26.1/24
!
interface Ethernet4
   shutdown
   mtu 1500
   no switchport
   ip address 192.22.33.1/24
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | Edge-22_lo0 | default | 192.168.0.22/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | Edge-22_lo0 | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description Edge-22_lo0
   no shutdown
   ip address 192.168.0.22/32
```

### VXLAN Interface

#### VXLAN Interface Summary

| Setting | Value |
| ------- | ----- |
| Source Interface | Dps1 |
| UDP port | 4789 |

#### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   description VTEP_Interface
   vxlan source-interface Dps1
   vxlan udp-port 4789
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
| 65222 | 192.168.0.22 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 192.22.25.2 | 65202 | default | - | - | - | - | - | - | - | - | - |
| 192.22.26.2 | 65203 | default | - | - | - | - | - | - | - | - | - |
| 192.22.34.2 | 65222 | default | - | - | - | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65222
   router-id 192.168.0.22
   neighbor 192.22.25.2 remote-as 65202
   neighbor 192.22.26.2 remote-as 65203
   neighbor 192.22.34.2 remote-as 65222
   !
   address-family ipv4
      network 192.168.0.22/32
      redistribute connected
```
