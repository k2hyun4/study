## STS 설치
**1. 작성일 기준 최신 버전인 [STS 3.9.4.RELEASE] 다운로드**
* https://spring.io/tools/sts/legacy.How+to+Download+and+Connect+with+STShow

**2. 압축 해제 후 sts.exe 실행**

## 프로젝트 생성
**1. new -> Spring Starter Project**

**2. Type : Gradle(BuildShip 2.x)**
* 상단에 에러 발생시 Help-Eclipse Marketplace 에서 Buildship Gradle Integration 설치
### Gradle 선택 이유
* Maven을 이용한 웹 프로젝트는 많이 생성해봤고, 
* 아래 글에 혹해서!(지금 시점에서 Gradle을 사용하지 않을 이유는 '익숙함' 뿐인 것 같다.)
* http://bkim.tistory.com/13

**3. 프로젝트명, 패키지명 등 수정 후 [Next]**

**4. Dependencies 추가(매우 편하다!)**
* Web
* MyBatis : Hibernate는 조금 더 공부해보자...(https://github.com/k2hyun4/study/tree/master/persistenceFramework)
* MySQL : Oracle을 많이 써봤기 때문에
* Thymeleaf : SpringBoot에서는 익숙했던 JSP를 공식적으로 지원하지 않으며, Thymeleaf를 밀어 줌
* Lombok : 편하다. Log 쓸 때라든가, Getter, Setter, 생성자를 자동생성 및 안보이게 해줘서 VO의 가독성이 향상

**5. [Finish]**

**6. Run**
* Run As -> SpringBootApp
* DataSource 설정없이 Run 해서 에러 발생
* build.gradle -> dependencies 내 mybatis compile 주석 처리 후 Gradle -> Refresh Gradle Project, 다시 Run

## 프로젝트 설정
### application.yml 생성
* src/main/resources 내 application.properties 삭제, application.yml 파일 생성
* spring boot 의 기본 설정을 변경할 때 활용
* spring boot에서 resource 하위의 .yml, .properties 파일을 읽어들임
* 가독성 면에서 yml >> properties

### thymeleaf 실시간 적용 설정
* resources/application.yml

```
  thymeleaf:
    cache: false
```

### Resource 폴더 생성
**1. resources**
* 기본 설정 파일(application.yml, mybatis-config.xml 등)
* index.html : 기본 url로 접근시 별도의 매핑이 없으면 index.html을 호출

**2. resources/templates**
* 일반적인 view 위치(html). controller에서 return 시 자동 prefix, suffix를 통해 호출됨

**3. resources/static**
* 정적 리소스 관리
* 이번 프로젝트에서는 js/css/img 폴더 생성하여 관리하자

**4. resources/mapper**
* Mybatis Mapper.xml 

## 기본 구현
### 컨트롤러
```@Controller``` : 컨트롤러 클래스 명시

```@Log``` : Lombok 라이브러리에서 제공하는 Log 활용

``` @Autowired``` : DAO클래스 의존성 주입

```@GetMapping, @PostMapping``` : url mapping

### VO
```@Getter, @Setter``` 활용

### DAO
* Interface

```@Repository``` : 의존성 주입을 위해 필요

``` @Mapper``` : 매퍼 선언

### db 세팅
**1. mysql 접속정보**
* resource/application.yml에 선언

```
spring:
  datasource: 
    driverClassName: com.mysql.jdbc.Driver
    url: jdbc:mysql://[url]:[포트]/[데이터베이스명]?useSSL=false&allowPublicKeyRetrieval=true 
    username: [아이디]
    password: [패스워드]
```

```useSSL=false``` : Logger에 자꾸 빨간 글씨로 ssl 사용하라고 뜨는 것 방지

```allowPublicKeyRetrieval=true``` : [java.sql.SQLNonTransientConnectionException: Public Key Retrieval]
* 해당 오류 방지용

**2. Mybatis설정**
* resources/application.yml에 선언

```
mybatis: 
  config-location: classpath:mybatis-config.xml 
```

* Mybatis 설정파일 생성(resources/mybatis-config.xml)

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
	<typeAliases>
		<package name="[값 클래스 fullname]"/>
	</typeAliases>
	<mappers>
		<mapper resource="[mapper xml 파일 경로]"/>
	</mappers>
</configuration>
```

* mapper.xml 설정

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="[@Mapper 적용한 DAO클래스 fullname]">

</mapper>
```

## Runnable jar 생성하기
* Spring boot에서는 war 대신 내장톰캣을 활용하는 Runnable jar 존재

**1. build.gradle 설정**

```
jar {
	manifest {
		attributes 'Main-Class': '[main method가 존재하는 클래스 fullname]'
	}
	archiveName '[생성될 jar명]'
	
  //library 포함시키기 위한 구문
	from {
		configurations.compile.collect {
			it.isDirectory() ? it : zipTree(it)
		}
	}
}
```

**2. jar 생성**
* Window -> Show View -> Gradle Tasks 활성화
* build/build or jar 실행
* [프로젝트경로]/build/libs 에 생성됨

**3. Runnable Jar 실행**
* cmd 활성화
* java -jar [runnable 자바 경로 및 파일명]