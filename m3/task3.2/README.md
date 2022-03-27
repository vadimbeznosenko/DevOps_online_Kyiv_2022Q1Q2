## всё настраивалось с кли попытаюсь описать


## захдим на ISP1

ISP1

## заходим в привилегированный режим

enable

## заходим в режим конфигурации

configure

## заходим в режим конфигурации интерфейса

interface gigabitEthernet 0/0

## назначаем айпишник


ip address 10.88.29.1 255.255.255.0

## включаем интерфейс

no shutdown 

## выходим из режима конфигурации интерфейса


exit 

## заходим в режим конфигурации интерфейса

interface gigabitEthernet 1/0

## назначаем айпишник

ip address 39.8.88.61 255.255.255.192

## включаем интерфейс


no shutdown 

## выходим из режима конфигурации интерфейса


exit 

## заходим в режим конфигурации интерфейса


interface gigabitEthernet 2/0

## назначаем айпишник

ip address 39.8.88.190 255.255.255.192

## включаем интерфейс

no shutdown 

## выходим из режима конфигурации интерфейса, могли бы это сделать через do write memory, но хотел красиво как в книжке

exit

## выходим из режима конфигурации


exit 


## сохраняем текущуу конфигурацию


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

## тут нужно описать, там было все как описовал

enable

## заходим конф

configure

## заходим в интерфейс

interface fastEthernet 0/2

## указываем в каком режиме будет рабоать порт

switchport mode access 

## можно было отдельно создавать влан но можно и он сам создаст
## теперь этой командой говорим что порт будет находится во втором влане

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

## заходим в конф.

configure

## заходим на интерфейс

interface gigabitEthernet 0/0

## удаляем айпишник

no ip address

exit

## теперь создаем под интерфей в интерфейсе

interface gigabitEthernet 0/0.2

## укороченная версия IEEE 802.1q или инкапсуляция указываем что будем работать со вторым выланом

encapsulation dot1Q 2

## назначаем айпишник который будет шлюзом для этого влана


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


![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m3/task3.2/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-02-12%2021-04-21.png)



![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m3/task3.2/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-02-12%2021-05-07.png)

![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m3/task3.2/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-02-12%2021-05-21.png)





