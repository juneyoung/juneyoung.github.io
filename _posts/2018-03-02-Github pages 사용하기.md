# Github Pages 사용하기

## 왜 `pages` 를 사용하게 되었나
~~쓰다 날려먹고 처음부터 쓰는 포스트. 하하하하하하하~~ 기존에도 git repository 를 사용하여 [개발 경험을 정리](https://github.com/juneyoung/DEV-INFOS)하고 있었는데 양이 많아지니 좀 블로그처럼 관리하고 싶다는 생각이 들었다. 

주로 결정에 영향을 미친 요인은 아래와 같음
- `md` 문법 사용 가능!
- 소스 리파지토리와 동일한 서비스에서 관리가 가능함
- 호스팅 관리가 필요없음 (자동으로 `{user}.github.io` 가 생성됨)

포스트는 웹에 블로그 생성 이후 포스트 등록과 같은 기본 액션에 대한 설명이 부족한 것 같아 작성하게 되었다. 그래서 ~~귀찮기 때문에~~ `pages repository` 생성하는 법은 과감히 생략했다. 


## 준비물 
### 0. `Ruby` 와 `RVM` 설치하기
로컬 환경을 갖추려면 `Jekyll` 을 사용해야 하고, 얘는 `Ruby` 가 선행 설치되어야 한다.
```
# command not found 가 나도 넘어감. 어차피 없으면 설치할 예정이니까!
$> ruby --version

# RVM(루비 버전 매니저) 을 설치함
$> curl -L https://get.rvm.io | bash -s stable

# Ruby 설치. 18년 03월 최신 버전은 2.5.0 이며 특정 버전이 필요하면 숫자만 바꿔주면 됨
$> rvm install ruby-2.5.0

# 방금 설치한 루비를 디폴트로 등록하기 (권장)
$> rvm --default use 2.5.0
```

### 1. `Jekyll` 설치하기
`pages` 는 `Jekyll` 이라는 프레임워크로 구성되어 있고, `gem` 명령을 이용해 간단히 설치할 수 있다.
```
# 초간단 설치!
$> gem install jekyll
```



## Jekyll 이해하기
Jekyll 은 기본적으로 정해져있는 템플릿이 있다. [기본 디렉토리 구조](http://jekyllrb-ko.github.io/docs/structure/) 를 모르면 개발이나 확장하기 어렵다.

### 0. 설정 파일

`git` 프로젝트 내 최상위에 보이는 `_config.yml` 파일이 `Jekyll` 의 설정 파일이다. 선택한 Theme 에 따라 위치 등이 다를 수 있다. 사용가능한 키워드는 [여기](http://jekyllrb-ko.github.io/docs/configuration/)에 잘 나와있다.

참고로 현재 사이트의 설정은 아래처럼 되어 있다.
```
# _config.yml 의 내부
theme: jekyll-theme-minimal
title: Dev Diary
description: |
  Writing about experiences of web development.
# 
# source: _source
deploy: _deploy
```
- `|`(파이프라인) 은 yml 에서 멀티라인 컨텐츠를 표기할 때 사용한다. 
- `source` 나 `destination` 에서 들고 있는 값은 디렉토리인데, 자동으로 생성되지 않으며 없으면 빌드 시 오류가 난다.
- `source` 가 설정되지 않으면 jekyll 프로젝트의 root(이 경우에는 `{user}.github.io` 디렉토리) 가 참조된다.(소스 변경하고 내용을 옮겨주지 않으면 파일탐색기 처럼 디렉토리 내용을 출력)
- `destination` 이 설정되지 않으면 `_site` 라는 디렉토리에 결과가 생성된다.

### 1. 포스트 등록하기

##### A. 디렉토리 규약

Jekyll 은 쉽게 관리할 수 있지만 그만한 규약이 있다.
- 포스트는 반드시 `_posts` 디렉토리 안에 넣어야 한다.(디렉토리 수동으로 만들어야 함)
- 포스트 파일의 형식은 반드시 `yyyy-MM-dd-{title}.{html/md}` 이어야 함

현재 프로젝트의 `_posts` 는 이렇다
```
# 한글이나 띄어쓰기도 문제없음!
$> ls -al /_posts
total 24
drwxr-xr-x   5 juneyoungoh  staff   160 Mar  4 15:26 .
drwxr-xr-x  13 juneyoungoh  staff   416 Mar  4 16:02 ..
-rw-r--r--@  1 juneyoungoh  staff  3429 Mar  4 15:59 2018-03-02-Github pages 사용하기.md
-rw-r--r--   1 juneyoungoh  staff  1952 Mar  4 14:05 2018-03-02-자주 사용하는 리눅스 명령어.md
-rw-r--r--   1 juneyoungoh  staff  1952 Mar  4 14:05 eng.2018-03-02-Linux-Commands.md
```

##### B. 포스트 내에서 변수 참조
공식 홈페이지의 [포스트 작성](http://jekyllrb-ko.github.io/docs/posts/)에서는 html 에서 사용하는 예를 들고 있어 혹시 md 에서는 안되지 않을까하는 걱정이 들었다. 그런데 MD 에서도 잘되더라. ~~그냥 태그 뺀 거~~

메인에서 포스트 목록 조회하는 부분은 아래처럼 처리할 수 있었다.
```
... 생략 ...
## Posts

{ % for post in site.posts % }
  [ { { post.title } } ]( { { post.url } } )
{ % endfor % }
... 생략 ...
```
`{ %` 문법을 [`Liquid Template` 언어](https://help.shopify.com/Liquid) 라고 부르는 모양. Jekyll 에서 지원하는 리퀴드 문법의 변수는 [여기](http://jekyllrb-ko.github.io/docs/variables/) 참조. 제대로 표기하면 `jekyll build` 오류가 발생해서 공백 넣었음

### 변경 내역 반영하기

github 가이드를 보면 바로 `master` 브랜치에 작업을 하는게 아니라 `gh_pages`라는 브랜치를 따도록 유도한다. 그러므로 현재까지 작업한 모든 내역은 `push` 해도 반영되지 않는다. 아래와 같은 방법으로 처리하면 된다.
1. 로컬에서 작업
2. `git add -A .` > `git commit -m {작업내역}` > `git push`
3. github 리파지토리 페이지에서 `New pull request` 버튼
4. `base:master`, `compare:gh_pages` 로 설정하고 `Create pull request`
5. `Merge pull request`
6. 잠시만 기다리면 반영완료!


## 참고자료
- [OSX 에서 Ruby 설치/업데이트 하기](http://codingpad.maryspad.com/2017/04/29/update-mac-os-x-to-the-current-version-of-ruby/)
- [pages 로컬 개발 환경 갖추기](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/) 
- [pages 공식 홈페이지](https://pages.github.com/)
- [jekyll 한글 페이지](https://jekyllrb-ko.github.io/) 