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
### #execInfo
* ${#execInfo.templateName}
### #dates
* ${#dates.createNow()}
### #numbers
* ${#numbers.formatDecimal(num, 표현 최소 자릿수, 천 단위 표현방식, 소수점 자릿수, 소수점 표현방식)}
* 천 단위, 소수점 표현방식 : 'POINT', 'COMMA', 'WHITESPACE', 'NONE'
* ${#numbers.formatCurrency(num)}
* ${#numbers.formatPercent(num, 표현 최소 자릿수, 소수점 자릿수}
* ${#numbers.sequence(from, to, step)}
### #strings
* ${#strings.isEmpty(str)}
* ${#strings.defaultString(str, 기본값)}
* ${#strings.contains(str, 찾을 문자열)}
* ${#strings.containsIgnoreCase(str, 찾을 문자열)}
* ${#strings.startsWith(str, 찾을 문자열)}
* ${#strings.endsWith(str, 찾을 문자열)}
* ${#strings.indexOf(str, 찾을 문자열)}
* ${#strings.substring(str,시작 index, 마지막 index)}
* ${#strings.substringAfter(str, prefix)}
* ${#strings.substringBefore(str, suffix)}
* ${#strings.replace(str, 찾을 문자열, 바꿀 문자열)} 
* ${#strings.prepend(str, prefix)}
* ${#strings.append(str, suffix)}
* ${#strings.toUpperCase(str)}
* ${#strings.toLowerCase(str)}
* ${#strings.trim(str)}
* ${#strings.length(str)}
* ${#strings.abbreviate(str, 최대표현수)} - 넘어가면 ..., 최대 표현수에 ...수도 포함
* ${#strings.capitalize(str)}
* ${#strings.unCapitalize(str)}
* ${#strings.capitalizeWords(str, 구분자)}
### #bools
* ${#bools.isTrue(param)}
### #maps
* ${#maps.containsKey(map, key)}
* ${#maps.containsValue(map, value)}
### #aggregates
* ${#aggregates.sum(array)}
* ${#aggregates.avg(array)}

## Replace & Fragment
```
//Fragment
<head th:fragment="fragment영역명">~~</head>
//Replace
<head th:replace="fragmentView경로 :: fragment영역명"/>
//Insert
<html th:insert="fragmentView경로 :: fragment영역명"></html>
```
### 주의점
* 이클립스에서 테스트 때는 정상 작동했는데, executable jar에서는 fragment를 못찾음
* 원인 : fragmentView경로를 "/"로 시작(classpath:\templates 기준을 잡기 위해...)
* 해결방안 : "/" 없이 시작하면 정상작동(상대경로로 적용되지 않고 잘 됨)
