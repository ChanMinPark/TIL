#Get started AWS EC2

###1. AWS 가입하기
AWS에 가입해서 1년간 무료로 일부 서비스를 이용할 수 있는 Free tier 혜택을 받으려면  
이메일, 전화번호, 신용카드가 필요하다.  

AWS Korea 웹페이지 링크 : http://aws.amazon.com/ko/  

링크에 접속해서 '계정 생성하기'를 통하여 계정을 생성한다.  
이메일 주소를 입력하고, 새 사용자를 선택하고, 로그인을 클릭한다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image01.PNG)


그럼 가입을 위한 기본정보를 입력하는 페이지가 나온다.  
전부 입력하고 '계정 생성'을 클릭한다.  
이때 이름은 영문으로 입력해야 한다. 나는 (GilDong Hong) 형식으로 입력했다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image02.PNG)


다음페이지에서는 연락처 정보를 입력하는데, 거주지 정보를 입력하면 된다.  
이때, 모든 정보는 영문으로 작성해야 한다.  
전체 이름은 이전 페이지에서 입력한 것 처럼 GilDong Hong 형식으로 입력했다.  
영문 주소 변환은 네이버에서 '영문주소 변환'을 검색하고 주소를 검색하면 된다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image03.PNG)


다음은 결제를 위한 정보를 입력한다.  
카드정보 입력인데, 프리 티어를 이용하더라도 카드 정보는 반드시 입력해야한다.  
그리고 최초 가입 때 1달러가 결제된다.  
카드 소유자 이름은 카드에 나온대로 입력하면 된다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image04.PNG)


다음은 ID확인이라는데 전화를 통해서 본인 인증 하는 단계이다.  
정보를 입력해 놓았으니 바로 전화 걸리를 하면된다. 그러면 전화가 온다.  
전화는 한국어로 안내가 나온다. 안내를 받고 가입페이지에 나오는 PIN번호를 입력하면 끝난다.  
가입 페이지에서 계속버튼을 누른다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image05.PNG)


계획 지원 단계는 서비스 제공 등급인건데...등급이 높을 수록 아마존에서 수준 높은 고객지원 서비스를 제공하는 것 같다.  
무료로 이용할 것이므로 '기본'을 그대로 두고 계속 진행한다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image06.PNG)


가입 끝~  
가입이 되면 바로 1년간은 Free tier가 적용된다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image07.PNG)


###2. AWS EC2 시작하기

우선 먼저, 리전을 'Seoul'로 선택한다. 한국에서 사용할 거라면 리전이 가까울 수록 좋을거니깐..  
리전은 AWS의 Data Center라고 생각하면 된다. 옛날엔 Seoul이 없었던 것 같지만 이제는 있다.
AWS 웹페이지에 로그인한 후에 오른쪽 상단에 계정 우측에서 리전을 선택할 수 있다.  

이제 EC2를 사용하기 위해 EC2 Instance를 생성한다.  
먼저 'AWS Management Console' 페이지로 들어간다.  
거기서 'EC2'를 클릭한다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image08.PNG)


그리고 가운데 'Launch Instance'를 클릭한다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image09.PNG)


Instance를 생성할 때는 어떤 종류의 Instance를 생성할지 정해야 한다.  
여기서는 AMI(Amazon Machine Image)를 선택한다.  
오른쪽의 'Select'를 클릭하면 된다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image10.PNG)


그 다음으로는 Instance의 성능을 선택하게 되는데, 당연히 성능에 따라서 요금이 다르다.  
Free tier는 t2.micro가 무료로 제공되기 때문에 t2.micro를 선택하고 'Review and Launch'를 클릭한다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image11.PNG)


다음 페이지에서 경고 문구를 보니, 웹서버를 쓸꺼면 HTTP 포트를 열어주라고 한다.  
이 작업은 Security Groups에서 할 수 있다. 'Edit security groups'를 클릭하여 수정 페이지로 간다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image12.PNG)


기본적으로 EC2에 접속하기 위한 SSH가 설정되어 있다.  
'Add Rule'을 눌러서 방화벽에 통과시킬 포트를 설정한다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image13.PNG)


나는 웹서버로 쓸거라서 HTTP와 HTTPS를 추가하였다.  
Source에 0.0.0.0/0은 모든 IP로부터의 접속을 허용한다는 것이다.  
특정 IP만 허용하게 하려면 수정하면되지만 난 그냥 뒀다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image14.PNG)


마지막으로 Review Instance Launch 단계에서 'Launch'를 눌러서 Instance를 생성한다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image15.PNG)


마지막!으로 SSH접속을 위한 key를 다운로드 받는다.  
Key는 [C:\user\{yourusername}\.ssh\{key이름}.pem] 위치에 저장하는 것이 좋다.(Windows환경)  
(Mac/Linux에서는 홈 디렉토리의 .ssh 하위에 저장하는 것이 좋다. [~/.ssh/{key이름}.pem])  
Tip. Windows에서 '.ssh' 폴더가 없으면 폴더를 새로 만들고 이름을 '.ssh.'으로 하면 마지막 점은 사라지면서 점으로 시작하는 폴더를 만들 수 있다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image16.PNG)


끝났다. 끝났다.  
View Instance를 클릭하면 생성한 Instance의 상태정보를 볼 수 있다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Get_started_AWS_EC2/image17.PNG)
