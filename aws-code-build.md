# AWS CodeBuild를 이용해서 프로젝트 빌드하기  

## AWS CodeBuild 란?  
> AWS CodeBuild는 소스 코드를 컴파일하고 테스트를 실행하며 배포 준비가 완료된 소프트웨어 패키지를 생성하는 완전 관리형 지속 통합 서비스입니다.  
>
> ㅡ 'AWS CodeBuild 웹사이트' 내용 중,  

설명에서도 알 수 있듯이 CodeBuild는 CD(Continuous Deployment, 지속적 통합)에 사용되는 서비스입니다.  

일반적으로, 빌드를 로컬에서 수행하고 직접 서버에 배포할 수 있습니다. 하지만 이런 시간을 단축하기 위해서 단순히 프로젝트를 git에 push하는 것만으로 자동으로 빌드를 수행하도록 CodeBuild와 같은 Tool을 이용합니다.  

CodeBuild 요금은 실제로 빌드한 시간 만큼만 지불하면 됩니다.  

## CodeBuild 작동 개요  
CodeBuild는 아래 그림처럼, 소스 공급자에 소스가 업로드 되면 CodeBuild에서 알아서 가져다가 빌드를 진행합니다. 그리고 빌드가 완료되면 아티팩트(빌드 결과물)를 아티팩트 저장소에 저장합니다.  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image01.JPG?raw=true)  

CodeBuild에서 지원하는 소스 공급자 리스트는 아래와 같습니다.  
- AWS CodeCommit  
- Amazon S3  
- Github  
- Github Enterprise  
- Bitbucket  

그리고 아티팩트 저장소는 Amazon S3를 선택하거나 '선택하지 않을 수' 있습니다.  
선택하지 않는 경우는, 빌드 후 절차에서 ECR에 저장하거나 단순 빌드 테스트하는 목적입니다.  

이번 포스팅에서는 CodeBuild를 기초적으로 사용해보기 위해서 아래와 같이 소스 공급자를 Github으로 하고, 아티팩트 저장소를 Amazon S3로 해보겠습니다.  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image02.JPG?raw=true)  

## CodeBuild로 프로젝트 빌드하기  
> 이번 포스팅에서 사용하는 소스코드는 Nuxt.js를 이용한 웹 프론트엔드 프로젝트입니다.  
> 그래서, 빌드 환경이 Node.js 이며 버전은 12 입니다.  

> [2019.12.07 기준] 한국어 AWS 문서가 아직 최신 내용으로 업데이트가 되지 않았습니다. 한국어 문서에는 nodejs 지원 버전이 8와 10이 있는데, 영어로 보면 nodejs 지원 버전이 10, 12가 추가되어 있네요.  

### (1) 아티팩트 저장소로 사용할 Amazon S3 Bucket 생성  
CodeBuild 프로젝트를 생성하기에 앞서서, 생성 과정에서 선택해줄, 아티팩트 저장소로 S3 Bucket을 생성해줍니다.  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image03.JPG?raw=true)  


### (2) buildspec.yml 작성  
buildspec.yml 파일에는 빌드과정에서 필요한 정보를 입력합니다. 빌드 환경을 설정하거나 빌드 과정에서 수행할 명령어들을 입력하고, 빌드 결과물에 대한 정보를 입력합니다.  
작성한 파일은 기본적으로 소스 프로젝트의 루트 디렉토리에 저장합니다.  

buildspec.yml에 대한 자세한 설명은 아래 링크에서 확인하실 수 있습니다.  
(링크: https://docs.aws.amazon.com/ko_kr/codebuild/latest/userguide/build-spec-ref.html )  

아래 예시는 제가 이번 포스팅에서 사용할 buildspec.yml의 내용입니다.  

```yml
# 버전은 현재, 0.2가 권장사항입니다.
version: 0.2

# 빌드 단계별로 원하는 명령을 입력합니다.
phases:
  # 빌드 전에 필요한 환경을 설치합니다.
  install:
    runtime-versions:
      nodejs: 12
  # 빌드 전에 수행할 명령을 입력합니다.
  pre_build:
    commands:
      - echo Buile Phase >> pre_build phase...
  # 빌드를 수행할 명령을 입력합니다.
  build:
    commands:
      - echo Buile Phase >> Build started on `date`
      - npm install
      - npm run generate
  # 빌드 후에 수행할 명령을 입력합니다.
  post_build:
    commands:
      - echo Buile Phase >> Build completed on `date`
# 빌드 결과물로 나온 아티팩트에 대한 정보를 제공합니다.
artifacts:
  # 빌드 환경에서 빌드 출력 결과물이 생성되는 위치를 나타냅니다.
  # '**/*'는 모든 파일을 재귀적으로 나타냅니다.
  files:
    - dist/**/*
```

### (3) CodeBuild 프로젝트 생성  
이제, AWS CodeBuild console에서 빌드 프로젝트를 생성합니다.  

먼저, console에서 '빌드 프로젝트 생성'을 클릭합니다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image04.JPG?raw=true)  

