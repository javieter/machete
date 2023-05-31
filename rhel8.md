# RHEL 8

## Gestión de redes
### Ver todas las interfaces de red
    # ip a
### Ver detalle de un interface particular
~~~
[folmedo@rhel ~]$ ip a s ens224
2: ens224: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:50:56:86:41:0a brd ff:ff:ff:ff:ff:ff
    inet 10.1.2.42/16 brd 10.1.255.255 scope global noprefixroute ens224
       valid_lft forever preferred_lft forever
[folmedo@rhel ~]$ 
~~~
### Ver estadísticas sobre rendimiento de la red
~~~
[folmedo@rhel ~]$ ip -s link show ens224
2: ens224: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 00:50:56:86:41:0a brd ff:ff:ff:ff:ff:ff
    RX: bytes  packets  errors  dropped overrun mcast   
    148980594088 1172670999 0       861334  0       58887   
    TX: bytes  packets  errors  dropped carrier collsns 
    189188779596 77715243 0       0       0       0       
[folmedo@rhel ~]$ 

~~~

### Ver nombre de servicio, protocolo y puerto por defecto
~~~
[folmedo@rhel ~]$ cat /etc/services |grep -v "#"|grep .  |head
echo            7/tcp
echo            7/udp
discard         9/tcp           sink null
discard         9/udp           sink null
systat          11/tcp          users
systat          11/udp          users
daytime         13/tcp
daytime         13/udp
qotd            17/tcp          quote
qotd            17/udp          quote
[folmedo@rhel ~]$ 
~~~

