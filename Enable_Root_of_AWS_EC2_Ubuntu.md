# AWS EC2에 생성한 우분투의 루트 계정 활성화하기.
AWS EC2에 우분투 인스턴스를 생성하면 기본적으로 Root계정은 막혀있습니다.  
그래서 기본적으로 우분투에 SSH접속하려면 암호로 접속하지 않고 AWS에서 다운로드 하는 키파일로 접속해야합니다.  
여러모로 루트 계정을 사용하지 못하는 것은 때때로 불편하니깐 루트 계정을 활성화합니다.  

## 1. 루트 계정 비밀번호 설정
아래 명령어를 입력하여 루트 계정의 비밀번호를 설정합니다.  
```
$sudo passwd root
```

## 2. SSH 비밀번호로 접속 가능하게 설정
/etc/ssh/sshd_config 를 에디터로 열어서 'PasswordAuthentication no'항목을 'PasswordAuthentication yes'로 수정합니다.  
또한 root를 비밀번호로 사용하는 것이기 때문에  
```
PermitRootLogin without-password
```
를 찾아서 맨앞에 #를 붙여서 주석처리하고 아랫줄에 다음을 추가합니다.  

```
PermitRootLogin yes
```

수정이 완료되었으면 저장하고 에디터를 나와서 아래 명령어로 ssh를 재시작 합니다.  
```
$sudo service ssh reload
```
