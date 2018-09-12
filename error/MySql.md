## Connection Error
### 1. MySQLNonTransientConnectionException 에러 발생

* DriverManager.getConnection(url, id, pw)시에 NullPointerException..?

### 2. 에러 해결하기

* 교재에서 제공해주는 connector.jar의 버전은 5.1.26
* 내가 설치한 MySQL 버전은 8.0이라 맞는 버전의 connector로 대체
* https://mvnrepository.com/artifact/mysql/mysql-connector-java/8.0.11


### 3. **SQLException 에러 발생**
* The server time zone value '´ëÇÑ¹Î±¹ Ç¥ÁØ½Ã' is unrecognized or represents more than one time zone

### 4. 에러 해결하기
* url 정보에 time zone 정보를 추가
* jdbc:mysql://{ip}/{db명}**?serverTimezone=UTC**

## Function DETERMINISTIC ERROR(1418)
* FUNCTION 생성 중 발생
* show global variables like 'log_bin_trust_function_creators'; 확인
* VALUE가 'OFF'일 경우 
* SET GLOBAL LOG_BIN_TRUST_FUNCTION_CREATORS = 'ON';
