# LF3
``` 
hostname LF3
!
interface Ethernet1
!
interface Ethernet2
!
interface Ethernet3
!
interface Ethernet4
   description SP0
   no switchport
   ip address 10.0.0.14/30
!
interface Ethernet5
   description SP1
   no switchport
   ip address 10.0.1.14/30
!
interface Ethernet6
!
interface Ethernet7
!
interface Ethernet8
!
interface Loopback0
   ip address 10.0.254.3/32
!
interface Management1
!
ip routing
!
router bgp 65000
   router-id 10.0.254.3
   timers bgp 1 3
   neighbor 10.0.0.13 remote-as 65000
   neighbor 10.0.0.13 bfd
   neighbor 10.0.1.13 remote-as 65000
   neighbor 10.0.1.13 bfd
   network 10.0.254.3/32