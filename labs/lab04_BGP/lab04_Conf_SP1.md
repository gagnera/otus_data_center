# SP0
``` 
hostname SP0
!
interface Ethernet1
   description LF0
   no switchport
   ip address 10.0.0.1/30
!
interface Ethernet2
   description LF1
   no switchport
   ip address 10.0.0.5/30
!
interface Ethernet3
   description LF2
   no switchport
   ip address 10.0.0.9/30
!
interface Ethernet4
   description LF3
   no switchport
   ip address 10.0.0.13/30
!
interface Ethernet5
!
interface Ethernet6
!
interface Ethernet7
!
interface Ethernet8
!
interface Loopback0
   ip address 10.0.255.0/32
!
interface Management1
!
ip routing
!
router bgp 65000
   router-id 10.0.255.0
   timers bgp 1 3
   bgp listen range 10.0.0.0/24 peer-group LEAF remote-as 65000
   neighbor LEAF peer group
   neighbor LEAF bfd
   neighbor LEAF route-reflector-client
   network 10.0.255.0/32
   redistribute connected