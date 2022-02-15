

ISP1

## заходим в привилегированный режим

enable

## заходим в режим конфигурации

configure

## заходим в интерфейс 

interface gigabitEthernet 0/0

## назначаем адресс


ip address 10.99.25.1 255.255.255.0

## включаем интерфейс


no shutdown 

## выходим  из интерфейса 


exit

## заходим в интерфейс

interface gigabitEthernet 1/0

## назначаем адресс


ip address 35.4.99.1 255.255.255.192

## включаем интерфейс

no shutdown 

## выходим  из интерфейса 

exit

## заходим в интерфейс

interface gigabitEthernet 2/0


## назначаем адресс

ip address 35.4.99.65 255.255.255.192

## включаем интерфейс

no shutdown 

## выходим  из интерфейса 

exit

## выходим из режима конфигурации


exit

## сохраняем текущую конфигурацию


write memory 

## всё тоже самое проделываем на другом и третьем маршрутизаторе, но с другими айпи адрессами

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




## теперь на втором маршрутизаторе настраиваем маршруты

ISP2

configure

## настройкам маршрутов с учетом следующего прыжка

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




## теперь чтобы настроить динамическую маршрутизацию нужно удалить статику

ISP1

configure

## команда no говорить что нужно удалить даную конфигурацию

no ip route 35.4.99.192 255.255.255.192 35.4.99.2

no ip route 4.25.99.0 255.255.255.0 35.4.99.66



## теперь заходи в конфигурацию динамической маршрутизации rip

router rip


## говорим на какой версии он будет работать

version 2

## обьявляем сеточки о которых знает маршрутизатор

network 10.99.25.0 

network 35.4.99.0

network 35.4.99.64

exit

exit

## показывает информацию, содержащуюся в базе данных RIP

show ip rip database 


## сохраняем текущую конфигурацию

write memory 


## всё тоже проделываем на третьем и первом маршрутизаторе только с другими параметрами


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


![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m3/task3.3/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-02-13%2021-06-35.png)

![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m3/task3.3/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-02-13%2020-53-12.png)

![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m3/task3.3/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-02-13%2021-06-18.png)



