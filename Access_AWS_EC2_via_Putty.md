# Putty를 이용해서 EC2(Ubuntu)에 접속하는 방법.

## 1. 키파일 변환
AWS의 EC2에서 서버를 생성하면 SSH접속을 위한 키파일을 *.pem 형식으로 제공합니다.  
그런데 Putty에서는 *.pem 형식의 키파일을 지원하지 않습니다.  
그래서 *.pem을 *.ppk로 변환해주어야 합니다.  
키파일 형식 변환은 Puttygen으로 할 수 있습니다.  
(다운로드 링크 : http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)  

(변환 방법 참고 링크 : https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html?icmpid=docs_ec2_console)
PuTTygen을 실행하고 'Load'를 눌러서 EC2를 생성할 때 다운받은 키파일을 선택합니다.  
주의할 점은 파일 형식을 All Files로 바꿔야 *.pem형식의 파일이 보입니다.  
'Save private key'를 클릭하고 passphrase없이 저장하겠냐는 질문창에서 Yes를 누릅니다.  
키파일 이름을 입력하는데 *.pem형식의 파일이름과 같게하고 확인합니다.  


## 2. Putty 접속
Putty를 실행합니다.  
'HostName(or IP address)'에 Instance 현황에서 'Connect'을 눌렀을 때 나타나는 계정 정보를 입력합니다.  
왼쪽 'Category'에서 SSH 하위 항목 중 Auth를 선택하면 오른쪽에 'Private key file for authentication'에서 'Browse'를 눌러서 위에서 변환한 *.ppk형식의 키파일을 선택합니다.  
'Open'을 클릭하면 접속이 됩니다.
