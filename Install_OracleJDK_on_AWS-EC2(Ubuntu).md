##AWS EC2(Ubuntu)에 Oracle JDK 설치하기.(apt-get 이용)

####1. Oracle jdk를 위한 apt repository 추가  
현재 Ubuntu에서는 기본적으로 openjdk를 설치할 수 있지만, oracle jdk는 기본 repository에서 빠져있다고 한다.  
그래서 oracle jdk를 apt-get으로 설치하기 위해서는 repository를 추가해 주어야 한다.  

```
$sudo add-apt-repository ppa:webupd8team/java
```

현재 기준으로 repository를 추가하면, 안내문구가 뜬다. 그것은 Java 9에 대한 안내이다. 혹시 Java 9을 사용할 사람은 그에 대한 사항을 명시해서 repository를 추가하라는 거 같다.  
그렇지만 현재는 안정되지 않은 java 9을 쓸 이유가 없으므로 그냥 엔터를 눌러서 진행한다.  

추가한 repository를 적용하려면 update를 해주어야 한다.  
```
$sudo apt-get update
```


####2. Oracle jdk 8 설치  
repository를 추가했으니 아래 명령어로 oracle jdk 8을 설치할 수 있다.  
```
$sudo apt-get install oracle-java8-installer
```

설치 중간에 라이센스 사용에 동의하냐고 묻는다. 'Ok'를 누르고 다음 창에서 'Yes'를 누르면 된다.  
설치가 완료되면 아래 명령어로 설치를 확인할 수 있다.  
```
$java -version
```

혹시 다른 java(다른 버전 또는 openjdk)가 동시에 깔려있어서 사용할 java를 선택해 주어야 하면 아래와 같이 할 수 있다.  
```
$sudo update-alternatives --config java
```
사용하고 싶은 java를 선택해주면 된다.  

마지막으로, Oracle jdk8을 사용하기 위한 환경변수 설정을 해줘야 하는데,  
수동으로 할 수도 있지만 oracle에서 환경변수 설정을 위한 패키지도 제공한다.  
```
$sudo apt-get install oracle-java8-set-default
```
위의 패키지를 설치한 후에는 반드시 Reboot해줘야 한다.  

이제 Oracle Java8 설치가 완료 되었다.

####3. 비고
- apt로 설치한 oracle java8이 jdk까지 설치되는 것이 맞나 싶었다. oracle의 설명을 보니깐 jdk와 jre가 모두 포함된 것이라고 한다. 오히려 jre만 설치하는게 불가능하다고 한다.
- Oracle에서 제공하는 'apt를 이용한 java8 설치 방법'은 아래 링크에서 확인 할 수 있다.
  - 링크 : http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html
