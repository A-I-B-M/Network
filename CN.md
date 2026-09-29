### DHCP 

ip dhcp pool R2G0/0

network 192.168.1.0 255.255.255.0

default-router 192.168.1.1

dns-server 8.8.8.8

ip dhcp excluded-address 192.168.1.1 192.168.1.10             R2# show ip dhcp pool



### ACL

**1. OUT — DENY ONE HOST/PC**

Router(config)# access-list 4 deny host 192.168.1.2

Router(config)# access-list 4 permit any

Router(config)# interface g0/1

Router(config-if)# ip access-group 4 out



**2. NETWORK BLOCK — DENY WHOLE NETWORK**

Router(config)# access-list 5 deny 192.168.1.0 0.0.0.255

Router(config)# access-list 5 permit any

Router(config)# interface g0/1

Router(config-if)# ip access-group 5 out



**3. IN — DENY ONE HOST/PC**

Router(config)# access-list 6 deny host 192.168.1.2

Router(config)# access-list 6 permit any

Router(config)# interface g0/1

Router(config-if)# ip access-group 6 in



### **NAT**

**access-list 1 permit 192.168.1.0 0.0.0.255**

**int g0/0           int g0/1**

ip nat inside     ip nat outside



ip nat inside source list 1 int g0/1 overload

