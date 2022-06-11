## два пункта сделал с гуи, каюсь не всемогущ


## создаем файлик


1983  echo 1>/home/sax/Загрузки/ami

## берем список имеджей перенаправляем в файлик чтобы не ломать галаз а поиском его найти

 1984  aws ec2 describe-images > /home/sax/Загрузки/ami
 
 ## поиск нужного имеджа
 
 1985  nano /home/sax/Загрузки/ami
 
 ## ищем уже существующуу секюр группу
 
 1987  aws ec2 describe-security-groups
 
 ## ищем уже существующий ключик
 
 2000  aws ec2 describe-key-pairs 
 
 
 ## создаем инстанс
 
 2001  aws ec2 run-instances --image-id ami-0eb7496c2e0403237 --security-group-ids sg-0fb4415cc5e0d3d6b --instance-type t2.micro --key-name home
 
 ## мочим его 
 
 2003  aws ec2 terminate-instances --instance-ids i-0e2b4f0c119531916
 
 ## cоздаем опять 
 
 2004  aws ec2 run-instances --image-id ami-0eb7496c2e0403237 --security-group-ids sg-0fb4415cc5e0d3d6b --instance-type t2.micro --key-name home
 
 ## чтобы зайти по внешнему апйпишнику нужно дать права на ключик 
 
 2005  sudo chmod 400 /home/sax/Загрузки/учеба/home.pem 
 
 ## но зашли мы по доменому именно, раздницы нет оно когда создает инстанс это всё показует
 
 2006  ssh -i "/home/sax/Загрузки/учеба/home.pem" ec2-user@ec2-18-193-81-141.eu-central-1.compute.amazonaws.com
 
 ## останавливаем 
 
 2007  aws ec2 stop-instances --instance-ids=i-02f6379c3f0834b32
 
 ## запускаем 
 
 2008  aws ec2 start-instances --instance-ids=i-02f6379c3f0834b32
 
 
 ## смотрим волюм айди 
 
2010  aws ec2 describe-instances --query 'Reservations[*].Instances[*].[Tags[?Key==`Name`].Value,InstanceId,BlockDeviceMappings[*].Ebs.VolumeId]' --output text

## делаем снепшот

 2011  aws ec2 create-snapshot --volume-id vol-015fc67efd081e01d
 
## делаем новый волюм 
 
 2012  aws ec2 create-volume --size 5 --region eu-central-1 --availability-zone eu-central-1a --volume-type gp2
 
 ## ататчим его к инстансу
 
 2013  aws ec2 attach-volume --volume-id vol-04c8f6e4e6a707e16 --instance-id i-02f6379c3f0834b32 --device /dev/sdf


## делаем имедж с снепшота

2002  aws ec2 register-image --name "from_snapshot" --region=eu-central-1 --description "AMI_from_snapshot_EBS" --block-device-mappings DeviceName="/dev/sda",Ebs={SnapshotId="snap-0c27d83c6ca56c9dc"} --root-device-name "/dev/sda1"
 
## с этого имеджа запускаем инстанс
 
 
 2005  aws ec2 run-instances --image-id ami-05b2727a84692b314 --security-group-ids sg-0fb4415cc5e0d3d6b --instance-type t2.micro --key-name home
 
## смотрим волюм нового инстанса
 
 
 2007  aws ec2 describe-instances --query 'Reservations[*].Instances[*].[Tags[?Key==`Name`].Value,InstanceId,BlockDeviceMappings[*].Ebs.VolumeId]' --output text
 
 ## отсоединяем его 
 
 2008  aws ec2 detach-volume --volume-id vol-0190865d6ffb00539
 
## создаем юзера, по умолчанию юзер создается с минимальными привелегиями
aws iam create-user --user-name prateek
## создаем бакет
 
 
 2010  aws s3 mb s3://sax41
 
## загружаем в бакет
 
 2012  aws s3 cp /home/sax/Загрузки/udemy/UC-1bd5fa96-2eb9-42b9-a7c0-44befd05a1cc.jpg s3://sax41

## для статик сайта создаем бакет

2001  aws s3 mb s3://sax41

## делаем его паблик

 2002  aws s3api put-public-access-block --bucket sax41 --public-access-block-configuration "BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=false,RestrictPublicBuckets=false"
 
## навешуем политику
 
 2005  aws s3api put-bucket-policy --bucket sax41 --policy "{
 
 \"Version\": \"2012-10-17\",
  
  
  \"Statement\": [
  
      {
	  
          \"Sid\": \"PublicReadGetObject\",
		  
          \"Effect\": \"Allow\",
		  
          \"Principal\": \"*\",
		  
          \"Action\": \"s3:GetObject\",
		  
          \"Resource\": \"arn:aws:s3:::sax41/*\"
		  
      }
	  
  ]
  
  
}"


## делаем статик веб сайт


 2006  aws s3 website "s3://sax41" --index-document index.html --error-document index.html
 
 ## загружа туда сайт
 
 2007  aws s3 sync /home/sax/Загрузки/demo-site/demo/ "s3://sax41/"  


## и командой курл проверяем

 curl http://sax41.s3-website.eu-central-1.amazonaws.com
 
 
 <!DOCTYPE html>
 
<html>

<head>

    <meta charset="UTF-8">
	
    <title>NGINX Fundamentals</title>
	
    <link rel="stylesheet" href="style.css" type="text/css">
	
</head>
	
	
	

<body>

    <header>
	
        <div class="inner">
		
            <img class="thumb" src="thumb.png" alt="NGINX Logo">
			
            <div class="heading">
			
                <h1>NGINX Fundamentals</h1>
				
                <br>
				
                <p>Learn how to install & configure an Nginx web server from scratch.</p>

		    
![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m2/task2.2/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-02-09%2015-56-41.png)

## создали домен и создали Hosted zone в AWS
![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m2/task2.2/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-06-10%2016-16-34.png)
## и теперь переносим AWS NS записи
![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m2/task2.2/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-06-10%2016-08-20.png)

![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m2/task2.2/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-06-10%2016-28-59.png)  
 ![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m2/task2.2/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202022-02-09%2017-15-49.png)
 ![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m2/task2.2/AZ900%20Vadym%20Beznosenko.jpg)
![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m2/task2.2/UC-d128a8d6-e863-41b0-bdac-f2f5f2b500d0.jpg)		 
![alt text](https://github.com/vadimbeznosenko/DevOps_online_Kyiv_2022Q1Q2/blob/master/m2/task2.2/UC-89e0db11-564c-4b03-a071-8f2492c0fe1c.jpg)
