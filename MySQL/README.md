## 계정 암호 변경 방법
* update ~~ set password=password('[패스워드]') where ~~
* 암호화 및 변경됨

## BLOB insert Query
### TRY!
```
  INSERT INTO 테이블명(BLOB 칼럼명) VALUES (LOAD_FILE('파일경로'));
```
* NULL값만 들어감...

### 문제 해결
* 허용된 경로 내 파일만 읽을 수 있도록 하는 설정 존재
* 허용된 경로 확인
```
  SHOW VARIABLES LIKE "secure_file_priv";
```
* 해당 경로에 파일을 복사, 다시 insert
* 경로 입력시 "\" → "/"
