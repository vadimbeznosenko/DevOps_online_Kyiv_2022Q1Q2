1) в убунте в целях безопасности, такая возможность отсутвует или это её нужно включать, там в ссш конф, что не советую делать, а то серваки 
проламливаются на ура, а вот в центосе такой финт с ушами пройдет, но его нужно отключать

sudo useradd -p 123  -s /bin/bash -m -d /home/test test

2)sudo passwd test

-d - удалить пароль пользователя, после этого он не сможет войти

-e - сделать пароль устаревшим

-i - через сколько дней после того, как пароль устарел, отключить аккаунт, если пользователь не сменил пароль

-l - запретить пользователю входить в систему

-n - минимальное количество дней между сменами пароля

-S - отобразить информацию об аккаунте

-u - отменяет действие параметра -l

-x - максимальное количество дней, пока пароль можно использовать.

-w - количество дней, после которых нужно предупреждать пользователя о том, что надо сменить пароль.

sudo cat /etc/shadow

3) vagrant@ubuntu-focal:~$ w

15:02:58 up  1:35,  1 user,  load average: 0.00, 0.00, 0.00

USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT

vagrant  pts/0    10.0.2.2         14:46    0.00s  0.04s  0.00s w

USER – имя учетной записи.

TTY – название терминала.

FROM – имя хоста или IP адрес, с которого пользователь вошел в систему под конкретной учетной записью.

LOGIN – время, когда та или иная учетная запись впервые с момента включения машины зарегистрировалась в системе.

IDLE – время, когда пользователь проявил активность с определенного аккаунта.

JCPU – время, использованное всеми процессами, запущенными в терминале tty.

PCPU – время, использованное текущим процессом (каким именно — можно посмотреть в столбце WHAT).

WHAT – текущие процессы и команды, которыми занят пользователь под конкретной учетной записью.

4)  sudo chfn -f test2 vagrant

sudo chfn -h 0172-666666 vagrant

5) info chfn
   
   man chfn
   
   info passwd
   
   man passwd
   
   info w
	
   sudo passwd vagrant -I
   
   sudo passwd vagrant -e
   
   sudo chfn -w 0172-666666 vagrant
   
   -w, --work-phone WORK_PHONE
   
    Change the user's office phone number
		   
   sudo chfn -h 0172-666666 vagrant
   
   -h, --home-phone HOME_PHONE
   
    Change the user's home phone number
   
   w -h
   
   -h (--no-header) — отказ от вывода заголовков
   
   w -s
   
   -s (--short) — краткий формат вывода
   
6) man more 
   
   man less
   
   more /home/vagrant/.bash_history 
   
   more /home/vagrant/.bash_logout 
   
   more /home/vagrant/.bashrc 
   
   less /home/vagrant/.bashrc 
   
   less /home/vagrant/.bash_logout 
   
   less /home/vagrant/.bash_history 
 
 7) grep "x:[0-1]...:[1000-65533]" /etc/passwd | cut -d: -f1 | finger -s
 
 8) vagrant@ubuntu-focal:~$ ls /home/vagrant/

vagrant@ubuntu-focal:~$ ll /home/vagrant/

total 28

drwxr-xr-x 4 vagrant vagrant 4096 Mar 24 19:22 ./

drwxr-xr-x 5 root    root    4096 Mar 25 14:47 ../

-rw-r--r-- 1 vagrant vagrant  220 Mar 21 21:57 .bash_logout

-rw-r--r-- 1 vagrant vagrant 3771 Mar 21 21:57 .bashrc

drwx------ 2 vagrant vagrant 4096 Mar 24 19:22 .cache/

-rw-r--r-- 1 vagrant vagrant  807 Mar 21 21:57 .profile

drwx------ 2 vagrant vagrant 4096 Mar 21 21:57 .ssh/

.bash_history – для хранения истории команд пользователя (500шт. По-умолчанию).

.bashrc – исполняемый файл, стартующий при входе пользователя в систему и производящий конфигурацию (настройку) оболочки, например, установку переменных 

окружения, синонимов (alias) и т.д. Файл . bashrc может содержать любой разрешенный набор команд и функций оболочки Bash, которые можно вводить в 

командной строке, а также сложные команды, применяемые в сценариях.

.bash_profile – Хранит пользовательские настройки окружения bash. Обычно вызывает .bashrc для получения синонимов, функций пользователя. (т.е. информацию 

из .bashrc).

