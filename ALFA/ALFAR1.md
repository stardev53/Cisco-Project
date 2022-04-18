『 ACL 』
```
access-list 1 permit 10.0.0.0 0.255.255.255
access-list 1 permit 172.16.0.0 0.15.255.255
access-list 1 permit 192.168.0.0 0.0.255.255

ip nat inside source list 1 interface Serial0/1/1 overload
ip nat inside source static tcp 172.17.15.2 80 1.15.0.2 80 
ip nat inside source static tcp 172.17.15.2 443 1.15.0.2 443

ip route 172.17.15.0 255.255.255.0 172.16.15.2 
ip route 172.18.15.0 255.255.255.0 172.16.15.2

access-list 100 permit tcp any any eq www
access-list 100 permit tcp any any eq 443
access-list 100 permit ip any 1.15.0.0 0.0.0.3
```
『 EIGRP 100 』
```
router eigrp 100
 network 172.16.15.0 0.0.0.255
 network 172.17.15.0 0.0.0.255
 network 172.18.15.0 0.0.0.255
 network 192.168.15.0 0.0.0.3
 redistribute static
 passive-interface FastEthernet0/0
```
『 Interfaces 』
```
interface FastEthernet0/0
 ip address 172.16.15.1 255.255.255.0
 ip nat inside
 no shut

interface Serial0/1/1
 ip address 1.15.0.2 255.255.255.252
 ip nat outside
 clock rate 125000
 crypto map OMAPA
 no shut
```
『 Tunnel100 | ALFA TO ENTA | 』
```
crypto isakmp policy 10
 encr aes 256
 authentication pre-share
 group 5
 lifetime 3600

crypto isakmp key Passw0rd address 1.15.0.1
crypto ipsec transform-set TRANS ah-sha-hmac esp-aes 256 esp-sha-hmac 

crypto map OMAPA 10 ipsec-isakmp 
 set peer 1.15.0.1
 set transform-set TRANS 
 match address 100

interface Tunnel100
 ip address 192.168.15.2 255.255.255.252
 tunnel source Serial0/1/1
 tunnel destination 1.15.0.1

interface Serial0/1/1
 ip address 1.15.0.2 255.255.255.252
 ip nat outside
 crypto map OMAPA

access-list 100 permit gre host 1.15.0.2 host 1.15.0.1
```
