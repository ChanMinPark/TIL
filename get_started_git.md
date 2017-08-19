## 새로운 local git repository 생성해서 새로 생성한 remote git repository에 업로드하기
(remote provider는 GitHub 이용)  

### <준비>  
.1. GitHub 사이트에서 repository를 만든다. 그러면 repository에 대한 주소를 획득할 수 있다.  
.2. 로컬pc에 로컬repository로 사용할 폴더를 새로 만든다. 이 폴더는 GitHub 사이트에서 만든 repository와 연동시킬 것이다.  

### <로컬repository에서 git을 사용하기 위한 설정작업>  
.3. 로컬pc에서 git을 설치한다.  
  - (리눅스의 경우)```sudo apt-get install git```  
  - (윈도우의 경우) https://git-scm.com/downloads  
  
.4. 로컬pc에서 만든 폴더에 들어가서 ```git init```명령을 수행하면 해당 폴더를 git에 연동시킬 폴더로 사용할 준비가 된다.  
.5. git에 upload할때 사용될 사용자명과 이메일을 등록한다.  
```
git config --global user.name "이름"
git config --global user.email "이메일"
```
.6. GitHub의 repository와 연동시키기 위해 repository주소를 닉네임으로 등록한다.  
```
git remote add (닉네임) (repository주소)
```

### <Git 사용>  
.7. ```git pull 닉네임 master``` 로 현재 GitHub에 있는 자료들을 로컬로 동기화 시킨다.   
.8. 파일의 추가,수정,삭제 등의 변경이 발생하면  
```git add (파일명)```으로 추가하고(전체 add는 ```$git add .```)  
```git commit -m "메세지"```를 한다. 그리고나서  
```git push 닉네임 master```로 GitHub에 최종적으로 업로드한다.  
