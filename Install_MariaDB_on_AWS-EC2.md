##Maria DB 설치 (on AWS EC2)  

####Step 1) Maria DB 설치  
**!참고!** Raspbian을 wheezy가 아닌 jessie버전으로 사용해야 한다. wheezy에서도 추가적인 과정을 통해서 mariadb-server 패키지를 받을 수 있지만 번거롭다. 그냥 jessie를 사용하는게 좋아보인다.  

apt-get을 이용해서 MariaDB를 설치한다.  
```
$sudo apt-get install mariadb-server
```
