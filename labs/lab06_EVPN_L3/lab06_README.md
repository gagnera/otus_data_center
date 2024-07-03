# VxLAN. L3 VNI

### Цель:
Настроить Overlay на основе VxLAN EVPN для L3 связанности между клиентами

### Схема:
![alt text](image.png "Занимательная картинка №1")

### Таблица распределения IP-адресов
| Sysname       | IP                | Desc |
| ------------- |:------------------:| -----:|
| **SP0**     | **10.0.255.0/32**   |**Loop**|
| SP0    | 10.0.0.1/30 |  LF0 |
| SP0  | 10.0.0.5/30        |   LF1|
| SP0  | 10.0.0.9/30        |   LF2 |
| SP0  | 10.0.0.13/30        |   LF3 |
| **SP1**     | **10.0.255.1/32**   |**Loop** |
| SP1    | 10.0.1.1/30 |  LF0 |
| SP1  | 10.0.1.5/30        |   LF1|
| SP1  | 10.0.1.9/30        |   LF2 |
| SP1  | 10.0.1.13/30        |   LF23 |
|    |    |    |
| **VL 100**     | **172.22.1.1**   |**VIP** |
| **VL 200**     | **172.22.2.1**   |**VIP** |
|    |    |    |
| **LF0**     | **10.0.254.0/32**   |**Loop** |
| **LF0**     | **10.0.254.0/32**   |**Loop** |
| LF0  | 10.0.0.2/30        |   SP0|
| LF0  | 10.0.1.2/30        |   SP1 |
| **LF1**    | **10.0.254.1/32**   |**Loop** |
| LF1  | 10.0.0.6/30        |   SP0|
| LF1  | 10.0.1.6/30        |   SP1 |
| **LF2**    | **10.0.254.2/32**   |**Loop** |
| LF2  | 10.0.0.10/30        |   SP0|
| LF2  | 10.0.1.10/30        |   SP1 |
| **LF3**    | **10.0.254.3/32**   |**Loop** |
| LF3  | 10.0.0.14/30        |   SP0|
| LF3  | 10.0.1.14/30        |   SP1 |
| CL00 | 172.22.1.100/24    |   VL 100 |
| CL01 | 172.22.2.200/24    |   VL 200 |
| CL10 | 172.22.1.110/24    |   VL 100 |
| CL20 | 172.22.2.220/24    |   VL 200 |

### Выводы с L2
``` 
LF2#sh ip rou vrf EVPNL3
 B I      172.22.1.100/32 [200/0] via VTEP 10.0.254.0 VNI 1 router-mac 50:00:00:d5:5d:c0 local-interface Vxlan1
 B I      172.22.1.110/32 [200/0] via VTEP 10.0.254.1 VNI 1 router-mac 50:00:00:03:37:66 local-interface Vxlan1
 B I      172.22.2.200/32 [200/0] via VTEP 10.0.254.0 VNI 1 router-mac 50:00:00:d5:5d:c0 local-interface Vxlan1
 C        172.22.2.0/24 is directly connected, Vlan200
``` 
``` 
LF2#sh bgp evpn route-type mac-ip
BGP routing table information for VRF default
Router identifier 10.0.254.2, local AS number 65000
Route status codes: * - valid, > - active, S - Stale, E - ECMP head, e - ECMP
                    c - Contributing to ECMP, % - Pending BGP convergence
Origin codes: i - IGP, e - EGP, ? - incomplete
AS Path Attributes: Or-ID - Originator ID, C-LST - Cluster List, LL Nexthop - Link Local Nexthop

          Network                Next Hop              Metric  LocPref Weight  Path
 * >      RD: 65000:200 mac-ip 5000.002f.d8fe
                                 -                     -       -       0       i
 * >Ec    RD: 65000:200 mac-ip 5000.0045.abdf
                                 10.0.254.0            -       100     0       i Or-ID: 10.0.254.0 C-LST: 10.0.255.0
 *  ec    RD: 65000:200 mac-ip 5000.0045.abdf
                                 10.0.254.0            -       100     0       i Or-ID: 10.0.254.0 C-LST: 10.0.255.1
 * >Ec    RD: 65000:200 mac-ip 5000.0045.abdf 172.22.2.200
                                 10.0.254.0            -       100     0       i Or-ID: 10.0.254.0 C-LST: 10.0.255.0
 *  ec    RD: 65000:200 mac-ip 5000.0045.abdf 172.22.2.200
                                 10.0.254.0            -       100     0       i Or-ID: 10.0.254.0 C-LST: 10.0.255.1
 * >Ec    RD: 65000:100 mac-ip 5000.0088.fe27
                                 10.0.254.0            -       100     0       i Or-ID: 10.0.254.0 C-LST: 10.0.255.0
 *  ec    RD: 65000:100 mac-ip 5000.0088.fe27
                                 10.0.254.0            -       100     0       i Or-ID: 10.0.254.0 C-LST: 10.0.255.1
 * >Ec    RD: 65000:100 mac-ip 5000.0088.fe27 172.22.1.100
                                 10.0.254.0            -       100     0       i Or-ID: 10.0.254.0 C-LST: 10.0.255.0
 *  ec    RD: 65000:100 mac-ip 5000.0088.fe27 172.22.1.100
                                 10.0.254.0            -       100     0       i Or-ID: 10.0.254.0 C-LST: 10.0.255.1
 * >Ec    RD: 65000:100 mac-ip 5000.00ae.f703
                                 10.0.254.1            -       100     0       i Or-ID: 10.0.254.1 C-LST: 10.0.255.0
 *  ec    RD: 65000:100 mac-ip 5000.00ae.f703
                                 10.0.254.1            -       100     0       i Or-ID: 10.0.254.1 C-LST: 10.0.255.1
 * >Ec    RD: 65000:100 mac-ip 5000.00ae.f703 172.22.1.110
                                 10.0.254.1            -       100     0       i Or-ID: 10.0.254.1 C-LST: 10.0.255.0
 *  ec    RD: 65000:100 mac-ip 5000.00ae.f703 172.22.1.110
                                 10.0.254.1            -       100     0       i Or-ID: 10.0.254.1 C-LST: 10.0.255.1
LF2#
``` 
### Торжество пинга состоялось: 
``` 
CL20#ping 172.22.1.100
PING 172.22.1.100 (172.22.1.100) 72(100) bytes of data.

--- 172.22.1.100 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 56ms
rtt min/avg/max/mdev = 76.410/97.573/110.869/11.637 ms, pipe 5, ipg/ewma 14.033/87.387 ms
``` 
``` 
CL20#ping 172.22.1.110

--- 172.22.1.110 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 48ms
rtt min/avg/max/mdev = 84.496/97.384/106.451/9.008 ms, pipe 5, ipg/ewma 12.179/101.162 ms
``` 
``` 
CL20#ping 172.22.2.200

--- 172.22.2.200 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 59ms
rtt min/avg/max/mdev = 124.139/159.695/181.602/21.312 ms, pipe 5, ipg/ewma 14.874/142.788 ms
CL20#