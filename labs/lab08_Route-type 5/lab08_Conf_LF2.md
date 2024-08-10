# LF2
``` 
hostname LF2
!
spanning-tree mode mstp
no spanning-tree vlan-id 4094
!
vlan 200
!
vlan 4094
   trunk group m1peer
!
vrf instance EVPNL3
!
interface Port-Channel10
   switchport mode trunk
   switchport trunk group m1peer
!
interface Port-Channel20
   description CL20
   switchport access vlan 200
   switchport trunk allowed vlan 200
   switchport mode trunk
   mlag 20
!
interface Ethernet1
!
interface Ethernet2
!
interface Ethernet3
   description SP0
   no switchport
   ip address 10.0.0.10/30
!
interface Ethernet4
   description SP1
   no switchport
   ip address 10.0.1.10/30
!
interface Ethernet5
!
interface Ethernet6
   channel-group 10 mode active
!
interface Ethernet7
   channel-group 10 mode active
!
interface Ethernet8
   description CL20
   channel-group 20 mode active
!
interface Loopback0
   ip address 10.0.254.2/32
!
interface Management1
!
interface Vlan200
   description RED_VLAN
   vrf EVPNL3
   ip address virtual 172.22.2.1/24
!
interface Vlan4094
   no autostate
   ip address 192.168.0.1/30
!
interface Vxlan1
   vxlan source-interface Loopback0
   vxlan udp-port 4789
   vxlan vlan 200 vni 200
   vxlan vrf EVPNL3 vni 1
   vxlan learn-restrict any
!
ip routing
ip routing vrf EVPNL3
!
mlag configuration
   domain-id mlag
   heartbeat-interval 2500
   local-interface Vlan4094
   peer-address 192.168.0.2
   peer-link Port-Channel10
!
router bgp 65000
   router-id 10.0.254.2
   timers bgp 1 3
   maximum-paths 2
   neighbor EVPN peer group
   neighbor EVPN remote-as 65000
   neighbor EVPN update-source Loopback0
   neighbor EVPN send-community extended
   neighbor 10.0.0.9 remote-as 65000
   neighbor 10.0.0.9 bfd
   neighbor 10.0.1.9 remote-as 65000
   neighbor 10.0.1.9 bfd
   neighbor 10.0.255.0 peer group EVPN
   neighbor 10.0.255.1 peer group EVPN
   !
   vlan 200
      rd 65000:200
      route-target import 65000:200
      route-target export 65000:200
      redistribute learned
   !
   address-family evpn
      neighbor EVPN activate
   !
   address-family ipv4
      network 10.0.253.2/32
      network 10.0.254.2/32
   !
   vrf EVPNL3
      rd 65000:1
      route-target import evpn 65000:1
      route-target export evpn 65000:1
      redistribute connected
!
end