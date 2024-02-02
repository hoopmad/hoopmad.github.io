---
title: GitHub Pages로 Jekyll 블로그 만들기.part1
date: YYYY-MM-DD HH:MM:SS +09:00
categories: [Blog, Git, Programming]
tags: [blog, github, ruby, jekyll, chirpy] 
img_path: /assets/img/blog_screenshots/
---

*👋안녕하세요, 훕마드입니다.*

## 왜 깃허브 블로그인가
**깃허브**(GitHub)는 소프트웨어 프로젝트를 함께 작업하고 공유하는 플랫폼입니다. 개발 분야를 공부했거나 개발자와 협업한 경험이 있다면 들어본 기억이 있을거에요. 깃허브는 코드를 공유하는 것 외에도 **깃허브 페이지**(GitHub Pages)를 통해 웹사이트를 호스팅 기능을 제공합니다. 최근엔 이걸 활용해 기술 블로그를 운영하는 사용자도 많이 있습니다. 물론 네이버, 티스토리, 벨로그 등 다양한 선택지가 존재하지만 특별히 개발자라면 깃허브로 시작하는 걸 추천합니다.

본격적으로 블로그 만들기 전에 제가 깃허브를 선택한 이유 3가지를 먼저 소개할게요.

### ✅장점 1_ 일단 멋있다.
기록을 위해 블로그를 작성하기도 하지만 많은 사람들이 보면 더 좋겠죠. 이때 흔한 플랫폼이 아닌 커스텀된 사이트라면 아무래도 더 눈길이 가기 마련입니다.
### ✅장점 2_ 포스팅만 해도 잔디를 심는다.
깃허브 저장소에 푸시(push)하는 방식으로 포스팅하므로 커밋이 필수입니다. 글만 올려도 프로필을 초록초록하게 만들 수 있습니다.

### ✅장점 3_ 에러와 함께 성장한다.
이런저런 수정을 하다 보면 에러를 마주할 수밖에 없습니다. 이 글을 쓰는 이유도 전에 만들었던 블로그 업데이트가 어려워 다시 배우며 수정하고 싶어서입니다. 가끔 블로그를 하는지 프로그래밍하는지 헷갈릴 수 있지만 미래에 성장할 자신을 상상하면서 같이 시도해 보면 좋겠습니다.

**✨아래는 완성된 블로그의 예시입니다.**
![example_1](example_1.png)
_최종 블로그 화면_

## 사전 준비
1. GitHub 계정
2. Git
3. 제일 좋아하는 소스코드 편집기
4. Ruby
5. Jekyll

시작하기에 앞서 몇 가지 준비가 필요합니다. 먼저 깃허브 계정이 필요하고, Git이 설치되어 있어야 합니다. 선호하는 소스코드 편집기를 준비해 주세요. 저는 편집도 가능하고 Git Bash 터미널을 쓸 수 있는 VS Code를 좋아합니다.

❗ **<span style="color:red"> 모든 설명은 윈도우 10을 기준으로 합니다. </span>**

### Ruby 설치
사실 개발 지식이 있더라도 웹페이지를 처음부터 만드는 일은 귀찮죠. 그래서 이미 뛰어난 개발자가 만들어 둔 블로그에 특화된 페이지를 쉽게 만들어주는 Jekyll을 사용합니다. 그리고 Jekyll은 Ruby라는 프로그래밍 언어로 만들어져 있어요. 걱정하지 마세요. Ruby를 공부하지 않아도 괜찮습니다. 몰라도 할 수 있습니다. 어렵지 않으니 멋진 블로그를 향해 같이 가시죠!

![ruby_1](ruby_1.png)
_Ruby 다운로드 페이지_

