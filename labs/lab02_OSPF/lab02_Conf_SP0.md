# SP0 
``` 
router id 10.0.255.0 
# 
bfd 
# 
interface GE1/0/0 
 undo portswitch 
 description LF0 
 undo shutdown 
 ip address 10.0.0.1 255.255.255.252 
 ospf network-type p2p 
 ospf bfd enable 
 ospf bfd min-tx-interval 100 min-rx-interval 100 
 ospf enable 255 area 0.0.0.0 
# 
interface GE1/0/1 
 undo portswitch 
 description LF1 
 undo shutdown 
 ip address 10.0.0.5 255.255.255.252 
 ospf network-type p2p 
 ospf bfd enable 
 ospf bfd min-tx-interval 100 min-rx-interval 100 
 ospf enable 255 area 0.0.0.0 
# 
interface GE1/0/2 
 undo portswitch 
 description LF2 
 undo shutdown 
 ip address 10.0.0.9 255.255.255.252 
 ospf network-type p2p 
 ospf bfd enable 
 ospf bfd min-tx-interval 100 min-rx-interval 100 
 ospf enable 255 area 0.0.0.0 
# 
interface GE1/0/3 
 undo portswitch 
 description LF3 
 undo shutdown 
 ip address 10.0.0.13 255.255.255.252 
 ospf network-type p2p 
 ospf bfd enable 
 ospf bfd min-tx-interval 100 min-rx-interval 100 
 ospf enable 255 area 0.0.0.0 
# 
interface LoopBack0 
 ip address 10.0.255.0 255.255.255.255 
 ospf enable 255 area 0.0.0.0 
# 
interface NULL0 
# 
ospf 255 
 area 0.0.0.0 
``` 