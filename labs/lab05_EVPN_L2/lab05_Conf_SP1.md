# SP1
``` 
hostname SP1
!
interface Ethernet1
!
interface Ethernet2
   description LF0
   no switchport
   ip address 10.0.1.1/30
!
interface Ethernet3
   description LF1
   no switchport
   ip address 10.0.1.5/30
!
interface Ethernet4
   description LF2
   no switchport
   ip address 10.0.1.9/30
!
interface Ethernet5
   description LF3
   no switchport
   ip address 10.0.1.13/30
!
interface Ethernet6
!
interface Ethernet7
!
interface Ethernet8
!
interface Loopback0
   ip address 10.0.255.1/32
!
interface Management1
!
ip routing
!
router bgp 65000
   router-id 10.0.255.1
   timers bgp 1 3
   bgp listen range 10.0.254.0/24 peer-group EVPN remote-as 65000
   bgp listen range 10.0.1.0/24 peer-group LEAF remote-as 65000
   neighbor EVPN peer group
   neighbor EVPN update-source Loopback0
   neighbor EVPN route-reflector-client
   neighbor EVPN send-community extended
   neighbor LEAF peer group
   neighbor LEAF bfd
   neighbor LEAF route-reflector-client
   redistribute connected
   !
   address-family evpn
      neighbor EVPN activate
   !
   address-family ipv4
      network 10.0.255.1/32
