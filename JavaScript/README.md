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

# ES6 추가된 기능
## String Interpolator
* 자바의 String.format처럼 활용
```
	let a = 'aaaa';
	let b = 'bbbb';
	
	console.log('a : ' + a + ', b : ' + b);
	console.log(`a : ${a}, b : ${b});
```
## Destructuring
```
	let json = {'a' : 'aaaa', 'b' : 'bbbb'};
	let {a : newA, b : newB} = json;
	//newA = 'aaaa', newB = 'bbbb'
	
	let array = [1, 2, 3];
	let [a, b, c] = array;
	//a = 1, b = 2, c = 3
```
## Default Parameters
* parameter의 기본값을 지정
```
	function sum(x = 1, y = 2) {
		return x + y;
	}

```
## Named Parameters
* 힌트 부여
```
	sum(x = 10, y = 1000);
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

## Map & Set
```
	let map = new Map();
	map.set('key', 'value');
	map.get('key');
	
	let set = new Set();
	set.add('value');
```

* Set은 Java Set처럼 중복 불허