[여기](https://rubyinstaller.org/downloads/){:target="_blank"}로 접속해 가장 WITH DEVKIT 아래 첫 번째 파일을 다운받으면 됩니다. 간혹 32bit를 설치하라는 글도 보이지만 챗GPT에 확인 결과 사용하는 OS에 맞게 설치하는 게 좋다고 하네요.

![ruby_2](ruby_2.png)
_친절한 GPT씨_

설치는 특별한 설정 없이 쭉 진행하시고 Setup 마지막 단계에서 <span style="color:red; background-color:#FFE6E6"> Run 'ridk install'</span> 박스가 체크 되어 있는지 확인하고 Finish를 눌러주세요.

![ruby_3](ruby_3.png)
_체크박스 확인 후 Finish_

그러면 아래와같이 새로운 cmd 창이 열립니다. 어떤 컴포넌트를 설치할 거냐 물어보는데 저희는 확실하지 않으니, Enter를 누를게요.
![ruby_4](ruby_4.png)
_unsure할 때마다 엔터를 누를 수 있다면 좋겠다_

아래와 같은 라인이 나오면 설치가 완료되었으니, 창을 닫아주세요.
```
Install MSYS2 and MINGW development toolchain succeeded
```

터미널에 Ruby 버전과 환경 변수 설정을 확인합니다.
```bash
ruby -v
```

### Jekyll 설치
Ruby가 문제없이 설치됐다면 Jekyll과 더불어 Ruby 프로젝트 관리를 도와주는 Bundler도 설치해 줍니다. 아래처럼 명령어로 간단하게 추가할 수 있어요.

```bash
gem install jekyll bundler
```
아래 명령어로 Jekyll과 Bundler가 잘 작동하는지 확인합니다. 혹시 command not found 에러가 나온다면 터미널을 다시 실행해 주세요.

```bash
jekyll -v

bundler -v
```

## GitHub Fork로 로컬 저장소 생성
> 이 방법으로 진행하면 푸시를 해도 깃허브 프로필에 커밋이 반영되지 않는 이슈가 있습니다. [기여가 프로필에 표시되지 않는 이유](https://docs.github.com/ko/account-and-profile/setting-up-and-managing-your-github-profile/managing-contribution-settings-on-your-profile/why-are-my-contributions-not-showing-up-on-my-profile#common-reasons-that-contributions-are-not-counted)를 확인해보면 fork 로 생성된 저장소는 pull request를 통해 부모 저장소에 merge가 완료되어야 한다네요. 해당 내용은 따로 다루도록 하겠습니다.

Jekyll 블로그는 다양한 테마가 존재합니다. 그중 심플하면서도 예쁜 "Chirpy" 테마를 사용할 거에요. 모든 설명은 해당 테마의 [공식 문서](https://chirpy.cotes.page/posts/getting-started/)를 기반으로 했습니다.

링크를 열면 Installation 파트에 사이트를 설정하는 두 가지 방법이 나옵니다. Chirpy Starter는 빠른 적용이 가능한데 커스텀에는 제약이 있어요. Fork를 하면 업그레이드가 어렵지만 수정이 자유롭습니다. 지난 블로그는 Starter를 사용했는데 나중에 스타일을 수정할 수도 있기 때문에 Fork로 저장소(Repository)를 만들겠습니다. [GitHub Fork 링크](https://github.com/cotes2020/jekyll-theme-chirpy/fork)로 접속해 주세요.

Fork 하는 페이지에서 USERNAME 부분에 자신의 깃허브 사용자명을 넣으면 됩니다. Description은 블로그에 대한 설명을 자유롭게 작성하거나 일단은 빈칸으로 남겨도 좋아요.

![fork_page](fork_page.png)
_fork 설정_

Create fork를 누르고 아래와 같이 페이지가 생성됐다면 성공입니다!

![forked](forked.png)
_새롭게 생성된 레퍼지토리_

이제 컴퓨터에 저장소를 clone 합니다. Code를 눌러 나오는 Git 저장소 주소를 복사합니다.

![clone](clone.png)
_주소 복사_

원하는 위치에 폴더를 만들고 콘솔 창으로 접근합니다. 저는 D 드라이브에 blog 폴더를 만들었어요. 그리고 콘솔 창에 아래 명령어를 입력하면 로컬 저장소가 생성됩니다.

```bash
git clone https://github.com/USERNAME/USERNAME.github.io.git
```

**깃허브에 블로그를 올리기 위한 준비와 로컬 저장소를 생성하는 것까지 진행해 봤습니다.
다음 포스팅에서 초기 설정 후 테마 적용으로 돌아올게요!**