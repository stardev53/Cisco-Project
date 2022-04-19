『 DHCP Configuration 』

```
⇨ Excluding first IP's from DHCP POOL

ip dhcp excluded-address 10.0.15.1
ip dhcp excluded-address 10.1.15.1
ip dhcp excluded-address 10.2.15.1

ip dhcp pool VLAN10
 network 10.0.15.0 255.255.255.0
 default-router 10.0.15.1 
 option 150 ip 10.1.15.1 
 dns-server 8.8.8.8 
ip dhcp pool VLAN20
 network 10.1.15.0 255.255.255.0
 default-router 10.1.15.1 
 option 150 ip 10.1.15.1 
 dns-server 8.8.8.8 
ip dhcp pool VLAN30
 network 10.2.15.0 255.255.255.0
 default-router 10.2.15.1 
 option 150 ip 10.1.15.1 
 dns-server 8.8.8.8
 
```
『 ACL Acess - Lists 』

```
ip nat inside source list 1 interface Serial0/0/0 overload
ip nat inside source list 2 interface Serial0/0/1 overload

access-list 1 permit 10.0.0.0 0.255.255.255
access-list 1 permit 172.16.0.0 0.15.255.255
access-list 1 permit 192.168.0.0 0.0.255.255
access-list 2 permit 10.0.0.0 0.255.255.255
access-list 2 permit 172.16.0.0 0.15.255.255
access-list 2 permit 192.168.0.0 0.0.255.255
```
『 EIGRP | Router EIGRP 100 is related to ALFA and 200 is to BETA | 』

```
router eigrp 100
 network 10.0.15.0 0.0.0.255
 network 10.1.15.0 0.0.0.255
 network 10.2.15.0 0.0.0.255
 network 192.168.15.0 0.0.0.3
 redistribute static
 redistribute eigrp 200
 passive-interface GigabitEthernet0/0
 passive-interface GigabitEthernet0/1


router eigrp 200
 network 10.0.15.0 0.0.0.255
 network 10.1.15.0 0.0.0.255
 network 10.2.15.0 0.0.0.255
 network 192.168.15.4 0.0.0.3
 redistribute static
 redistribute eigrp 100
 passive-interface GigabitEthernet0/0
 passive-interface GigabitEthernet0/1
```
 『 Telephony-services 』
```
telephony-service
 max-ephones 10
 max-dn 10
 ip source-address 10.1.2.1 port 2000
 auto assign 1 to 10
 create cnf-files
 
ephone-dn  1
 number 100
ephone-dn  2
 number 101
ephone-dn  3
 number 102
 
 ```
  『 Virtual Interfaces for VLANS 』
 ```
 interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 10.0.15.1 255.255.255.0
 ip nat inside
 no shut
 exit
interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 10.1.15.1 255.255.255.0
 ip nat inside
 no shut
 exit
interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address 10.2.15.1 255.255.255.0
 ip nat inside
 no shut
 exit
 ```
 『 Tunnel 100 - ENTA TO ALFA 』
 
 ```
 crypto isakmp policy 10
 encr aes 256
 authentication pre-share
 group 5
 lifetime 3600

crypto isakmp key Passw0rd address 1.15.0.2 
crypto ipsec transform-set TRANS ah-sha-hmac esp-aes 256 esp-sha-hmac
 mode tunnel

crypto map OMAPA 10 ipsec-isakmp 
 set peer 1.15.0.2
 set transform-set TRANS 
 match address 101

interface Tunnel100
 ip address 192.168.15.1 255.255.255.252
 tunnel source Serial0/0/0
 tunnel destination 1.15.0.2

interface Serial0/0/0
 ip address 1.15.0.1 255.255.255.252
 ip nat outside
 crypto map OMAPA

access-list 101 permit gre host 1.15.0.1 host 1.15.0.2
 ```
 『 Tunnel 200 - ENTA TO BETA 』
 ```
 crypto isakmp key Passw0rd address 2.15.0.2 
crypto ipsec transform-set TRANS2 ah-sha-hmac esp-aes 256 esp-sha-hmac 
mode tunnel

crypto map MAPA 10 ipsec-isakmp 
 set peer 2.15.0.2
 set transform-set TRANS2 
 match address 100

interface Tunnel200
 ip address 192.168.15.5 255.255.255.252
 tunnel source Serial0/0/1
 tunnel destination 2.15.0.2

interface Serial0/0/1
 ip address 2.15.0.1 255.255.255.252
 ip nat outside
 crypto map MAPA

access-list 100 permit gre host 2.15.0.1 host 2.15.0.2
 ```

 
