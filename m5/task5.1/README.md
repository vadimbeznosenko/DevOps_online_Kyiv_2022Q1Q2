![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m5/task5.1/4.png)

схема была сделана в прогрме GNS3

1)для сервера был выбран Centos7, потому для настройки интерфейсов заходим в /etc/sysconfig/network-scripts/ или же пользуемся nmtui
так как интерфейс enp0s3 смотрит на DHCP сервер ещё по бестпрактису прибиваем его по маку на сервере который раздает адресса, поскольку при долгом отключении этот адресс может быть уже занятым другим устройством
![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m5/task5.1/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-04-09%2016-34-09.png)


![image](https://user-images.githubusercontent.com/87521485/162885537-88afb884-58e9-472e-96bb-83eb08f8f0f1.png)


2) в конфиге данного сервиса видно что клиенские машинки были прибиты по мак адрессам и далее на скрине видно на ках интерфейсах он рботает, так как без кешироещего DNSа никуда, был выбран ещё Unbound, настройки прилагаются
![image](https://user-images.githubusercontent.com/87521485/162885676-77882372-3c45-461c-9ccb-d7e573ab8d58.png)
![image](https://user-images.githubusercontent.com/87521485/162885773-63c7058f-c1b1-47f0-a741-0f903cf87c85.png)
![image](https://user-images.githubusercontent.com/87521485/162885810-d786e463-0520-47dd-8001-616a028fd6b8.png)


3) маршрута нету и связи между ними тоже нету, можно пинганут только шлюзы на сервере

на следующем скирне виден домашний роутер с маршрутом, проверено mtr так как эта утилита и делает трасировку и пингует
![image](https://user-images.githubusercontent.com/87521485/162885930-10d24103-afa6-4ee3-b2cb-8b6810e820cd.png)
![image](https://user-images.githubusercontent.com/87521485/162885981-2cfba281-5bd4-4d88-bffd-022efb3110a4.png)

и не забываем включить на сервере следующее

echo 1 > /proc/sys/net/ipv4/ip_forward

4)на скрне все показано 
![image](https://user-images.githubusercontent.com/87521485/162886179-43dfbe19-7d4f-4edc-a34d-036d2486908d.png)

тут просто делам маршруты

sudo ip route add 172.17.49.0/24 via 172.16.29.1

sudo ip route add 172.17.39.0/24 via 10.8.88.1

5)
sudo ip route del 172.17.49.0/24 via 172.16.29.1

sudo ip route del 172.17.39.0/24 via 10.8.88.1

sudo ip route add 172.17.0.0/16 via 10.8.88.1

6) на скрине видно что клиент может подключатся к серверу по адрессу шлюза 10.8.88.1 и на адресс клиента1 172.16.29.1, на клаент2 работает по тому же принцепу это тахнология называется джамплик и так делаются бастионхосты в AWS
![image](https://user-images.githubusercontent.com/87521485/162886263-5c77ca39-9348-4765-b582-2cf8023fb828.png)



7) на сервере просто блокирум подсеть клиента2 для порта ssh, лучше делать именно REJECT поскольку если сервер будет повергаться атакам, то атакующея сторона будет думать что там ничего нету

iptables -I INPUT -s 10.8.88.0/24 -p tcp --dport ssh -j REJECT

на клиенте1 принцеп похож как с портом ssh

iptables -I INPUT -s 172.17.49.1/24 -p icmp -j REJECT

8) зашли на роутер и выключили маршрут


на  сервере прописали следующее

iptables -t nat -A POSTROUTING -o enp0s3 -s 10.8.88.0/24 -j MASQUERADE

iptables -t nat -A POSTROUTING -o enp0s3 -s 10.88.29.0/24 -j MASQUERADE
