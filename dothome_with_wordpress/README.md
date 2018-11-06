## 닷홈(무료호스트)에서 생성한 WordPress 자체호스팅에 설정하기

### 0. Why?
* 자택 근무 중... 디자이너가 홈페이지를 제작해야 함
* 워드프레스로 만드는게 편하다고 함...(뭐가 편한지 모르겠지만)
* dothome.co.kr 에서 무료호스팅을 신청하여 자체 작업 후...
* 자택 근무 종료 후 사무실 서버에 호스팅해주기로 함

### 1. 닷홈 호스팅 생성하기
1.1 dothome.co.kr 계정 생성 및 로그인

1.2 웹 호스팅 - 무료 호스팅 - WordPress UTF-8(한글) 신청하기

1.3 우측 상단 마이닷홈 클릭하여 호스팅 확인

1.4 편한 작업........(?)

### 2. 닷홈 정보 및 자료 백업하기
2.1 마이닷홈 화면에서 원하는 호스팅 상세보기 선택

2.2 FTP 및 DB의 ID/PW 확인(호스팅 신청시 입력했던 정보들...)

**DB 백업**

2.3 [2.1] 화면에서 [MySQL 관리(UTF-8)] 주소 접속 및 로그인

2.4[내보내기] 선택 후 퀵 실행 - .sql 파일 다운로드 완료!

**파일 백업**

2.5 [2.1] 화면에서 웹서버 아이피 확인

2.6 ftp 프로그램 설치(ex : FileZilla)

2.7 ftp 접속(ftp://[웹서버 아이피]) (id/pw : [2.2]에서 확인)

2.8 html 하위 파일 전부 다운로드

### 3. AutoSet 설치
* AutoSet : Apache 서버, PHP, MySQL 설정을 GUI로 제공해주는 프로그램 중 하나

3.1 설치파일 다운로드(https://sourceforge.net/projects/project-autoset/)

3.2 설치
* MySQL도 설치 권장함(Word Press는 테이블 접속 로직이 존재... 기존 설치된 MySQL이 있어도 환경이 다르면ㅠㅠ)

3.3 [설정] - [오토셋 설정] - [오토셋 설치 정보] 에서 MySQL Root ID/PW 확인(기본값 : root/autoset)

3.4 MySQL 설치 폴더 경로도 확인

3.5 웹서버, MySQL 시작
* 오류시 포트 확인(웹서버 : 80, MySQL : 3306. 기존 서비스가 사용중이면 시작 안됨)

### 4. 파일 및 DB 설정

**파일 Set**

4.1 AutoSet [제어] - [홈 디렉토리 열기] 에 [2.8] 결과물 복사 후 웹 서버 재시작

**DB 설정**

4.2 AutoSet [제어] - [phpMyAdmin 접속] 후 로그인(ID/PW : [3.3] 참고)

4.3 [가져오기] 선택 후 [2.4] 결과 파일 선택

4.4 CMD 실행 후 설정
```
cd [3.4]\bin //해당 폴더로 이동
mysql -u [Root ID] -p //Root 권한으로 접속. [3.3] 참고
Enter Password :    //[3.3] 참고해서 PW 입력
show databases;   //현재 데이터베이스 확인. 닷홈 호스팅명과 동일한 데이터베이스 명이 존재해야 함
use mysql;
create user [userID]@localhost identified by '[userPW]';  //[2.2] 와 동일한 ID/PW 사용
use [닷홈 호스팅 데이터베이스명];
grant all on [데이터베이스명].* to [userID]@localhost; //권한 부여
exit  //설정 완료. 확인 절차 시작
mysql -u [userID] -p
Enter Password :
use [데이터베이스명];
select 문 날려보기 성공하면 완료
```

4.5 AutoSet에서 MySQL 재시작

### 5. 완료
* 브라우저에서 localhost 로 접속하여 확인~


## AutoSet Https 적용하기
### 0. 사전작업
* 포트 인바운드 설정, ssl 인증받아 crt.pem, key.pem 받기(ex: use letsencrypt)

### 1. 매니저 설정
* [설정] - [웹서버 세부 설정] - [웹서버 모듈 관리] : mod_ssl.so 체크 후 확인
* [설정] - [PHP 세부 설정] - [PHP 확장모듈 관리] : php_openssl.ddl 체크 후 확인
* [설정] - [웹서버 세부 설정] - [가상 호스트 설정] : 주도메인, 홈디렉토리, 관리자 메일 입력

### 2. [AutoSetHome]\server\conf\httpd.conf 설정
* 경로 : [AutoSetHome]\server\conf\httpd.conf
* Listen [port] 밑에 Listen [ssl port] 추가

### 3. httpd-vhosts.conf 설정
* 경로 : [AutoSetHome]\server\conf\extra\httpd-vhosts.conf
* 내용 추가
```
<VirtualHost *:[ssl port]>
	ServerName domain.com
	ServerAlias www.domain.com
	ServerAdmin [관리자 메일]
	DocumentRoot [port의 DocumentRoot와 동일하게]
	ErrorLog logs/domain.com-error_log
	CustomLog logs/domain.com-access_log common
	<Directory />
	Options FollowSymLinks
	AllowOverride FileInfo
	Require all granted
	</Directory>
	SSLEngine on
	SSLCertificateFile [crt.pem 경로]
	SSLCertificateKeyFile [key.pem 경로]
	SSLProtocol all
	SSLCipherSuite HIGH:MEDIUM
</VirtualHost>
```

* ref : http://amina.co.kr/bbs/board.php?bo_table=tip&wr_id=3844
