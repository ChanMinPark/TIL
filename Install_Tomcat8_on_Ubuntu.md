# 우분투에 Tomcat 8 설치하기

## 1. Tomcat 8 다운로드
Tomcat 8 다운로드 페이지(http://tomcat.apache.org/download-80.cgi)에서 다운로드 할 톰캣의 다운로드 링크를 알아냅니다.  
저는 8.0.37(현재 최신)을 다운로드 받기 위해서 'Core'의 'tar.gz'에 우클릭해서 링크 주소 복사하기를 하였습니다.(http://mirror.navercorp.com/apache/tomcat/tomcat-8/v8.0.37/bin/apache-tomcat-8.0.37.tar.gz)  

우분투에서 wget으로 위의 링크의 파일을 다운로드합니다.  
```
$wget http://mirror.navercorp.com/apache/tomcat/tomcat-8/v8.0.37/bin/apache-tomcat-8.0.37.tar.gz
```


## 2. Tomcat 8 파일 압축해제 및 폴더 이동
다운로드 받은 Tomcat 8 파일을 압축해제 합니다.  
```
$tar xvfz apache-tomcat-8.0.37.tar.gz
```

압축을 해제한 폴더를 /usr/local 이하로 이동시킵니다.  
```
$sudo mv apache-tomcat-8.0.37 /usr/local/
```


## 3. Tomcat 8 환경설정
/etc/profile를 에디터(vi, nano 등)로 열어서 맨 아래에 아래와 같이 Tomcat 8에 대한 설정을 추가 합니다.  
```
export CATALINA_HOME=/usr/local/apache-tomcat-8.0.37
export CLASSPATH=.:$CATALINA_HOME/lib/jsp-api.jar:$CATALINA_HOME/lib/servlet-api.jar
PATH=$PATH:$CATALINA_HOME/bin
```

저장하고 나왔으면 아래 명령어로 설정파일을 적용시킵니다.  
```
source /etc/profile
```


## 4. 포트 변경
톰캣을 처음 설치하면 접속 포트가 8080으로 되어 있습니다.  
이를 HTTP(80) 포트로 변경해줍니다.  

설정 파일을 엽니다.  
```
$cd /usr/local/apache-tomcat-8.0.37/conf
$nano server.xml
```

아래 부분을 찾습니다.  
```
 <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```

이 부분에서 8080을 80으로 수정합니다.  
```
<Connector port="80" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```



## 5. Tomcat 8 구동
톰캣 폴더의 bin 폴더로 가서 톰캣을 구동시킵니다.  
```
$cd /usr/local/apache-tomcat-8.0.37/bin
$sh startup.sh
```

**주의사항! 반드시 루트 권한으로 startup시켜야합니다. 루트 계정인 상태로 진행하거나 sudo를 꼭 붙여줘야 포트가 제대로 열립니다.**  

웹브라우저에서 ```http://{ip주소}```를 입력하여 웹서버가 구동되었는지 확인합니다.  
톰캣 설정 페이지가 나타나면 정상적으로 구동이 된 것입니다.
