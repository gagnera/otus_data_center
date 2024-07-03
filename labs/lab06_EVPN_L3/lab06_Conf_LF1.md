# LF1
``` 
hostname LF1
!
spanning-tree mode mstp
!
vlan 100
!
vrf instance EVPNL3
!
interface Ethernet1
!
interface Ethernet2
   description SP0
   no switchport
   ip address 10.0.0.6/30
!
interface Ethernet3
   description SP1
   no switchport
   ip address 10.0.1.6/30
!
interface Ethernet4
!
interface Ethernet5
!
interface Ethernet6
!
interface Ethernet7
!
interface Ethernet8
   description CL10
   switchport access vlan 100
!
interface Loopback0
   ip address 10.0.254.1/32
!
interface Management1
!
interface Vlan100
   description BLUE_VLAN
   vrf EVPNL3
   ip address virtual 172.22.1.1/24
!
interface Vxlan1
   vxlan source-interface Loopback0
   vxlan udp-port 4789
   vxlan vlan 100 vni 100
   vxlan vrf EVPNL3 vni 1
   vxlan learn-restrict any
!
ip routing
ip routing vrf EVPNL3
!
router bgp 65000
   router-id 10.0.254.1
   timers bgp 1 3
   maximum-paths 2 ecmp 2
   neighbor EVPN peer group
   neighbor EVPN remote-as 65000
   neighbor EVPN update-source Loopback0
   neighbor EVPN send-community extended
   neighbor 10.0.0.5 remote-as 65000
   neighbor 10.0.0.5 bfd
   neighbor 10.0.1.5 remote-as 65000
   neighbor 10.0.1.5 bfd
   neighbor 10.0.255.0 peer group EVPN
   neighbor 10.0.255.1 peer group EVPN
   !
   vlan 100
      rd 65000:100
      route-target import 65000:100
      route-target export 65000:100
      redistribute learned
   !
   address-family evpn
      neighbor EVPN activate
   !
   address-family ipv4
      network 10.0.254.1/32
   !
   vrf EVPNL3
      rd 65000:1
      route-target import evpn 65000:1
      route-target export evpn 65000:1
!
``` 