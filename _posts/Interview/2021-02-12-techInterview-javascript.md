---
title: Javascript 기술 면접 정리
toc: true
categories:	
    - Interview
tags:
- Javascript
last_modified_at: 
---



`Daily Update`

## javascript

### undefined vs null

- `undefined` : 어떠한 값으로도 할당되지 않아 자료형이 정해지지 않은(undefined) 상태
- `null` : null로 값이 할당된 상태. 즉 null은 자료형이 정해진(defined) 상태

### var vs let vs const

- `var` : function-scoped, 재선언 가능, 재할당 가능
- `let` : block-scoped, 재선언 불가능, 재할당 가능
- `const` : block-scoped, immutable , 재선언 불가능, 재할당 불가능

### scope

- `scope` : 허용범위

- `global-scope` : 전역변수 scope
- `local-scope` : 지역변수 scope

### hoisting

- 함수의 선언부가 해당하는 `scope`영역의 최상단으로 끌어올려지는 것
- `var` 은 **function-scoped** 이므로 함수의 최상단으로 선언부(var value)가 **호이스팅**된다.

```javascript
fucntion hoistingEx(){
    // 이 위치로 hoisting 된다.
	console.log("value="+value);
	var value = 10;
	console.log("value="+value);
}
hoistingEx();

[실행결과]
value=undefined
value=10
```

### this (in javascript)

- `this` 키워드는 기본적으로 전역객체이다. 브라우저에서는 `window`가 된다.

```javascript
console.log(this);
console.log(this===window);

[출력]
[object Window]
true
```

- `this` 를 생성자 혹은 객체의 메소드로 사용하지 않는경우 `this`는 전역객체가 된다.

```javascript
const person=(name,gender)=>{
  this.name=name;
  this.gender=gender;
}

let gwang=person("광근","남");
console.log(gwang); // undefined
console.log(name);  // 광근
console.log(gender); // 남
```

이때, `gwang`은 `person`함수가 아무것도 `return`하지 않기 때문에 어떤 값으로도 초기화되어있지 않다. 따라서 `undefined`가 발생한다.

- `this`는 해당 메서드를 호출한 객체로 바인딩된다.

```javascript
var myobject={
    name:'foo',
    sayName:function(){
        console.log(this.name);
    }
};

var otherobject={
    name:'bar'
};

otherobject.sayName=myobject.sayName;

myobject.sayName();
otherobject.sayName();

[결과]
foo
bar
```

#### Ref.

[javascript-this](https://hyunseob.github.io/2016/03/10/javascript-this/)

### closure

- 클로저는 내부함수가 외부함수의 context에 접근할 수 있는 것을 가리킨다.
- 내부함수는 외부함수의 지역변수에 접근 할 수 있는데 외부함수의 실행이 끝나서 **외부함수가 소멸된 이후**에도 **내부함수가 외부함수의 변수에 접근** 할 수 있다. 이러한 메커니즘을 클로저라고 한다.

```javascript
function makeAdder(x) {
  var y = 1;
  return function(z) {
    y=100;
    return x + y + z;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);
//클로저에 x와 y의 환경이 저장됨

console.log(add5(2));  // 107 (x:5 + y:100 + z:2)
console.log(add10(2)); // 112 (x:10 + y:100 + z:2)
//함수 실행 시 클로저에 저장된 x, y값에 접근하여 값을 계산
```

- `javascript`에서 우리가 쓰는 많은 코드는 이벤트 기반이다. `click`, `key function` 등
- 이러한 경우 코드는 콜백형태로 전달된다. => 콜백 : 이벤트에 응답하여 실행되는 단일함수
- 위와 같은 상황에서 `closure`를 활용할 수 있다.
- 아래는 사용자의 `click`에 따라 `font-size`를 변경하는 기능의 자바스크립트코드이다.

```javascript
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);

document.getElementById('size-12').onclick = size12;
document.getElementById('size-14').onclick = size14;
document.getElementById('size-16').onclick = size16;
```

#### Ref.

[MDN - Closure](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Closures)

[생활코딩 - Closure](https://opentutorials.org/course/743/6544)
