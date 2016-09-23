# AWS EC2로 우분투 서버 만들기

## 1. AWS 콘솔에 접속

## 2. AWS 콘솔에서 EC2 선택

## 3. 'Launch Instance' 클릭

## 4. Step1. 에서 원하는 운영체제 선택
이번에는 Free Tier로 제공되는 'Ubuntu Server 14.04 LTS (HVM), SSD Volume Type'을 선택합니다.  

## 5. Step2. 에서 서버 사양 선택
Free Tier로 제공되는 't2.micro'를 선택합니다.  
'Review and Launch'를 선택합니다.  

## 6. Step7. 에서 Instance 설정을 확인합니다.
Step2. 에서 'Review and Launch'를 바로 클릭하면, Step7. 에서 이런 메세지가 나타납니다.  

이는 보안설정이 안되어 있으니 설정하는게 좋다라고 알려주는 것입니다.  
'Edit security groups'을 눌러서 보안 설정에 들어갑니다.  

## 7. Step6. 에서 보안 그룹 설정
Step 6. 에서는 보안 그룹을 설정할 수 있습니다. 저는 웹서버로 사용할 것이므로 Type에서 HTTP, HTTPS를 선택하고 추가합니다. 'Add Rule'을 선택하면 하나씩 추가할 수 있습니다.  
그리고 ssh로 원격접속을 할 것이기 때문에 SSH도 추가합니다.  
선택적으로 'Security group name' 에서 이름을 바꿔줘도 됩니다.  
접근 가능한 IP를 제한하려면 Source를 수정합니다. '0.0.0.0/0'은 모든 IP에서 접근 가능하다는 것입니다.  
'Review and Launch'를 선택하여 설정을 완료합니다.  


## 8. 보안설정 후의 Step7. 에서 'Launch' 버튼을 클릭

## 9. 키파일 생성
키파일을 생성합니다. 키파일은 서버에 SSH로 원격접속할 때 사용됩니다.  
기존의 키파일이 없으면 'Create a new key pair'를 선택하고 키파일 이름을 입력하고 'Download Key Pair'를 눌러서 키파일을 다운받습니다.  
Key는 [C:\user{yourusername}.ssh{key이름}.pem] 위치에 저장하는 것이 좋습니다.(Windows환경)  
(Mac/Linux에서는 홈 디렉토리의 .ssh 하위에 저장하는 것이 좋다. [~/.ssh/{key이름}.pem])  
Tip. Windows에서 '.ssh' 폴더가 없으면 폴더를 새로 만들고 이름을 '.ssh.'으로 하면 마지막 점은 사라지면서 점으로 시작하는 폴더를 만들 수 있습니다.  
키파일을 저장했으면 'Launch Instances'를 누릅니다.  

## 10. 서버 접속
Instance 현황에서 해당 서버를 선택하고 상단에 'Connect'를 누르면 ssh 접속할 수 있는 방법이 나옵니다.
