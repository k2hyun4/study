## 람다표현식(Lambda Expression)
* 익명함수를 활용하기 위한 표현식
* 함수형 프로그래밍 방식에 기반

### 형태
* (parameters) -> expression
* (parameters) -> {statements;}

### 람다 캡쳐(Lambda Caputuring)
* final 속성인 변수 활용 가능


## forEach
```
Map<String, String> map;    //값 들어갔다고 가정
map.forEach((key, value) -> {
  Sytem.out.println(key);
  Sytem.out.println(value);
});
```

## 함수형 인터페이스(Functional Interface)
* 딱 하나의 추상 메소드를 정의 가능한 인터페이스
* 람다식 활용을 가능하게 만들어주는 요소
```
@FunctionalInterface
public interface Consumer {
  public abstract void accept(T t);
}
```

### 다양한 함수형 인터페이스
***Boxing<>보다는 특화형을 사용하는 것을 권장(Predicate<Integer> 보다 IntPredicate)***

* Supplier(get) : T type 리턴
* Consumer<T>(accept)
* Function<T, R>(apply) : T 타입을 받아 R 타입을 리턴
* Predicate<T>(test) : T 타입을 받아 boolean을 리턴
* UnaryOperator<T>(apply) : T 타입을 받아 T타입을 리턴
* BinaryOperator<T>(apply) : T 타입 파라미터1, 2를 받아 T 타입 리턴
* Compartor<T>(compare)

***Bi 활용~***

### 함수형 인터페이스 Customize
```
List<String> list;    //값 들어갔다고 가정
Consumer<String> consumer = new Consumer<String>() {
  public void accept(String value) {
    System.out.println(value);
  }
}

list.forEach(consumer);
```

## Method Reference
* 람다식의 메서드 구현 파트가 기존하는 메서드 한 줄로 끝날 경우 활용 가능

### [Class]::[instance method(public)]
* parameter1 : 메소드 수행 객체
* parameter2~ : parameters

### [Class]::[static method]
* 해당 Class의 static method에 전달
* parameters : parameters

### [Object]::[instance method(new)]
* 해당 Object의 instance method에 전달
* parameters : parameters

### 생성자 참조
```
//parameter 없는 생성자 example
Supplier<Person> constructor1 = Person:new;
Person person1 = constructor1.get();

//parameter 있는 생성자 example
Function<String, Person> constructor2 = Person:new;
Person person2 = constructor2.apply("홍길동");
```

## 추가된 Collection Method
* Iterable.forEach(Consumer)
* Iterator.forEachRemaining(Consumer)
* **Collection.removeIf(Predicate)**
* Collection.spliterator()
* Collection.stream()
* Collection.parallelStream()
* List.sort(Comparator)
* List.replaceAll(UnaryOperator)
* Map.forEach(BiConsumer)
* **Map.replaceAll(BiFunction)**
* **Map.putIfAbsent(K, V)**
* Map.remove(Object, Object)
* Map.replace(K, V, V)
* Map.replace(K, V)
* Map.computeIfAbsent(K, Function)
* **Map.computeIfPresent(K, BiFunction)**
* Map.compute(K, BiFunction)
* Map.merge(K, V, BiFunction)
* **Map.getOrDefault(Object, V)**

## Stream
### 특징
* 연속된 자료들을 다루고 연산하는 API를 지원
* Collection처럼 데이터를 추가하거나 삭제 하는 등의 API가 아님
* Method Chaning 형태
* Lazy(최종연산 메서드가 실행될 때 중간 연산도 실행)
* ShortCircuit(중간 연산에서 false면 알아서 break)
* 기본형에 특화된 객체 제공(IntStream 등)

### 단점
* 성능 저하...

## String.join()
* String.join(", ", list)

## Optional
* null 관련 처리를 해주는 클래스
* chaining method 활용 가능
### 예제
```
Optional.ofNullable(order)
			.map(Order::getMember)
			.map(Member::getAddress)
			.map(Address::getCity)
			.orElse("Seoul");
```
* map()을 통해 Optional 객체로 변환, 변환, 변환
* orElse를 통해 default 처리
```
Optional.ofNullable(order)
        .filter(o -> o.getDate().getTime() > System.currentTimeMillis()
        .map(Order::getMember);
```
* filter()를 패스하지 못하면 optional을 지워버림
