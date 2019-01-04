# Persistence Framework
* 말 그대로 데이터의 지속성을 유지해주기 위한 프레임워크
## 종류
* SQL Mapper(Ex : MyBatis)
* ORM(Object-Relational mapper)(Ex : Hibernate)

# JPA? Hibernate?
* http://victorydntmd.tistory.com/195
## JPA
* Java Persistent API
* 자바 ORM 기술에 대한 API 표준 명세(인터페이스)
* JPA를 구현한 것이 Hibernate, EclipseLink, DataNucleus 등

## Hibernate
* 보다 객체지향적, 생산성이 높으며 유지보수에 편리하다고 함
* 복잡한 쿼리가 필요한 경우 한계가 있으며, 잘 모르고 쓰면 성능 문제가 존재

# Mybatis
## if문 주의사항
* 조건문에 쓰이는 값은 무조건 getter가 필요
* String, Boolean 등의 단일 파라미터는 VO나 Map에 담아서 보내야 함
* 기본 파라미터 : value

## BLOB SELECT하기
```
  <resultMap id="아무거나" type="hashmap">
    <result column="컬럼명" property="프로퍼티 아무거나" jdbcType="BLOB" javaType="[B"/>
  </resultMap>
  
  <select id="아이디" resultMap="아무거나">
    SELECT ~~~
  </select>
```
* Map<String, Object>로 받아서, "프로퍼티 아무거나" 로 가져오면 끝!(return byte[])
* ref : http://machunroo.tistory.com/entry/mybatis-byte-array-insert
