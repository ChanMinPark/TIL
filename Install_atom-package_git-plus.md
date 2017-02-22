# Atom에서 git-plus 설치하기
(부제 : git-plus 에러 시행착오)

### 1. git-plus 설치
Atom의 상단 메뉴에서 'Packages'-'Settings View'-'Install Packages/Themes'를 선택합니다.  

그 다음, git-plus를 검색해서 Install합니다.  
설치는 끝입니다.(너무 간단)  

### 2. git-plus 설정
사실 이 부분이 난관이었습니다.  

처음 Atom을 접하고 여러 패키지들을 설치했는데, 아무것도 따로 설정을 해줄 필요는 없었습니다.  
그래서 git-plus도 설치하고 아무런 설정을 해주지 않았죠...  
이게 실수였습니다.  

Atom뿐만 아니라 git을 사용하는 어떤 프로그램이든 git프로그램의 위치를 알아야 git을 수행합니다.  
그래서 git-plus도 자신이 사용할 git프로그램이 어디있는지 경로를 알아야 정상적으로 동작합니다.  

위에서 git-plus를 설치하고 나면 바로 'Install'이 있던 자리에 'Settings' 버튼이 생깁니다.  
Setting에 들어가면 Git Path를 설정 할 수 있는데, 여기에 자신이 사용하는 git프로그램의 경로를 입력해주면됩니다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/atom_git_issue/image02.JPG)

git-plus가 사용할 git프로그램의 위치를 모르면 아래와 같이 텍스트가 깨진 상태로 어쩌고저쩌고 에러가 발생합니다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/atom_git_issue/image01.JPG)
