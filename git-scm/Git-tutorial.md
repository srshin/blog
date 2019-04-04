## git 설치
https://git-scm.com/

### 전역 사용자 설정
```
git config --global user.name “Your name”  
git config --global user.email “Your email address”  
```
### 저장소별 사용자 설정
```
git config user.name “Your name”   
git config user.email “Your email address”  
```
### 조회
```
D:\BigData\Git\GitTest>git config --global --list
user.name=srshin
user.email=sangrimshin@gmail.com
difftool.sourcetree.cmd='C:/Program Files/KDiff3/kdiff3.exe' "$LOCAL" "$REMOTE"
mergetool.sourcetree.cmd='C:/Program Files/KDiff3/kdiff3.exe' "$BASE" "$LOCAL" "$REMOTE" -o "$MERGED"
mergetool.sourcetree.trustexitcode=true
```
## Repository 만들기[1] 수동 : local에서 생성해서 수동으로 가져오는 방법   
### folder 생성
```
D:\BigData\Git>mkdir gitTutorial
D:\BigData\Git>cd gitTutorial
```
### git init: .git 생성 (repository)
```
D:\BigData\Git\gitTutorial>git init
Initialized empty Git repository in D:/BigData/Git/gitTutorial/.git/
D:\BigData\Git\gitTutorial>dir /a
2019-03-14  오후 12:46    <DIR>          .
2019-03-14  오후 12:46    <DIR>          ..
2019-03-14  오후 12:46    <DIR>          .git
```
### add remote repository
```
D:\BigData\Git\local>git remote add  origin https://github.com/srshin/bigdata.git
```
### remote 저장소에서 데이터 가져오기 
fetch : 자동으로 merge하지 않음.   
```
D:\BigData\Git\local>git fetch origin
remote: Enumerating objects: 67, done.
remote: Counting objects: 100% (67/67), done.
remote: Compressing objects: 100% (49/49), done.
remote: Total 67 (delta 9), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (67/67), done.
From https://github.com/srshin/bigdata
 * [new branch]      master     -> origin/master
```
pull : 자동 merge까지 수행
## Repository 만들기[2] 자동 : clone remote (folder생성 및 가져오기까지 자동으로)   
```
D:\BigData\Git\gitTutorial>git clone https://github.com/srshin/bigdata.git
Cloning into 'bigdata'...
remote: Enumerating objects: 67, done.
remote: Counting objects: 100% (67/67), done.
remote: Compressing objects: 100% (49/49), done.
remote: Total 67 (delta 9), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (67/67), done.
```
## remote 저장소 확인하기 
```
D:\BigData\Git\bigdata>git remote
origin

D:\BigData\Git\bigdata>git remote -v
origin  https://github.com/srshin/bigdata.git (fetch)
origin  https://github.com/srshin/bigdata.git (push)
```
## local 관리 
### git status
```
D:\BigData\Git\bigdata>git status
On branch master
Your branch is up to date with 'origin/master'.
nothing to commit, working tree clean
```
### add new file : UNSTAGE  -> STAGED state
```
D:\BigData\Git\bigdata>git add  new.md
D:\BigData\Git\bigdata>git status
On branch master
Your branch is up to date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
        new file:   new.md
```
### git commit
```
D:\BigData\Git\bigdata>git commit -m "first commit by commandline"
[master 9e71888] first commit by commandline
 1 file changed, 4 insertions(+)
 create mode 100644 new.md
```
* commit과 add를 동시에
```
D:\BigData\Git\bigdata>git commit -a -m "first commit by commandline"
[master e02b4bf] first commit by commandline
 1 file changed, 2 insertions(+), 1 deletion(-)
```
### .gitignore 
git folder에 있으나 관리하지 않을 파일들 정의
### diff
```
working directory :   
D:\BigData\Git\bigdata>git diff
staging area : 
D:\BigData\Git\bigdata>git diff --staged
```
## remote 관리 
### remote에 파일 올리기
```
D:\BigData\Git\bigdata>git push origin master
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 4 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 585 bytes | 292.00 KiB/s, done.
Total 6 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 1 local object.
To https://github.com/srshin/bigdata.git
   d86613a..e02b4bf  master -> master
```
### remote 저장소 확인
```
D:\BigData\Git\bigdata>git remote show origin
* remote origin
  Fetch URL: https://github.com/srshin/bigdata.git
  Push  URL: https://github.com/srshin/bigdata.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
```
## Branching
### 현재 branch확인
```
D:\BigData\Git\bigdata>git branch
* master
  test01
D:\BigData\Git\bigdata>git branch -v
* master 93914b2 [ahead 1] branch test
  test01 93914b2 branch test
```
### make a branch
```
D:\BigData\Git\bigdata>git branch test01
```
### switch to a branch
```
D:\BigData\Git\bigdata>git checkout test01
Switched to branch 'test01'
```
### branch 만들면서 동시에 switch 
```
$ git checkout -b iss53
Switched to a new branch "iss53"
```
### 변경사항 commit
```
D:\BigData\Git\bigdata>git commit -a -m "branch test"
[test01 93914b2] branch test
 1 file changed, 2 insertions(+), 1 deletion(-)
```
### switch to master
```
D:\BigData\Git\bigdata>git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
```
### LOCAL BRANCH merge
```
D:\BigData\Git\bigdata>git merge test01
Updating e02b4bf..93914b2
Fast-forward
 new.md | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```
### REMOTE BRANCH merge
1. fetch remote. Do NOT pull remote (pull = fecth + merge, NOT recommended)[Refer to git tutorial](https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%A6%AC%EB%AA%A8%ED%8A%B8-%EB%B8%8C%EB%9E%9C%EC%B9%98)
```
D:\BigData\Git\bigdata>git fetch
```
2. branch확인 
```
D:\BigData\Git\bigdata>git branch -vv
* master 93914b2 [origin/master] branch test
  test01 93914b2 branch test
```
3. merge remote branch
```
git merge origin/serverfix 
```
