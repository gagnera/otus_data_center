# LF1
``` 
router id 10.0.254.1
#
bfd
#
interface GE1/0/0 
 undo portswitch
 description SP1 
 undo shutdown
 ip address 10.0.1.6 255.255.255.252 
 ospf network-type p2p
 ospf bfd enable 
 ospf bfd min-tx-interval 100 min-rx-interval 100
 ospf enable 255 area 0.0.0.0#
#
interface GE1/0/1 
 undo portswitch
 description SP0 
 undo shutdown
 ip address 10.0.0.6 255.255.255.252 
 ospf network-type p2p
 ospf bfd enable 
 ospf bfd min-tx-interval 100 min-rx-interval 100
 ospf enable 255 area 0.0.0.0#
#
interface LoopBack0 
 ip address 10.0.254.1 255.255.255.255
 ospf enable 255 area 0.0.0.0#
#
ospf 255 
 area 0.0.0.0
``` 