# 모두의 연구소 바이오메디컬랩 블로그

바이오메디컬랩 블로그에는 다음 스택으로 구성되어 있습니다.

- [GitHub Pages](https://pages.github.com/): GitHub에서 정적 웹사이트를
    호스팅해주는 서비스
- [Jekyll](https://jekyllrb.com/): 정적 웹사이트 제작 도구
- [Jasper2](https://github.com/jekyller/jasper2): Jekyll 테마

정적 웹사이트란, 웹서버에 별도의 DB 및 콘텐츠 관리 프로그램(CMS) 없이,
순수한 HTML 웹 문서로만 구성된 홈페이지입니다. 콘텐츠를 관리해주는 프로그램이
따로 없으므로, 새로운 내용을 올릴 때마다 소스코드에서 다시 웹 문서를 컴파일하는
방식으로 최신화해야 합니다.

## 설치

Ubuntu 16.04 기준입니다.

### 1. 준비사항

Ruby 버전 2.1.0 이상이 필요합니다.

~~~bash
$ sudo apt-get install ruby ruby-dev dh-autoreconf
$ ruby --version
ruby 2.X.X
~~~

Bundler를 설치합니다.

~~~bash
$ gem install bundler
~~~

NPM 및 Gulp를 설치합니다.

~~~bash
$ sudo apt-get install npm
$ sudo ln -s /usr/bin/nodejs /usr/bin/node
$ sudo npm install gulp-cli -g
$ sudo npm install gulp -D
~~~

### 2. 소스 및 빌드 준비

새 디렉토리를 만듭니다.

~~~bash
$ mkdir blog
$ cd blog
~~~

소스 및 빌드 브랜치를 각각의 디렉토리로 가져옵니다.

~~~bash
$ git clone https://github.com/modulabs-biomedical.github.io --branch source src
$ git clone https://github.com/modulabs-biomedical.github.io --branch master build
~~~

소스 디렉토리로 이동하여 플러그인들을 설치해줍니다.

~~~bash
$ cd src
$ bundle install
$ npm install
~~~

### 3. 로컬 환경에서 사이트 확인

드디어 준비가 끝났습니다. 사이트를 보기 위해 임시 서버를 실행합니다.

~~~bash
$ bundle exec jekyll serve
~~~

http://127.0.0.1:4000에서 사이트를 확인할 수 있습니다.

### 4. 새로운 게시글 입력

이미지는 `assets/images`에, 게시글은 `_posts`에 넣어주고, 다시 임시 서버를
실행하여 잘 적용되었는지 확인합니다.

### 5. 변경사항 업로드

변경사항을 빌드합니다.

~~~bash
$ bundle exec jekyll build
~~~

`assets/css` 내의 파일을 변경한 경우 스타일을 다시 컴파일해야 합니다.

~~~bash
$ gulp
~~~

원하는 결과를 얻었다면 변경점들을 git에 commit하고 push합니다.

~~~bash
$ git add --all
$ git commit -m '새 게시글 등록'
$ git push origin source
~~~

빌드된 결과물도 동일하게 commit 및 push합니다.

~~~bash
$ cd ../build
$ git add --all
$ git commit -m '새 게시글 등록'
$ git push origin master
~~~