생성 페이지가 나타나면 아래의 사항들에 값을 입력해줍니다.  
프로젝트 구성 섹션에서는 '프로젝트 이름'을 필수로 입력해주고, 선택적으로 '설명', '빌드 배지'를 설정합니다.  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image05.JPG?raw=true)  

소스 섹션에는 모든 정보를 입력해줍니다. 저는 Github을 소스로 선택하였으며, Github과의 열결을 위하여 OAuth 방식을 사용하였습니다.  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image06.JPG?raw=true)  

OAuth 방식으로 Github에 연결하려면 'Github에 연결' 버튼을 눌러서 새로 뜬 Github에 로그인 창에서 로그인을 해줘야합니다. 로그인을 하고 나면 'Authorize aws-codesuite' 버튼을 눌러서 AWS CodeBuild에서 Github에 접근할 수 있게 허용해줍니다.  

Github과 연결하고 나면 소스 섹션이 아래와 같이 변합니다.  
'내 Github 계정의 리포지토리'를 선택하면 'Github 리포지토리'를 눌렀을 때, 내 Github 리포지토리 목록이 나와서 선택할 수 있습니다.  
목록에서 소스로 사용할 리포지토리를 선택해주세요.  
그리고 '소스 버전' 항목에 저는 release를 입력했습니다. '소스 버전'에 입력하는 버전은 CodeBuild console에서 수동으로 빌드할 때 기본으로 사용할 소스의 버전입니다.  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image07.JPG?raw=true)  

저는 release 브랜치에 PUSH 이벤트가 발생 했을 때 빌드가 실행되게 하기 위해서, '기본 소스 Webhook 이벤트' 섹션에서 이벤트 유형 중에 PUSH를 선택했습니다. 그리고서, '이러한 조건에서 빌드 시작'의 옵션 중에서 'HEAD_REF'에 'refs/heads/release'를 입력했습니다.  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image13.JPG?raw=true)  

환경 섹션에서는 아래 이미지처럼만 설정해줍니다. 기본적인 설정이며, 각자에 맞는 환경이 필요하다면 상황에 맞게 빌드 환경을 설정하시면 됩니다.  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image08.JPG?raw=true)  

Buildspec 섹션에서는 Buildspec을 어떻게 제공할지 설정하는데, 저는 아까 buildspec.yml을 작성하고 프로젝트 루트 디렉토리에 저장해놨습니다. 그래서 'buildspec 파일 사용'을 선택하고 넘어갑니다.  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image09.JPG?raw=true)  

아티팩트 섹션에서는 빌드 결과물을 내보낼 저장소에 대한 정보를 입력합니다.  
저는 Amazon S3에 결과물을 저장할 것이기 때문에 S3를 선택했고, '버킷 이름'은 클릭하면 버킷 리스트가 나타납니다.  
다른 항목들은 필수는 아니기 때문에 저는 입력하지 않았습니다.  

마지막으로 로그 섹션에서도 기본적으로 선택되어 있는 CloudWatch 로그를 선택하고 끝냅니다.  

모든 설정이 완료되면 하단에 있는 '빌드 프로젝트 생성' 버튼을 누릅니다.  


### (4) 빌드  
빌드 프로젝트가 생성되었으니, 빌드를 한번 해봅니다.  
빌드 프로젝트 화면에서 '빌드 시작' 버튼을 누릅니다.  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image10.JPG?raw=true)  

그러면, 빌드 구성을 조금 수정할 수 있는 페이지로 이동하는데, 변경하지 않거나 상황에 맞게 조금 변경하고 '빌드 시작'을 누르면 빌드가 시작됩니다.  

빌드가 진행되면 상태가 '진행 중' 이었다가 완료되면 실패 또는 성공으로 나타납니다!!  

![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image11.JPG?raw=true)  
![](https://github.com/ChanMinPark/TIL/blob/master/image/aws-code-build/image12.JPG?raw=true)  

'기본 소스 Webhook 이벤트' 섹션에 설정이 잘 되었다면, Git 이벤트를 발생시켰을 때도 동일하게 빌드가 진행되는 것을 확인할 수 있습니다.  