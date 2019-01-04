## Server to JS
### Server
```
model.addAttribute("name", value);
```

### JS
```
<script th:inline="javascript">
  let name = [[${name}]];
</script>
```

## 반복문
```
<div th:each="alias : ${name}"></div>
```

## 속성 추가에 활용
```
<img th:attr="src=@{|${name}|}">
```
## block, href 사용 이유, value in value
### example
* code
```
	<th:block th:with="id=${42774564}">
		<a th:href="@{https://stackoverflow.com/questions/{value}(value=${id})}">Stack Overflow</a>
	</th:block>
```
* result
```
  <a href="https://stackoverflow.com/questions/42774564">Stack Overflow</a>
```
### block
* 동적생성 이후 사라짐
* for thymeleaf 활용

### th:href 사용 이유
* 동적 href 생성을 위해

### value in value
* @{~~~ {value}(value=${~~})~~~}
* 소괄호 부분이 없으면 value 적용이 되지 않은 채 "{value}" 라는 텍스트가 됨

## Useful Expression Utility
### ${#execInfo.templateName}
### ${#dates.createNow()}
### ${#numbers.formatDecimal(num, 표현최소자릿수, 천단위 표현방식, 소수점자릿수, 소수점 표현방식)}
* 천단위, 소수점 표현방식 : 'POINT', 'COMMA', 'WHITESPACE', 'NONE'
### ${#numbers.formatCurrency(num)}
