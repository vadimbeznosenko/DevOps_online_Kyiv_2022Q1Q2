.gitconfig


# ну тут думаю понятно

[user]
        name = Vadym Beznosenko
        email = vadim.beznosenko88@gmail.com

тут тоже 
[core]
        editor = nano
        excludesFile = /home/sax/.gitignore
        
алиасы для моего комфорта
[alias]
        c = config
        commitall = "!git add -A; git commit"
[commit]
        verbose = true
        
люблю когда красивенько
[pretty]
        my = format:%C(yellow)%h %C(dim green)%cd %C(reset)| %s%d [%an]



создаем папки и файлы, так как это будет не сильно интресно по заданию решил его модифицировать
1942  mkdir -p ./m1/task1.1/
 1943  touch ./m1/task1.1/README.md
 1944  mkdir -p ./m2/task2.1/
 1945  touch ./m2/task2.1/README.md
 1946  mkdir -p ./m2/task2.2/
 1947  touch ./m2/task2.2/README.md
 1948  mkdir -p ./m3/task3.1/
 1949  touch ./m3/task3.1/README.md
 1950  mkdir -p ./m4/task4.1/
 1951  touch ./m4/task4.1/README.md
 1952  mkdir -p ./m5/task5.1/
 1953  touch ./m5/task5.1/README.md
 1954  mkdir -p ./m6/task6.1/
 1955  touch ./m6/task6.1/README.md
 1956  mkdir -p ./m7/task7.1/
 1957  touch ./m7/task7.1/README.md
 1958  mkdir -p ./m8/task8.1/
 1959  touch ./m8/task8.1/README.md
 1960  mkdir -p ./m8/task8.2/
 1961  touch ./m8/task8.2/README.md
 1962  git add .
 1963  git commit -m "Golden_Copy"
 
 
 
 пушим на гит
 1964  git push origin 
 
 заходим в папку
 1969  cd /home/sax/Загрузки/DevOps_online_Kyiv_2022Q1Q2/m1/task1.1/
 создаем ветку и заходим в неё
 1971  git checkout -b develop
 
 обожаю команду эхо
 1991  echo 1> index.html
 1992  git add .
 1993  git commit -m "add index.html"
 создаем другую ветку заходим туда
 1994  git checkout -b images
 
 копирую свой серт по гиту
 1995  cp /home/sax/Загрузки/udemy/UC-1bd5fa96-2eb9-42b9-a7c0-44befd05a1cc.jpg /home/sax/Загрузки/DevOps_online_Kyiv_2022Q1Q2/m1/task1.1/
 1996  git add .
 1997  git commit -m "add images"
 
 тут я понял что наложал
 2005  mkdir images
 2007  mv UC-1bd5fa96-2eb9-42b9-a7c0-44befd05a1cc.jpg ./images/
 2009  git add .
 2010  git commit -m "create folder images and copy imeges, edit index.html"
 
 правлю индех для картинки
 2011  nano index.html 
 2012  git add .
 2013  git commit -m "add paht images in index.html"
 
 создаем третью ветку
 2015  git checkout -b styles
 
 тут уже не наложал
 2016  mkdir styles
 2017  mv ~/Загрузки/master/css-hexagon-image-with-border/css/* /home/sax/Загрузки/DevOps_online_Kyiv_2022Q1Q2/m1/task1.1/styles/
 2018  git add .
 2019  git commit -m "add styles"
 2024  git add .
 2025  git commit -m "add styles"
 2026  git checkout develop 
 2027  git merge images 
 2028  git merge styles
 тут я понял что наложал и эта команда помжет смерджить комфлик
 2029  git checkout --conflict=diff3 --merge index.html
 
 тут без любимого ви никак,нужно кое что поправить
 2030  vi index.html 
 2032  git checkout develop 
 2034  git add .
 2035  git commit -m "merge images and style to develop, fix conflict merge"
 
 люблю красивые логи
 2037  git log --pretty=format:'%C(yellow)%h %C(dim green)%cd %C(reset)| %s%d [%an]' --date=format:'%F %R'
 
 e4475a3 2022-02-04 11:14 | add certificate (HEAD -> master, origin/master) [Vadym Beznosenko]
d123d47 2022-02-04 11:03 | merge images and style to develop, fix conflict merge [Vadym Beznosenko]
2426618 2022-02-04 09:25 | add paht images in index.html (origin/images, origin/develop, images, develop) [Vadym Beznosenko]
c2aac04 2022-02-04 09:20 | create folder images and copy imeges, edit index.html [Vadym Beznosenko]
c4999c9 2022-02-03 22:01 | add images [Vadym Beznosenko]
20155b6 2022-02-03 21:58 | add index.html [Vadym Beznosenko]
f48426b 2022-02-03 21:18 | Golden_Copy (origin/main, origin/HEAD, main) [Vadym Beznosenko]
58cde28 2022-02-03 21:00 | Initial commit [Vadym Beznosenko]

 2042  git push origin --all 
