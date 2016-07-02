##Maria DB 설치 (on AWS EC2)  

####Step 1) Maria DB 설치  
apt-get을 이용해서 MariaDB를 설치한다.  
apt-cache 를 이용하면 설치 전에 다운 받은 패키지가 있는지, 어떤 버전을 다운 받을 수 있는지 확인 할 수 있다.  
확인은 선택사항이다.  
```
$apt-cache policy mariadb-server
```
![](https://github.com/ChanMinPark/TIL/blob/master/image/Install_MariaDB_on_AWS-EC2/image01.PNG)

설치는 apt-get install을 이용한다.  
```
$sudo apt-get install mariadb-server
```

설치 과정중에 root 계정에 대한 비밀번호를 물어본다.(2번 물어본다.)  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Install_MariaDB_on_AWS-EC2/image02.PNG)
![](https://github.com/ChanMinPark/TIL/blob/master/image/Install_MariaDB_on_AWS-EC2/image03.PNG)

잠시 후면 설치가 완료된다.  

설치를 확인하기 위하여 MariaDB에 접속해 본다.  
```
$mysql -u root -p
```
아래 그림처럼 나오면 설치가 정상적으로 된 것이다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Install_MariaDB_on_AWS-EC2/image04.PNG)
