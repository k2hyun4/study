## 특징

### 1. 경량 컨테이너
*  자바 객체를 관리함

### 2. POJO 방식
* Plain하고 Old한 Java Object
* ↔ EJB(Enterprise Java Bean)
* EJB is Too Much!
  
### 3. IoC, DI
* 

### 4. AOP 지원
* Aspect-Oriented Programming
* 로깅, 보안, 트랜잭션 등 공통적으로 쓰이는 기능들을 분리, 개발하고 실행 시에 서로 조합할 수 있도록 함

### 5. 확장성, 영속성

## 컨테이너
* 인스턴스의 Life Cycle을 관리, 추가 기능 제공

### 종류

**1. BeanFactory**
* getBean()이  호출되어야 빈 생성

**2. Application Context**
* 애플리케이션 기동 후 미리 빈 생성

## 주요 모듈
* 제어 반전 컨테이너
* 관점 지향 프로그래밍 프레임워크
* 데이터 엑세스 프레임워크
* 트랜잭션 관리 프레임워크
* 모델-뷰-컨트롤러 패턴
* 배치 프레임워크