### Ver estadísticas de sockets
~~~
[folmedo@rhel ~]$ netstat -natupe
(No info could be read for "-p": geteuid()=1676 but you should be root.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       User       Inode      PID/Program name    
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      0          22859      -                   
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      0          17125      -                   
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      0          325716477  -                   
tcp        0      0 10.1.2.42:45632         10.1.1.238:22           ESTABLISHED 10008      289918781  -                   
tcp        0      0 10.1.2.42:45652         10.1.1.238:22           ESTABLISHED 10008      289919909  -                   
tcp        0      0 10.1.2.42:45598         10.1.1.238:22           ESTABLISHED 10008      289919411  -                   
tcp        0      0 10.1.2.42:22            10.64.7.182:34838       ESTABLISHED 0          536163271  -                   
tcp        0      0 10.1.2.42:33318         10.7.25.101:22          ESTABLISHED 10008      453587773  -                   
tcp        0      0 10.1.2.42:45522         10.1.1.238:22           ESTABLISHED 10008      289917747  -                   
tcp6       0      0 :::443                  :::*                    LISTEN      0          11064091   -                   
tcp6       0      0 :::111                  :::*                    LISTEN      0          17128      -                   
tcp6       0      0 :::80                   :::*                    LISTEN      0          11090769   -                   
tcp6       0      0 :::8080                 :::*                    LISTEN      0          11064070   -                   
tcp6       0      0 :::81                   :::*                    LISTEN      0          11064424   -                   
tcp6       0      0 :::22                   :::*                    LISTEN      0          325716479  -                   
udp        0      0 0.0.0.0:111             0.0.0.0:*                           0          17123      -                   
udp        0      0 127.0.0.1:323           0.0.0.0:*                           0          18210      -                   
udp        0      0 0.0.0.0:903             0.0.0.0:*                           0          17124      -                   
udp        0      0 0.0.0.0:58934           0.0.0.0:*                           0          23750      -                   
udp        0      0 0.0.0.0:35051           0.0.0.0:*                           0          23747      -                   
udp6       0      0 :::111                  :::*                                0          17126      -                   
udp6       0      0 ::1:323                 :::*                                0          18211      -                   
udp6       0      0 :::903                  :::*                                0          17127      -                   
[folmedo@rhel ~]$ ss -natupe
Netid  State      Recv-Q Send-Q                          Local Address:Port                                         Peer Address:Port              
udp    UNCONN     0      0                                           *:111                                                     *:*                   ino:17123 sk:ffff9fe16e6f8cc0 <->
udp    UNCONN     0      0                                   127.0.0.1:323                                                     *:*                   ino:18210 sk:ffff9fe168670000 <->
udp    UNCONN     0      0                                           *:903                                                     *:*                   ino:17124 sk:ffff9fe16e6f9100 <->
udp    UNCONN     0      0                                           *:58934                                                   *:*                   ino:23750 sk:ffff9fe168672200 <->
udp    UNCONN     0      0                                           *:35051                                                   *:*                   ino:23747 sk:ffff9fe168671540 <->
udp    UNCONN     0      0                                        [::]:111                                                  [::]:*                   ino:17126 sk:ffff9fe16aac0000 v6only:1 <->
udp    UNCONN     0      0                                       [::1]:323                                                  [::]:*                   ino:18211 sk:ffff9fe16a8a0000 v6only:1 <->
udp    UNCONN     0      0                                        [::]:903                                                  [::]:*                   ino:17127 sk:ffff9fe16aac04c0 v6only:1 <->
tcp    LISTEN     0      100                                 127.0.0.1:25                                                      *:*                   ino:22859 sk:ffff9fe16a838f80 <->
tcp    LISTEN     0      128                                         *:111                                                     *:*                   ino:17125 sk:ffff9fe16a838000 <->
tcp    LISTEN     0      128                                         *:22                                                      *:*                   ino:325716477 sk:ffff9fe16a83be00 <->
tcp    ESTAB      0      0                                   10.1.2.42:45632                                          10.1.1.238:22                  timer:(keepalive,19min,0) uid:10008 ino:289918781 sk:ffff9fddd7dab640 <->
tcp    ESTAB      0      0                                   10.1.2.42:45652                                          10.1.1.238:22                  timer:(keepalive,21min,0) uid:10008 ino:289919909 sk:ffff9fe169cbc5c0 <->
tcp    ESTAB      0      0                                   10.1.2.42:45598                                          10.1.1.238:22                  timer:(keepalive,22min,0) uid:10008 ino:289919411 sk:ffff9fe16afe1f00 <->
tcp    ESTAB      0      0                                   10.1.2.42:22                                            10.64.7.182:34838               timer:(keepalive,84min,0) ino:536163271 sk:ffff9fe070b8e4c0 <->
tcp    ESTAB      0      0                                   10.1.2.42:33318                                         10.7.25.101:22                  timer:(keepalive,101min,0) uid:10008 ino:453587773 sk:ffff9fe0dbc9e4c0 <->
tcp    ESTAB      0      0                                   10.1.2.42:45522                                          10.1.1.238:22                  timer:(keepalive,11min,0) uid:10008 ino:289917747 sk:ffff9fe16afe4d80 <->
tcp    LISTEN     0      128                                      [::]:443                                                  [::]:*                   ino:11064091 sk:ffff9fe16aac98c0 v6only:0 <->
tcp    LISTEN     0      128                                      [::]:111                                                  [::]:*                   ino:17128 sk:ffff9fe16aac8000 v6only:1 <->
tcp    LISTEN     0      128                                      [::]:80                                                   [::]:*                   ino:11090769 sk:ffff9fe16c20eb40 v6only:0 <->
tcp    LISTEN     0      128                                      [::]:8080                                                 [::]:*                   ino:11064070 sk:ffff9fe16aaca100 v6only:0 <->
tcp    LISTEN     0      128                                      [::]:81                                                   [::]:*                   ino:11064424 sk:ffff9fe16c209080 v6only:0 <->
tcp    LISTEN     0      128                                      [::]:22                                                   [::]:*                   ino:325716479 sk:ffff9fe16c20dac0 v6only:1 <->
[folmedo@rhel ~]$
~~~