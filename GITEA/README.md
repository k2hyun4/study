## gitea?
* for window git 서버 구축
* gitlab : linux용

## gitea 설치하기
* download : https://dl.gitea.io/gitea/
* exe 실행 --> http://localhost:3000으로 접속(default값)
* database : mysql은 오류가 발생하여,,, SQLite 활용
* gitea.exe가 있는 폴더\custom\conf\app.ini 에서 설정 변경 가능

* ref : http://juicyjusung.blogspot.com/2018/05/gitea.html

## https 설정
### 인증서 받기
* LetsEncrpyt-win-simple
* https://github.com/k2hyun4/study/blob/master/LetsEncrypt/README.md

### setting
```
 PROTOCOL = https
 ROOT_URL = https://도메인
 DISABLE_SSH = false
 SSH_PORT = 22
 CERT_FILE = crt.pem 경로
 KEY_FILE = key.pem 경로
```

## User 생성 및 권한 부여
### 1. User 생성

**command line 활용**
* gitea admin create-user --name [사용자명] --password [비밀번호] --email [메일주소]
* ref : https://docs.gitea.io/en-us/command-line/

**GUI 활용**
* gitea 메인 화면 우측 상단 메뉴 - Site Administration - User Accounts 활용

### 2. Collaborators 설정
* repository - 설정 - Collaborators 검색(사용자명) 후 쓰기 권한 주기
