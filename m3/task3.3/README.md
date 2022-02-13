ISP1


enable
configure
interface gigabitEthernet 0/0
ip address 10.99.25.1 255.255.255.0
no shutdown 
exit
interface gigabitEthernet 1/0
ip address 35.4.99.1 255.255.255.192
no shutdown 
exit
interface gigabitEthernet 2/0
ip address 35.4.99.65 255.255.255.192
no shutdown 
exit
exit
write memory 



ISP2


enable
configure
interface gigabitEthernet 0/0
ip address 35.4.99.194 255.255.255.192
no shutdown 
exit
interface gigabitEthernet 1/0
ip address 35.4.99.2 255.255.255.192
no shutdown 
exit
interface gigabitEthernet 3/0
ip address 35.4.99.129 255.255.255.192
no shutdown 
exit
exit
write memory 



ISP3


configure
interface gigabitEthernet 3/0
ip address 35.4.99.130 255.255.255.192
no shutdown 
exit
interface gigabitEthernet 2/0
ip address 35.4.99.66 255.255.255.192
no shutdown 
exit 
interface gigabitEthernet 0/0
ip address 4.25.99.1 255.255.255.0
no shutdown
exit
exit
write memory 


ISP2

configure
ip route 10.99.25.0 255.255.255.0 35.4.99.1
ip route 4.25.99.0 255.255.255.0 35.4.99.130


ISP1


configure
ip route 35.4.99.192 255.255.255.192 35.4.99.2
ip route 4.25.99.0 255.255.255.0 35.4.99.66
exit
write


ISP3


configure
ip route 10.99.25.0 255.255.255.0 35.4.99.65
ip route 35.4.99.192 255.255.255.192 35.4.99.129
exit
write


ISP1
configure
no ip route 35.4.99.192 255.255.255.192 35.4.99.2
no ip route 4.25.99.0 255.255.255.0 35.4.99.66
router rip
version 2
network 10.99.25.0 
network 35.4.99.0
network 35.4.99.64
exit
exit
show ip rip database 
write memory 


ISP3

no ip route 10.99.25.0 255.255.255.0 35.4.99.65
no ip route 35.4.99.192 255.255.255.192 35.4.99.129
router rip 
version 2
network 4.25.99.0
network 35.4.99.64
network 35.4.99.128
exit
exit
write memory 
show ip rip database 


ISP2


enable
configure

no ip 4.25.99.0 255.255.255.0 35.4.99.130
no ip route 4.25.99.0 255.255.255.0 35.4.99.130
no ip route 10.99.25.0 255.255.255.0 35.4.99.1
router rip 
version 2
network 35.4.99.192
network 35.4.99.0
network 35.4.99.128
exit
exit
show ip rip database 
show ip rip database 



