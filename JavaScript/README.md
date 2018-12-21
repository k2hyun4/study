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
