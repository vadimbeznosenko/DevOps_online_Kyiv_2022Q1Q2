1)

#!/bin/bash

select key --all for see all host in network or --target for see see all open port in network

do
    case $key in
    
    --all)
            eval 'nmap -sL 192.168.0.0/16';;
            
    --target)
            eval 'nmap -p 0-65535 192.168.0.0/16';;
            
    *)      
            echo "good bye" 
            
    esac


2)

awk '{ print $1}' /home/sax/Загрузки/apache_logs.txt| sort | uniq -c | sort -nr | head -n 1

awk {'print $15'} /home/sax/Загрузки/apache_logs.txt |sort|uniq -c|sort -nr|head -n 1

awk '{ print $1}' /home/sax/Загрузки/apache_logs.txt | sort | uniq -c | sort -nr | awk '{ print $1}' | awk 'BEGIN {sum=0} {sum=sum+$1} END {print sum}'

cat /home/sax/Загрузки/apache_logs.txt | grep error404 | awk '{ print $15}'

awk '{ print $4}' /home/sax/Загрузки/apache_logs.txt| sort | uniq -c | sort -nr | head -n 1


3) добавляем в cron и вся дедуплекация, которая нужна в задании, вы же понимаете что в высоконагруженых средах никто так не будет поступать, есть для этого borg, bacula, veeam

и лучше уже переходить на  systemctl status *timer

#!/bin/bash
eval 'rsync -azvh /home/vagrant/source /home/vagrant/dest --log-file=/home/vagrant/log'