.bash_logout – Этот сценарий отрабатывает, когда пользователь выходит из системы.

.ssh/- тут хранятся ключи плюс файл авторизации для ссщ

9)tree -P '*s' --prune

tree -L 2

10)file .bash_history

11)  cd /home/vagrant/sites/

cd ./demo-site/

cd ~

cd $HOME

12)ls опции /путь/к/папке

-a - отображать все файлы, включая скрытые, это те, перед именем которых стоит точка;

-A - не отображать ссылку на текущую папку и корневую папку . и ..;

--author - выводить создателя файла в режиме подробного списка;

-b - выводить Escape последовательности вместо непечатаемых символов;

--block-size - выводить размер каталога или файла в определенной единице измерения, например, мегабайтах, гигабайтах или килобайтах;

-B - не выводить резервные копии, их имена начинаются с ~;

-c - сортировать файлы по времени модификации или создания, сначала будут выведены новые файлы;

-C - выводить колонками;

--color - включить цветной режим вывода, автоматически активирована во многих дистрибутивах;

-d - выводить только директории, без их содержимого, полезно при рекурсивном выводе;

-D - использовать режим вывода, совместимый с Emacs;

-f - не сортировать;

-F - показывать тип объекта, к каждому объекту будет добавлен один из специализированных символов */=>@|;

--full-time - показывать подробную информацию, плюс вся информация о времени в формате ISO;

-g - показывать подробную информацию, но кроме владельца файла;

--group-directories-first - сначала отображать директории, а уже потом файлы;

-G - не выводить имена групп;

-h - выводить размеры папок в удобном для чтения формате;

-H - открывать символические ссылки при рекурсивном использовании;

--hide - не отображать файлы, которые начинаются с указанного символа;

-i - отображать номер индекса inode, в которой хранится этот файл;

-l - выводить подробный список, в котором будет отображаться владелец, группа, дата создания, размер и другие параметры;

-L - для символических ссылок отображать информацию о файле, на который они ссылаются;

-m - разделять элементы списка запятой;

-n - выводить UID и GID вместо имени и группы пользователя;

-N - выводить имена как есть, не обрабатывать контролирующие последовательности;

-Q - брать имена папок и файлов в кавычки;

-r - обратный порядок сортировки;

-R - рекурсивно отображать содержимое поддиректорий;

-s - выводить размер файла в блоках;

-S - сортировать по размеру, сначала большие;

-t - сортировать по времени последней модификации;

-u - сортировать по времени последнего доступа;

-U - не сортировать;

-X - сортировать по алфавиту;

-Z - отображать информацию о расширениях SELinux;

-1 - отображать один файл на одну строку.

vagrant@ubuntu-focal:~$ ls -a

.  ..  .bash_history  .bash_logout  .bashrc  .cache  .profile  .ssh

vagrant@ubuntu-focal:~$ ls -A

.bash_history  .bash_logout  .bashrc  .cache  .profile  .ssh

vagrant@ubuntu-focal:~$ ls -b

vagrant@ubuntu-focal:~$ ls -B

vagrant@ubuntu-focal:~$ ls -c

vagrant@ubuntu-focal:~$ ls -C

vagrant@ubuntu-focal:~$ ls -d

vagrant@ubuntu-focal:~$ ls -D

vagrant@ubuntu-focal:~$ ls -f

..  .cache  .ssh  .profile  .bashrc  .bash_logout  .bash_history  .

vagrant@ubuntu-focal:~$ ls -F

vagrant@ubuntu-focal:~$ ls -g

total 0

vagrant@ubuntu-focal:~$ ls -G

vagrant@ubuntu-focal:~$ ls -h

vagrant@ubuntu-focal:~$ ls -H

vagrant@ubuntu-focal:~$ ls -i

vagrant@ubuntu-focal:~$ ls -l

total 0

vagrant@ubuntu-focal:~$ ls -L

vagrant@ubuntu-focal:~$ ls -m

vagrant@ubuntu-focal:~$ ls -n

total 0

vagrant@ubuntu-focal:~$ ls -N

vagrant@ubuntu-focal:~$ ls -Q

vagrant@ubuntu-focal:~$ ls -r

vagrant@ubuntu-focal:~$ ls -R

.:

vagrant@ubuntu-focal:~$ ls -s

