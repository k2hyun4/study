### GIT?
* 버전관리도구

## GIT - Local 편
### 0. GIT, SourceTree(GIT GUI Client) 설치
* https://git-scm.com/
* https://www.sourcetreeapp.com/

### 1. Local Repository 생성
* GIT : 원하는 폴더로 가서 "git init"
* SourceTree : New tab - Create - Path 및 Name 설정, Create

### 2. Operations
* Untracked
* Unmodified
* Modified
* Staged : commit 대기 상태

### 3. Branch, Checkout
### 4. Merge, Rebase
* Merge : Fast-forward-merge, 3-way-merge
* Rebase : 3-way-merge를 방지하기 위한 수단


## .gitignore 설정 후 적용시키기
```
$ git rm -r --cached .
$ git add .
$ git commit -m "커밋메세지"
```
* [ref : http://theeye.pe.kr/archives/2091](http://theeye.pe.kr/archives/2091)

## refusing to merge unrelated histories
```
$ git pull origin 브런치명 --allow-unrelated-histories
```
* [ref : https://gdtbgl93.tistory.com/63](https://gdtbgl93.tistory.com/63)
