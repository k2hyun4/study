## window.onload
* 여러 js 파일을 link하고 각 파일마다 window.onload 실행 시 문제
* 해결 방안
```
addLoadEvent(init);

function addLoadEvent(func){
    let oldonload = window.onload;
    
    if (typeof window.onload != 'function'){
        window.onload = func;
    } else {
		window.onload = function(){
			oldonload();
            func();
        };
    }
}

function init() {
	
};
```
* ref : https://tistory.kkwang.com/177

## index 구하기
```
//JQuery
$('selector').index();

//JavaScript
for (~~~)

Math.floor(Array.from(this.parentNode.childNodes).indexOf(this) / 2);

Math.floor(Array.prototype.indexOf.call(this.parentNode.childNodes, this) / 2);
```

* ref : https://stackoverflow.com/questions/4649699/is-it-possible-to-get-elements-numerical-index-in-its-parent-node-without-loopi

# insertBefore
## [parentElement].insertBefore([newElement], [standardEelment]);
* standardElement가 undefined라면, appendChild() 와 동일

# 기억할 function들
## call, apply, bind
### call
* 모든 함수에 사용 가능
* this를 특정 값으로 지정 가능
```
const bruce = {
	name: 'Bruce'
}

function greet(age) {
	return 'My name is ' + this.name;
}

greet();	//'My Name is ';
greet(bruce);		//
```

### apply

### bind

# ES6 추가된 기능
## Arrows
```
let evens = [2, 4, 6, 8, 10];
let nums = evens.map((v, i) => v + i);
```

## Template Strings(String Interpolator)
* 자바의 String.format처럼 활용
```
let a = 'aaaa';
let b = 'bbbb';
	
console.log('A : ' + a + ', B : ' + b);
console.log(`A : ${a}, B : ${b});
```

## Multi-line-String
```
//ES5
var str = 'aaaaaaaa\n'
	+ 'bbbbbbb';
	
//ES6
var str = `aaaaaaa
	bbbbbb`;
```

## 비구조화 할당(destructuring assignment)
* de + structure + ing
```
let [a, , b] = [1, 2, 3];
//a = 1, b = 3

let json = {'a' : 'aaaa', 'b' : 'bbbb'};
let {a : newA, b : newB} = json;
//newA = 'aaaa', newB = 'bbbb'

//ex2
const {scrollHeight, clientHeight} = this.box;

const scrollHeight = this.box.scrollHeight;
const clientHeight = this.box.clientHeight;
```

## class

```
class Sample {
	constructor(param1, param2, ...) {
	this.param1 = param1;
		this.param2 = param2;
		.....
	}
}
```

* 함수 추가, extends, overriding도 가능

## Enhanced Object Literals
* ...?
* ref : [es2015features](https://github.com/gsfe/es2015features/tree/master/enhanced-object-literals)

## Promises
* 어렵쓰.. 중첩시 이점이 있다던데
```
//ES5
setTimeout(function() {
	console.log('hi');
}, 1000);

//ES6
let wait1000 = new Promise((resolve, reject) => {
	setTimeout(resolve, 1000)
}).then(() => {
	console.log('hi');
});
```

## Map & Set
```
let map = new Map();
map.set('key', 'value');
map.get('key');

let set = new Set();
set.add('value');
```

* Set은 Java Set처럼 중복 불허

## WeakMap & WeakSet
* ......

## Named Parameters
* 힌트 부여
```
sum(x = 10, y = 1000);
```

## Default
```
function f(x, y = 12) {
	
}
```

## Rest
* parameters를 array로 변환
```
function f(x, ...y) {
	return x * y.length;
}

let result = f(3, 'hello', true);
//result = 6. parameter y : ['hello', true]

let numArray = [4, 2, 1, 11, 6];
Math.min(...numArray);		//1
Math.max(...numArray);		//11
```

## Spread operator
* ...뒤에 오는 배열 값을 복사
* 배열 아니고 배열 값!
```
function f(x, y, z) {
	return x + y + z;
}

//let result = f(1, 2, 3);
let result = f(...[1, 2, 3]);
//result = 6
```

## for...of
* array 외의 것도 loop을 돌림... 그냥 다 돌림
```
for (var a of array) {}
```

## Symbol
* 키의 충돌을 피하기 위해 만들어진 Javascript의 새로운 Type
* 고유한 값. 불변값
* Symbol() : 새롭고 고유한 심볼 리턴
* Symbol.for(String key) : 기존할 경우 기존 심볼 리턴
```
let keyArray = [Symbol('kkh'), Symbol('kkh'), Symbol.for('kkh'), Symbol.for('kkh')];
keyArray[0] == keyArray[1];	//false
testArray[2] == testArray[3];	//true
```
## proxy(보류ㅠㅠ)

## 추가된 라이브러리, 메서드 중에...
* Number.isInteger(1.1);	//false
* "abcde".includes("cd");	//true
* "abc".repeat(3);	//"abcabcabc"
* [0, 0, 0, 0].fill(100, 1, 3);		//[0, 100, 100, 0]	//end index - 1 까지만 적용됨
* [1, 3, 5, 7, 9].findIndex(x => x == 3);		//1
