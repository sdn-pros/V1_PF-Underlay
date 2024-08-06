# PE4

## Table of Contents

- [Management](#management)
  - [DNS Domain](#dns-domain)
  - [Management API HTTP](#management-api-http)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router ISIS](#router-isis)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [MPLS](#mpls)
  - [MPLS and LDP](#mpls-and-ldp)
  - [MPLS Interfaces](#mpls-interfaces)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)

## Management

### DNS Domain

DNS domain: atd.lab

#### DNS Domain Device Configuration

```eos
dns domain atd.lab
!
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | Default Services |
| ---- | ----- | ---------------- |
| False | True | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT | - | - |

#### Management API HTTP Device Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf MGMT
      no shutdown
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **mstp**

#### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 32768 |

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
spanning-tree mst 0 priority 32768
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Device Configuration

```eos
!
vlan internal order ascending range 1006 1199
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
| Ethernet1 | P2P_LINK_TO_PE3_Ethernet1 | routed | - | 192.168.102.45/31 | default | 1500 | False | - | - |
| Ethernet2 | P2P_LINK_TO_P3_Ethernet3 | routed | - | 192.168.102.39/31 | default | 1500 | False | - | - |
| Ethernet3 | P2P_LINK_TO_P4_Ethernet3 | routed | - | 192.168.102.43/31 | default | 1500 | False | - | - |
| Ethernet4 | REGION2 | routed | - | 192.53.84.2/24 | VRF_A | - | False | - | - |
| Ethernet5 | REGION2 | routed | - | 192.54.84.2/24 | VRF_A | - | False | - | - |
| Ethernet6 | P2P_LINK_TO_RR6_Ethernet7 | routed | - | 192.168.102.52/31 | default | 1500 | False | - | - |
| Ethernet8 | P2P_LINK_TO_RR5_Ethernet13 | routed | - | 192.168.102.50/31 | default | 1500 | False | - | - |

##### ISIS

| Interface | Channel Group | ISIS Instance | ISIS BFD | ISIS Metric | Mode | ISIS Circuit Type | Hello Padding | Authentication Mode |
| --------- | ------------- | ------------- | -------- | ----------- | ---- | ----------------- | ------------- | ------------------- |
| Ethernet1 | - | CORE | - | 50 | point-to-point | level-1 | True | - |
| Ethernet2 | - | CORE | - | 50 | point-to-point | level-1 | True | - |
| Ethernet3 | - | CORE | - | 50 | point-to-point | level-1 | True | - |
| Ethernet6 | - | CORE | - | 50 | point-to-point | level-1 | True | - |
| Ethernet8 | - | CORE | - | 50 | point-to-point | level-1 | True | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_PE3_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 192.168.102.45/31
   mpls ip
   isis enable CORE
   isis circuit-type level-1
   isis metric 50
   isis hello padding
   isis network point-to-point
!
interface Ethernet2
   description P2P_LINK_TO_P3_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 192.168.102.39/31
   mpls ip
   isis enable CORE
   isis circuit-type level-1
   isis metric 50
   isis hello padding
   isis network point-to-point
!
interface Ethernet3
   description P2P_LINK_TO_P4_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 192.168.102.43/31
   mpls ip
   isis enable CORE
   isis circuit-type level-1
   isis metric 50
   isis hello padding
   isis network point-to-point
!
interface Ethernet4
   description REGION2
   no shutdown
   no switchport
   vrf VRF_A
   ip address 192.53.84.2/24
!
interface Ethernet5
   description REGION2
   no shutdown
   no switchport
   vrf VRF_A
   ip address 192.54.84.2/24
!
interface Ethernet6
   description P2P_LINK_TO_RR6_Ethernet7
   no shutdown
   mtu 1500
   no switchport
   ip address 192.168.102.52/31
   mpls ip
   isis enable CORE
   isis circuit-type level-1
   isis metric 50
   isis hello padding
   isis network point-to-point
!
interface Ethernet8
   description P2P_LINK_TO_RR5_Ethernet13
   no shutdown
   mtu 1500
   no switchport
   ip address 192.168.102.50/31
   mpls ip
   isis enable CORE
   isis circuit-type level-1
   isis metric 50
   isis hello padding
   isis network point-to-point
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | MPLS_Overlay_peering | default | 192.168.101.24/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | MPLS_Overlay_peering | default | - |

##### ISIS

| Interface | ISIS instance | ISIS metric | Interface mode |
| --------- | ------------- | ----------- | -------------- |
| Loopback0 | CORE | - | passive |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description MPLS_Overlay_peering
   no shutdown
   ip address 192.168.101.24/32
   isis enable CORE
   isis passive
   node-segment ipv4 index 224
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### Virtual Router MAC Address

#### Virtual Router MAC Address Summary

Virtual Router MAC Address: 02:1c:73:00:dc:00

#### Virtual Router MAC Address Device Configuration

```eos
!
ip virtual-router mac-address 02:1c:73:00:dc:00
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| MGMT | True |
| VRF_A | True |

#### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf MGMT
ip routing vrf VRF_A
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| MGMT | false |
| VRF_A | false |

### Static Routes

#### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP | Exit interface | Administrative Distance | Tag | Route Name | Metric |
| --- | ------------------ | ----------- | -------------- | ----------------------- | --- | ---------- | ------ |
| MGMT | 0.0.0.0/0 | 192.168.0.1 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 192.168.0.1
```

### Router ISIS

#### Router ISIS Summary

| Settings | Value |
| -------- | ----- |
| Instance | CORE |
| Net-ID | 49.0001.0000.0001.0024.00 |
| Type | level-1 |
| Router-ID | 192.168.101.24 |
| Log Adjacency Changes | True |
| SR MPLS Enabled | True |

#### ISIS Interfaces Summary

| Interface | ISIS Instance | ISIS Metric | Interface Mode |
| --------- | ------------- | ----------- | -------------- |
| Ethernet1 | CORE | 50 | point-to-point |
| Ethernet2 | CORE | 50 | point-to-point |
| Ethernet3 | CORE | 50 | point-to-point |
| Ethernet6 | CORE | 50 | point-to-point |
| Ethernet8 | CORE | 50 | point-to-point |
| Loopback0 | CORE | - | passive |

#### ISIS Segment-routing Node-SID

| Loopback | IPv4 Index | IPv6 Index |
| -------- | ---------- | ---------- |
| Loopback0 | 224 | - |

#### ISIS IPv4 Address Family Summary

| Settings | Value |
| -------- | ----- |
| IPv4 Address-family Enabled | True |
| Maximum-paths | 4 |

#### Router ISIS Device Configuration

```eos
!
router isis CORE
   net 49.0001.0000.0001.0024.00
   is-type level-1
   router-id ipv4 192.168.101.24
   log-adjacency-changes
   !
   address-family ipv4 unicast
      maximum-paths 4
   !
   segment-routing mpls
      no shutdown
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65001 | 192.168.101.24 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### MPLS-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | mpls |
| Remote AS | 65001 |
| Source | Loopback0 |
| BFD | True |
| Send community | all |
| Maximum routes | 0 (no limit) |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 192.168.101.35 | Inherited from peer group MPLS-OVERLAY-PEERS | default | - | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS | - | Inherited from peer group MPLS-OVERLAY-PEERS | - | - | - | - |
| 192.168.101.36 | Inherited from peer group MPLS-OVERLAY-PEERS | default | - | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS | - | Inherited from peer group MPLS-OVERLAY-PEERS | - | - | - | - |
| 192.53.84.1 | 65201 | VRF_A | - | - | - | - | - | - | - | - | - |
| 192.54.84.1 | 65201 | VRF_A | - | - | - | - | - | - | - | - | - |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Encapsulation |
| ---------- | -------- | ------------- |

#### Router BGP VPN-IPv4 Address Family

##### VPN-IPv4 Peer Groups

| Peer Group | Activate | Route-map In | Route-map Out | RCF In | RCF Out |
| ---------- | -------- | ------------ | ------------- | ------ | ------- |
| MPLS-OVERLAY-PEERS | True | - | - | - | - |

#### Router BGP VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| VRF_A | 192.168.101.24:19 | connected |

#### Router BGP Device Configuration

```eos
!
router bgp 65001
   router-id 192.168.101.24
   maximum-paths 4 ecmp 4
   no bgp default ipv4-unicast
   neighbor MPLS-OVERLAY-PEERS peer group
   neighbor MPLS-OVERLAY-PEERS remote-as 65001
   neighbor MPLS-OVERLAY-PEERS update-source Loopback0
   neighbor MPLS-OVERLAY-PEERS bfd
   neighbor MPLS-OVERLAY-PEERS send-community
   neighbor MPLS-OVERLAY-PEERS maximum-routes 0
   neighbor 192.168.101.35 peer group MPLS-OVERLAY-PEERS
   neighbor 192.168.101.35 description RR5
   neighbor 192.168.101.36 peer group MPLS-OVERLAY-PEERS
   neighbor 192.168.101.36 description RR6
   !
   address-family evpn
   !
   address-family ipv4
      no neighbor MPLS-OVERLAY-PEERS activate
   !
   address-family vpn-ipv4
      neighbor MPLS-OVERLAY-PEERS activate
      neighbor default encapsulation mpls next-hop-self source-interface Loopback0
   !
   vrf VRF_A
      rd 192.168.101.24:19
      route-target import vpn-ipv4 65001:19
      route-target export vpn-ipv4 65001:19
      router-id 192.168.101.24
      neighbor 192.53.84.1 remote-as 65201
      neighbor 192.54.84.1 remote-as 65201
      redistribute connected
      !
      address-family ipv4
         neighbor 192.53.84.1 activate
         neighbor 192.54.84.1 activate
   !
   router bgp 65001
     address-family ipv4
       no neighbor Region1-UNDERLAY-PEERS activate

     vrf VRF_A
       neighbor Region2-UNDERLAY-PEERS peer group
       neighbor Region2-UNDERLAY-PEERS remote-as 65201
       neighbor 192.54.83.1 peer group Region2-UNDERLAY-PEERS
       neighbor 192.54.83.1 description RR3-Underlay-Peer
       neighbor 192.54.84.1 peer group Region2-UNDERLAY-PEERS
       neighbor 192.54.84.1 description RR4-Underlay-Peer
     
       address-family ipv4
         neighbor Region2-UNDERLAY-PEERS activate
         network 192.168.101.24/32
```

## BFD

### Router BFD

#### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 300 | 300 | 3 |

#### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
```

## MPLS

### MPLS and LDP

#### MPLS and LDP Summary

| Setting | Value |
| -------- | ---- |
| MPLS IP Enabled | True |
| LDP Enabled | False |
| LDP Router ID | - |
| LDP Interface Disabled Default | - |
| LDP Transport-Address Interface | - |

#### MPLS and LDP Device Configuration

```eos
!
mpls ip
```

### MPLS Interfaces

| Interface | MPLS IP Enabled | LDP Enabled | IGP Sync |
| --------- | --------------- | ----------- | -------- |
| Ethernet1 | True | - | - |
| Ethernet2 | True | - | - |
| Ethernet3 | True | - | - |
| Ethernet6 | True | - | - |
| Ethernet8 | True | - | - |

## Multicast

### IP IGMP Snooping

#### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

#### IP IGMP Snooping Device Configuration

```eos
```

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | enabled |
| VRF_A | enabled |

### VRF Instances Device Configuration

```eos
!
vrf instance MGMT
!
vrf instance VRF_A
```
