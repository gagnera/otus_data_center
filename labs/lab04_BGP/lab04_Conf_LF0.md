# LF0
``` 
hostname LF0
!
interface Ethernet1
   description SP0
   no switchport
   ip address 10.0.0.2/30
!
interface Ethernet2
   description SP1
   no switchport
   ip address 10.0.1.2/30
!
interface Ethernet3
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
   ip address 10.0.254.0/32
!
interface Management1
!
ip routing
!
router bgp 65000
   router-id 10.0.254.0
   timers bgp 1 3
   neighbor 10.0.0.1 remote-as 65000
   neighbor 10.0.0.1 bfd
   neighbor 10.0.1.1 remote-as 65000
   neighbor 10.0.1.1 bfd
   network 10.0.254.0/32