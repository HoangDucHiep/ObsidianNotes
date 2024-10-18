---
title: Config IP Router
tags:
  - Mạng-Máy-Tính
---
- Config ip cho các cổng:
``` shell
R-UTC>
R-UTC>en
R-UTC>en
R-UTC>enable
R-UTC#conf
R-UTC#conf terminal
Enter configuration commands, one per line. End with CNTL/Z.
R-UTC(config)#inter
R-UTC(config)#interface f
R-UTC(config)#interface fastEthernet 0/0
R-UTC(config-if)#ip ad
R-UTC(config-if)#ip address 99.100.31.1 255.255.255.0
R-UTC(config-if)#ipv6 ad
R-UTC(config-if)#ipv6 address A1B3:4E1C::1/64
R-UTC(config-if)#no shu
R-UTC(config-if)#no shutdown
```
