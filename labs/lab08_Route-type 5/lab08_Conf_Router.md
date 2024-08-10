# Router
``` 
 sysname Router
#
interface GE1/0/0
 undo portswitch
 description LF0
 undo shutdown
 ip address 10.0.255.254 255.255.255.252
#
interface LoopBack0
 ip address 1.1.1.1 255.255.255.255
#
interface NULL0
#
bgp 65001
 router-id 10.0.255.254
 peer 10.0.255.253 as-number 65000
 #
 ipv4-family unicast
  network 1.1.1.1 255.255.255.255
  peer 10.0.255.253 enable
