# LF1
``` 
hostname LF1
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
!
interface Loopback0
   ip address 10.0.254.1/32
!
interface Management1
!
ip routing
!
router bgp 65000
   router-id 10.0.254.1
   timers bgp 1 3
   neighbor 10.0.0.5 remote-as 65000
   neighbor 10.0.0.5 bfd
   neighbor 10.0.1.5 remote-as 65000
   neighbor 10.0.1.5 bfd
   network 10.0.254.1/32