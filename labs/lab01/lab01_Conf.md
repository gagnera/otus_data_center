# Configs

### SP0
``` 
interface GE1/0/0
 undo portswitch
 description LF0
 undo shutdown
 ip address 10.0.0.1 255.255.255.252

interface GE1/0/1
 undo portswitch
 description LF1
 undo shutdown
 ip address 10.0.0.5 255.255.255.252

interface GE1/0/2
 undo portswitch
 description LF2
 undo shutdown
 ip address 10.0.0.9 255.255.255.252

interface GE1/0/3
 undo portswitch
 description LF3
 undo shutdown
 ip address 10.0.0.13 255.255.255.252
 
interface LoopBack0
 ip address 10.0.255.0 255.255.255.255 
```
### SP1
```
interface GE1/0/0
 undo portswitch
 description LF1
 undo shutdown
 ip address 10.0.1.5 255.255.255.252

interface GE1/0/1
 undo portswitch
 description LF0
 undo shutdown
 ip address 10.0.1.1 255.255.255.252

interface GE1/0/2
 undo portswitch
 description LF3
 undo shutdown
 ip address 10.0.1.13 255.255.255.252

interface GE1/0/3
 undo portswitch
 description LF2
 undo shutdown
 ip address 10.0.1.9 255.255.255.252

interface LoopBack0
 ip address 10.0.255.1 255.255.255.255
```
 ### LF0
 ```
 interface GE1/0/0
 undo portswitch
 description SP0
 undo shutdown
 ip address 10.0.0.2 255.255.255.252

interface GE1/0/1
 undo portswitch
 description SP1
 undo shutdown
 ip address 10.0.1.2 255.255.255.252

interface LoopBack0
 ip address 10.0.254.0 255.255.255.255
```
  ### LF1
  ```
interface GE1/0/0
 undo portswitch
 description SP1
 undo shutdown
 ip address 10.0.1.6 255.255.255.252

interface GE1/0/1
 undo portswitch
 description SP0
 undo shutdown
 ip address 10.0.0.6 255.255.255.252

interface LoopBack0
 ip address 10.0.254.1 255.255.255.255
```
### LF2
```
 interface GE1/0/2
 undo portswitch
 description SP0
 undo shutdown
 ip address 10.0.0.10 255.255.255.252

interface GE1/0/3
 undo portswitch
 description SP1
 undo shutdown
 ip address 10.0.1.10 255.255.255.252

interface LoopBack0
 ip address 10.0.254.2 255.255.255.255
```
 ### LF3
 ```
 interface GE1/0/2
 undo portswitch
 description SP1
 undo shutdown
 ip address 10.0.1.14 255.255.255.252

interface GE1/0/3
 undo portswitch
 description SP0
 undo shutdown
 ip address 10.0.0.14 255.255.255.252

interface LoopBack0
 ip address 10.0.254.3 255.255.255.255