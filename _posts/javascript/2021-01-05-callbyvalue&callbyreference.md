---
title: Call by Value vs Call by Reference [JAVASCRIPT]
toc: true
categories:	
    - Javascript
tags:
- call by value
- call by reference
- javascript
last_modified_at: 
---

 사실 이 포스팅을 작성하게 된 계기는 [프로그래머스 자물쇠와 열쇠 ](https://programmers.co.kr/learn/courses/30/lessons/60059) 이 문제를 풀이하다 '맞왜틀'에 빠졌기 때문이다. 배열 **argument**를 함수의 매개변수로 넘겨주며, 기본 배열 값의 변경되어 문제가 발생했다. 개념의 중요성을 다시 한번 느끼게 된 경험이었다.

<br/>

그래서 **call by value**, **call by reference**의 개념과 자바스크립트 내에서는 어떻게 사용되는지 알아보려한다.

# Call by value, Call by Reference란 무엇인가?

```
Call by value - 값을 전달한다.
Call by Refrence - 참조 값을 전달한다.
```

<br/>

시작하기에 앞서, **parameter** 와 **argument**의 정의를 정리해봤다. **Call by value**, **Call by Reference**를 이해하기 위해 참고하면 좋을 것같다.

* [참고] parameter vs argument

```javascript
parameter는 함수 혹은 메서드내에서 정의되는 변수명이다.
argument는 함수 혹은 메서드를 호출할 때 전달하거나 입력되는 실제 값이다.

ex)

function test(para1,para2){
	return para1 + " " + para2;
}

// test 함수 내에 정의된 para1, para2는 parameter이다.

test(argu1,argu2);
// test 함수를 호출할 때 전달되는 argu1, argu2는 argument이다.

```

<br/>

본격적으로 **argument**를 함수 혹은 메소드의 매개변수로 전달하는 **두 방식**에 대해 알아보자.

# Call by Value

call by value의 특징은 이렇다.

- **argument**가 값으로 넘어온다.

- 값이 넘어올 때, 값을 **복사**하여 넘겨준다.
- 호출하는 곳에서 값을 **복사**하여 넘겨주기 때문에, 호출 당한 곳에서 호출자의 argument 값을 **변경**할 수 없다. 즉, 원본 **argument** 값이 **변경 될 위험이 없다.** 
- **Call by value 타입**에는 `number`, `string`, `boolean` 등이 있다.

````

````



<br/>

# Call by Reference

call by reference의 특징은 이렇다.

- **argument**로 **reference**를 넘겨준다.
  - reference는 메모리 주소를 담고있는 변수이다.
- **reference** 자체를 넘기기 때문에 **call by value와 다르게** 값을 복사해 넘기는 형태가 아니다.
- 호출하는 곳에서 참조 값을 넘겨주기 때문에, 호출 당한 곳에서 호출자의 argument 값을 **변경**할 수 있다. 즉, 원본 **argument** 값이 **변경 될 위험이 발생한다.**
- **Call by Reference** 타입에는 `array`, `object`, `date` 등이 있다.

```

```









# Reference

- [jimmyjoo.log - call by value vs call by reference](https://velog.io/@jimmyjoo/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%8F%89%EA%B0%80%EC%A0%84%EB%9E%B5-Call-By-Value-vs-Call-By-Reference-vs-Call-By-Sharing)
- [bbackteaho - 얕은복사, 깊은복사](https://bbaktaeho-95.tistory.com/37)
