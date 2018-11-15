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
