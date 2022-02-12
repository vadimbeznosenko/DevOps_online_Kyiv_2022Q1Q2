
ISP1


enable

configure

interface gigabitEthernet 0/0

ip address 10.88.29.1 255.255.255.0

no shutdown 

exit 

interface gigabitEthernet 1/0

ip address 39.8.88.61 255.255.255.192

no shutdown 

exit 

interface gigabitEthernet 2/0

ip address 39.8.88.190 255.255.255.192

no shutdown 

exit

exit 

write memory 


ISP2


enable

configure

interface gigabitEthernet 1/0

ip address 39.8.88.62 255.255.255.192

no shutdown 

exit 

interface gigabitEthernet 0/0

ip address 39.8.88.254 255.255.255.192

no shutdown 

exit 

interface gigabitEthernet 3/0

ip address 39.8.88.125 255.255.255.192

no shutdown 

exit 

exit

write memory 

ISP3

enable

configure

interface gigabitEthernet 0/0

ip address 8.29.88.1 255.255.255.0

no shutdown 

exit 

interface gigabitEthernet 3/0

ip address 39.8.88.126 255.255.255.192

no shutdown 

exit

interface gigabitEthernet 2/0

ip address 39.8.88.189 255.255.255.192

no shutdown 

exit

exit 

write memory 


Data Center 


enable

configure

interface fastEthernet 0/2

switchport mode access 

switchport access vlan 2

no shutdown 

exit

interface fastEthernet 0/3

switchport mode access 

switchport access vlan 3

exit

interface fastEthernet 0/4

switchport mode access
 
switchport access vlan 4

exit

interface gigabitEthernet 0/1

switchport mode trunk 

switchport trunk allowed vlan 2-4

exit

exit

write memory 



ISP3


configure

interface gigabitEthernet 0/0

no ip address

exit

interface gigabitEthernet 0/0.2

encapsulation dot1Q 2

ip address 8.29.88.1 255.255.255.192

no shutdown 

exit 

interface gigabitEthernet 0/0.3

encapsulation dot1Q 3

ip address 8.29.88.65 255.255.255.192

no shutdown 

exit 

interface gigabitEthernet 0/0.4

encapsulation dot1Q 4

ip address 8.29.88.129 255.255.255.192

no shutdown 

exit

exit

write memory 

