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