total 0

vagrant@ubuntu-focal:~$ ls -S

vagrant@ubuntu-focal:~$ ls -t

vagrant@ubuntu-focal:~$ ls -u

vagrant@ubuntu-focal:~$ ls -U

vagrant@ubuntu-focal:~$ ls -X

vagrant@ubuntu-focal:~$ ls -Z

vagrant@ubuntu-focal:~$ ls -1

так как линукс это не юникс, потому команду ls -la не буду поскольку чисто линуксовая команда это ls -alF или же ll алиас

vagrant@ubuntu-focal:~$ ls -alF

total 32

drwxr-xr-x 4 vagrant vagrant 4096 Mar 26 07:43 ./

drwxr-xr-x 5 root    root    4096 Mar 25 14:47 ../

-rw------- 1 vagrant vagrant   73 Mar 26 07:43 .bash_history

-rw-r--r-- 1 vagrant vagrant  220 Mar 21 21:57 .bash_logout

-rw-r--r-- 1 vagrant vagrant 3771 Mar 21 21:57 .bashrc

drwx------ 2 vagrant vagrant 4096 Mar 24 19:22 .cache/

-rw-r--r-- 1 vagrant vagrant  807 Mar 21 21:57 .profile

drwx------ 2 vagrant vagrant 4096 Mar 21 21:57 .ssh/

-rwxrw-r--: права доступа к файлам

‘1’ Указывает количество ссылок на файлы.

vagrant означает владельца файла

vagrant указывает группу, к которой принадлежит файл

4096 указывает размер файла

Mar 26 07:43 указывает время последнего обновления файла

дальше представляет имя файла или директории

13) mkdir ./test

ll /  | tee ./test/1

cat ./test/1

cp ./test/1 /home/vagrant/

rm -ri ./test/

rm -r /home/vagrant/1

14)  mkdir test

cp .bash_history ./test/labwork2

ln -s ./test/labwork2 softlink

ln ./test/labwork2 hardlink

vagrant@ubuntu-focal:~$ ls -alFi ./test/

total 20

256101 -rw------- 2 vagrant vagrant  421 Mar 26 13:24 hardlink

256101 -rw------- 2 vagrant vagrant  421 Mar 26 13:24 labwork2

30801 lrwxrwxrwx 1 vagrant vagrant   15 Mar 26 13:24 softlink -> ./test/labwork2

хард линки можно определить по айноде

vagrant@ubuntu-focal:~/test$ mv hardlink /home/vagrant/test/hard_lnk_labwork2

vagrant@ubuntu-focal:~/test$ mv softlink /home/vagrant/test/symb_lnk_labwork2

rm labwork2

доступ по сим линку к файлу трачен а доступ по хард линку нет поскольку айнода ещё жива

15) по умолчанию locate нету в линукс потому find

find / -name "*traceroute*"

find / -name "*squid*"

16) df -h

mount

/proc/mounts

17)df -h | wc -l

mount | wc -l

cat /proc/mounts | wc -l

18)  find /etc/ -name *host*

find /etc/ -name *ss*

19) ll /etc/ | grep host

ll /etc/ | grep ss

20) ll /etc/ | more 

ll /etc/ | less

21) ll /dev/

fd0	Первый дисковод

fd1	Второй дисковод

sda	First hard disk

sdb	Second hard disk

sda1	Первый раздел на первом жёстком диске IDE

sdb7	Десятый раздел на четвёртом жёстком диске SCSI

sr0	First CD-ROM

sr1	Second CD-ROM

ttyS0	Последовательный порт 0, COM1 под MS-DOS

ttyS1	Последовательный порт 1, COM2 под MS-DOS

psaux	Устройство мышь PS/2

gpmdata	Псевдо-устройство, повторитель данных от демона GPM (мыши)

cdrom	Символическая ссылка на привод CD-ROM

mouse	Символическая ссылка на файл устройства мыши

null	Всё, что записывается в это устройство, исчезнет

zero	Можно бесконечно читать нули из этого устройства

22)ll /dev/

Ниже представлено краткое описание 7 различных типов файлов в Linux:

- — обычный файл;

d — каталог;

c — символьное устройство;

b — блочное устройство;

s — (локальный) сокет;

p — именованный канал;

l — символьная ссылка.

23) ls -ltu /etc/ | head -n5
