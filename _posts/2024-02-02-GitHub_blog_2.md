---
title: GitHub Pages로 Jekyll 블로그 만들기.part2
date: 2024-02-02 11:00:00 +0900
categories: [Blog, Git, Programming]
tags: [blog, github, ruby, jekyll, chirpy] 
img_path: /assets/img/blog_screenshots/
---

**👋안녕하세요, 훕마드입니다.**

지난 포스팅에서 Chirpy 테마의 원격 저장소를 clone 하고 컴퓨터에 생성하는 것까지 다뤘는데요. 이제 로컬에서 페이지를 설정해 구동하고 깃허브 서버에 배포까지 진행하겠습니다.

## 환경 설정
생성한 디렉토리로 이동하면 이미 많은 파일이 생성되어 있습니다. 처음 구동 시 환경 설정을 도와주는 init 파일이 'tools' 폴더 안에 있어요. 만약 PC에 Node.JS가 설치 되어 있다면 다음 명령어를 실행하면 됩니다. 저는 VS Code에서 git bash 터미널을 사용했어요.
```bash
tools/init
```

실행 후 아래 문구가 나온다면 성공입니다!
```
[INFO] Initialization successful!
```

다음은 Dependency 설치입니다. 의존성이라고 번역되는데 쉽게 말해 하나의 소프트웨어나 프로그램이 정상적으로 작동하기 위해 필요한 다른 소프트웨어, 라이브러리, 또는 모듈을 의미합니다. 예전엔 일일이 설치해야 했다면, 그 과정을 간단하게 해주는 기술이죠. 아래 명령어를 실행하면 블로그 실행 준비가 완료됩니다.
```bash
bundle
```
다음 명령어로 로컬 서버에서 블로그를 구동할 수 있어요. 접속 주소는 '127.0.0.1:4000' 입니다.
```bash
bundle exec jekyll serve
```

## 기본 정보 수정
좋아요! 이제 블로그를 수정해 배포하는 일만 남았네요.

루트 폴더의 _config.yml 파일을 열어줍니다. 아래 표는 제가 수정한 내용입니다. 참고해서 원하는 만큼 수정해 주세요.

| 변수 | 값 | 설명 |
| :-- | :-- | :-- |
| timezone | Asia/seoul | 시간대를 서울로 설정합니다. |
| title | Hoopmad | 블로그 메인에 표시되는 제목입니다. |
| tagline | I like to code and hoop. | 블로그에 대한 짧은 설명이나 인사말을 적어주세요. |
| description | Featuring various topics ... AI. | 검색엔진 최적화(SEO)와 관련이 있다는데 저는 일단 마음대로 적었습니다. 추후 다듬을 계획입니다. |
| url | "https://hoopmad.github.io" | 블로그 주소가 될 url입니다. 원격 저장소 이름과 같게 설정해주세요. |
| github | hoopmad | 깃허브 아이디를 적어주세요. |
| twitter | hoopmad_ | 트위터 아이디를 적어주세요. |
| social.name | Hoopmad | 글의 작성자와 저작권에 나타날 이름입니다. 저는 아이디와 같게 설정했어요. | 
| social.email | hoopmad22@gmail.com | 이메일 주소를 적어주세요. | 
| social.links | - https://twiiter.com/hoopmad_<br> - https://github.com/hoopmad |  | 
| theme_mode | [dark] | 블로그의 테마를 정합니다. 한 가지를 선택하면 고정됩니다. 주석 처리된 상태로 두면 사용자의 시스템 테마에 맞춰집니다. | 
| avatar | assets/img/profile.png | 프로필 이미지를 등록할 수 있어요. 해당 위치에 파일을 저장하면 됩니다. |

배포 전 로컬 서버를 구동해 수정 사항이 있는지 확인해 주세요.
```bash
bundle exec jekyll serve
```

## 페이지 배포
👏이제 마지막 단계입니다. [공식 Wiki](https://chirpy.cotes.page/posts/getting-started/){:target="_blank"}에서는 Pages 설정을 Github Actions로 변경 후 푸시하라고 나오는데 기본 설정인 **Deploy from a branch**에서 진행해야 오류 없이 배포되네요.

터미널에서 변경 사항을 커밋하고 푸시를 해볼게요.

```bash
git add .

git commit -m "initial settings"

git push
```

원격 저장소의 Actions 탭으로 이동 수 커밋 이름을 클릭하면 빌드되는 과정을 확인할 수 있어요.

![deploy_2](deploy_2.png)
_빌드 시작_

![deploy_3](deploy_3.png)
_빌드 완료 후 배포 시작_

아래와 같이 초록색 체크 표시가 나오면 배포까지 성공입니다! 바로 적용되지는 않고, 5-10분 정도 후에 사이트에 접속하면 됩니다.

![deploy_4](deploy_4.png)
_배포 완료_

URL로 접속해 블로그가 나오면 성공입니다! 깃허브 블로그 오픈을 축하합니다!🎉🎉
![example_2](example_2.png)
_최종 배포된 블로그 홈_

> **2월 15일 수정 사항**
>
> 원격 저장소의 Actions 탭으로 들어가면 *pages build and deployment*가 실행된 것을 볼 수 있는데요. 실행 로그를 확인해 보면 푸시할 때마다 빌드를 두 번 진행하게 됩니다. GitHub Actions로 설정을 변경해 한 번만 실행되도록 해줄게요.
>
> 초기 배포가 완료되면 깃허브 원격 저장소로 접속해 Settings 페이지로 이동해주세요. 왼쪽 사이드바에서 Pages 메뉴를 선택하면 아래와 같은 창이 나옵니다. Source 드롭다운 메뉴에서 GitHub Actions를 선택해 주세요. 이제 커밋을 깃허브로 푸시하면 Actions workflow가 실행되면서 자동으로 빌드 및 배포가 이루어져요.
>
> ![deploy_1](deploy_1.png)
_Pages에서 Actions 선택_

## 마치며

복잡한 여정을 함께해주셔서 감사합니다. 꼭 필요한 설명만 담았기 때문에 진행하며 막히는 부분이 나올 수 있습니다. 댓글로 오류를 남겨주시면 해결 방법을 같이 연구해 보겠습니다.

감사합니다.
