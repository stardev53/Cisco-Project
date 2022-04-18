『 DHCP Configuration 』

```
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