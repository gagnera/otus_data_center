# LF0
``` 
sysname LF0
#
bfd
#
isis 255
 network-entity 49.1000.0025.4000.00
#
interface GE1/0/0
 undo portswitch
 description SP0
 undo shutdown
 ip address 10.0.0.2 255.255.255.252
 isis enable 255
 isis circuit-type p2p
 isis circuit-level level-1
 isis authentication-mode hmac-sha256 key-id 255 cipher %^%#\Mi6+n&x!KfkVf>#2Z)Cp0RN3W9AaS!-xFBS)N1N%^%#
 isis bfd enable
 isis bfd min-tx-interval 100 min-rx-interval 100
 #
interface GE1/0/1
 undo portswitch
 description SP1
 undo shutdown
 ip address 10.0.1.2 255.255.255.252
 isis enable 255
 isis circuit-type p2p
 isis circuit-level level-1
 isis authentication-mode hmac-sha256 key-id 255 cipher %^%#\Mi6+n&x!KfkVf>#2Z)Cp0RN3W9AaS!-xFBS)N1N%^%#
 isis bfd enable
 isis bfd min-tx-interval 100 min-rx-interval 100
#
interface LoopBack0
 ip address 10.0.254.0 255.255.255.255
 isis enable 255