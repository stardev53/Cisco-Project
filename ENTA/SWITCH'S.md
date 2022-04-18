『 SW7 』
```
spanning-tree vlan 10 priority primary
spanning-tree vlan 20 priority secundary

interface Port-channel1
 switchport mode trunk

interface FastEthernet0/3
 switchport mode trunk

interface FastEthernet0/4
 switchport mode trunk

interface FastEthernet0/11
 switchport mode trunk
 channel-protocol lacp
 channel-group 1 mode active

interface FastEthernet0/12
 switchport mode trunk
 channel-protocol lacp
 channel-group 1 mode active
 
interface FastEthernet0/15
 switchport mode trunk
```
『 SW9 』
```
spanning-tree vlan 20 priority secundary
spanning-tree vlan 30 priority primary

interface Port-channel1
 switchport mode trunk

interface FastEthernet0/11
 switchport mode trunk
 channel-protocol lacp
 channel-group 1 mode active

interface FastEthernet0/12
 switchport mode trunk
 channel-protocol lacp
 channel-group 1 mode active
         
interface FastEthernet0/13
 switchport mode trunk
```
『 SW11 | Vlan20 is for VO-IP 』
```
spanning-tree vlan 30 priority secundary

interface Port-channel2
 switchport mode trunk
 
interface FastEthernet0/4
 switchport access vlan 30
 switchport mode access
 
 interface FastEthernet0/5
 switchport mode access
 switchport voice vlan 20
 mls qos trust cos
 spanning-tree portfast

interface FastEthernet0/11
 switchport mode trunk
 channel-protocol lacp
 channel-group 2 mode active
         
interface FastEthernet0/12
 switchport mode trunk
 channel-protocol lacp
 channel-group 2 mode active

interface FastEthernet0/13
 switchport mode trunk
 ```
 『 SW14 』
  ```
 interface Port-channel2
 switchport mode trunk

interface FastEthernet0/4
 switchport access vlan 10
 switchport mode access

interface FastEthernet0/11
 switchport mode trunk
 channel-protocol lacp
 channel-group 2 mode active

interface FastEthernet0/12
 switchport mode trunk
 channel-protocol lacp
 channel-group 2 mode active
 
interface FastEthernet0/15
 switchport mode trunk
  ```
