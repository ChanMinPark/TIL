###AWS EC2(Ubuntu)에 Tomcat7 설치하기. (apt-get 이용)  

####1. 아래 명령어를 이용해서 tomcat7을 간단하게 설치한다.  
```
$sudo apt-get install tomcat7
```

설치과정에서 JDK나 JRE가 없다고 할 수도 있다. 이 경우는 Tomcat의 설정에서 JAVA_HOME의 경로가 잘못 잡혀있는 것이다.  
아래 2번 과정으로 JAVA_HOME경로를 잡아준다.  

####2. JAVA_HOME 경로 잡아주기.
Tomcat의 설정파일에 있는 JAVA_HOME 경로를 본인의 JDK위치로 잡아줘야 한다.  
나는 우분투에 Oracle java8을 설치했다.(설명 링크 : https://github.com/ChanMinPark/TIL/blob/master/Install_OracleJDK_on_AWS-EC2(Ubuntu).md)  
그래서 나의 JAVA_HOME 경로는 ```/usr/lib/jvm/java-8-oracle```이다.  

아래 명령어를 입력하여 Tomcat의 JAVA_HOME 경로를 바꿔주러 간다.  
```
$sudo nano /etc/default/tomcat7
```

명령어를 입력하면 중간쯤에 JAVA_HOME 변수가 보인다.  
맨 앞에 '#'을 제거하여 주석처리를 벗겨내고, JAVA_HOME의 경로를 본인의 것으로 수정한다.  
나는 위에서 언급한 ```/usr/lib/jvm/java-8-oracle```이다.

####3. Tomcat7 구동
```
$sudo service tomcat7 start
```

명령어를 입력하면 tomcat7이 정상 구동되면서 아래와 같이 출력한다.  
```
 * Starting Tomcat servlet engine tomcat7
   ...done.
```

####4. Tomcat7 구동 확인
웹브라우저에서 ```ip주소:8080```으로 접속해서 tomcat7이 구동 되었는지 확인한다.  
구동이 정상적으로 되었으면 ```It works!```라고 웹브라우저에 나타난다.  

우분투에서 tomcat 포트가 열려있는지 확인할 수도 있는데,  
```
$sudo netstat -tnlp
```
를 입력하면 8080(tomcat 기본 포트)포터를 확인할 수 있다.  
