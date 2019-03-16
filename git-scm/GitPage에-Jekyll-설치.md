### Ruby 설치
1. [ruby download](https://www.ruby-lang.org/en/downloads/)
2. dos command 선택 창에서 [3] - MSYS2 and MINGW development toolchain 을 선택
### git repository 생성 후 local에서 clone
```
D:\BigData\Git>git clone https://github.com/srshin/srshin.github.io.git
```
### jekyll bundler 설치 & version 확인
```
D:\BigData\Git\srshin.github.io>gem install jekyll bundler
D:\BigData\Git\srshin.github.io>jekyll -v
jekyll 3.8.5

```
### 테마 clone
D:\BigData\Git\srshin.github.io>git clone https://github.com/jarrekk/Jalpc.git
###  개발환경에서 확인
서버실행
```
D:\BigData\Git\srshin.github.io>jekyll serve
```
http://127.0.0.1:4000 확인 
### 수정후 git 반영
```
git commit -a -m “comment”
git push -u origin master  (-u option : 로컬 브랜치를 새로 만든 후 원격저장소에 해당 브랜치를 push하고자 할 때) 
```
### admin설치 
```
D:\BigData\Git\srshin.github.io>bundle install
```
http://127.0.0.1:4000/admin


