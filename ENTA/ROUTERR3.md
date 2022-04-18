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
