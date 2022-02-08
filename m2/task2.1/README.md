## начнем с разбора вагрант файла


### говорим вагранту на какой версии он работает

VAGRANTFILE_API_VERSION = "2"

### чтобы миксовать конфигурации

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

### при кучи виртуалок эта штука позволяет искользовать один ssh ключь
 
  config.ssh.insert_key = false

### при кучи машин задаем блок для пределеной

  config.vm.define "sax-OptiPlex-3010_Beznosenko" do |vm|
  
###  определяем сам бокс
  
    vm.vm.box = "ubuntu/focal64"
    
###   настраиваем сеточку
    
    vm.vm.network "public_network", ip: "192.168.31.10"
    
###     тут всё понятно, проброс портов
    
    vm.vm.network "forwarded_port", guest: 80, host: 8080
    
    vm.vm.network "forwarded_port", guest: 443, host: 8443
    
    vm.vm.network "forwarded_port", guest: 22, host: 2201
    
###     чтобы с кли вбокса не пробрасывать папку я пробросил её вагарнтом
    
	vm.vm.synced_folder "/home/sax/data/", "/home/vagrant/data"
	
###   этой строкой определяем какой будет провайдер, что дергать чтобы создавалась машинка
  
    vm.vm.provider "virtualbox" do |vb|
    
 ###    задаем память 
    
      vb.customize ["modifyvm", :id, "--memory", "1024"]
      
  ###     задаем количество вцпу
      
      vb.customize ["modifyvm", :id, "--cpus", "1"]
      
  ###     задаем количесво видео
      
	    vb.customize ["modifyvm", :id, "--vram", "16"]
	  
  end
end

### новый блок для новой машнки

 config.vm.define "sax-OptiPlex-3010_Beznosenko2" do |vm2|
 
   vm2.vm.box = "ubuntu/focal64"
   
   vm2.vm.network "public_network", ip: "192.168.31.11"
   
   vm2.vm.network "forwarded_port", guest: 80, host: 8081
   
   vm2.vm.network "forwarded_port", guest: 443, host: 8444
   
   vm2.vm.network "forwarded_port", guest: 22, host: 2202
   
   vm2.vm.synced_folder "/home/sax/data/", "/home/vagrant/data"
   
   vm2.vm.provider "virtualbox" do |vb|
   
     vb.customize ["modifyvm", :id, "--memory", "1024"]
     
     vb.customize ["modifyvm", :id, "--cpus", "1"]
     
     vb.customize ["modifyvm", :id, "--vram", "16"]
     
end



### этим блоком мы дергаем ансабль, чтобы сконфигурил уже готовые машинки

   vm2.vm.provision "ansible" do |ansible|
   
###    тут мы говорим на каких машинках это делать
   ansible.limit = 'all'
   
###    тут сама плайбука
      ansible.playbook = "mezzanine-across-hosts.yml"
    end
 end
end









## кли ноута


### поднимаем машинки 

1938  vagrant up 

### смотрим на состояние машинок

 1939  vagrant status 
 
###  смотрим на состояние машинок через вбокс кли
 
 1940  VBoxManage list vms
 
###  выключаем машинку
 
 1944  VBoxManage controlvm "t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875" poweroff
 
###  включаем 
 
 1953  VBoxManage startvm "t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875"
 
###  делаем паузу
 
 1956  VBoxManage controlvm "t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875" pause
 
###  востановляем работу
 
 1957  VBoxManage controlvm "t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875" resume
 
###  сбрасуем если залипла
 
 1958  VBoxManage controlvm "t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875" reset
 
###  выключаем 
 
 1966  VBoxManage controlvm "t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875" poweroff

###  клонируем
 
###  1974  VBoxManage clonevm t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875 --name="t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875_clone1" --register --mode=all --options=keepallmacs --options=keepdisknames --options=keephwuuids
 
###  смотрим какие мы молодцы
 
 1975  VBoxManage list vms
 
###  добавляем одну в групу 
 
 1979  VBoxManage modifyvm "t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875" --groups "/TestGroup"
 
###  добавляем вторую
 
 1981  VBoxManage modifyvm "t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875_clone1" --groups "/TestGroup"
 
###  включем их
 
 1982  VBoxManage startvm "t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875__clone1"
 
 1983  VBoxManage startvm "t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875"
 
###  делаем снепшот 
 
 1984  VBoxManage snapshot t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875 take snap-001
 
 1985  VBoxManage snapshot t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875 take snap-002
 
 1986  VBoxManage snapshot t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875 take snap-003
 
 
 
 
 1987  vagrant status 
 
###  заходим на машинку по ssh
 
 1988  vagrant ssh sax-OptiPlex-3010_Beznosenko 
 
 ### смотрим снепшоты
 
 1991  VBoxManage snapshot t1_sax-OptiPlex-3010_Beznosenko_1643976189460_14875 list
 
 ### собираем бокс
 
 1994  vagrant package --vagrantfile ~/Загрузки/Epam/m2/t1 --output my_box.box
 
###  всё мочим без зазрения совести
 
 1997  vagrant destroy -f
 
 
<img src="/home/sax/Загрузки/DevOps_online_Kyiv_2022Q1Q2/m2/task2.1/UC-eeffe613-cfb0-447a-bd1f-87e25a4a16b5.jpg"> 
 
