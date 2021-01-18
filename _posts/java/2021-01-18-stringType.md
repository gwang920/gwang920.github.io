---
title: Java - String vs StringBuilder vs StringBuffer
toc: true
categories:	
    - Java
tags: 
- Java
- String
last_modified_at:
---

 **String**, **StringBuilder**, **StringBuffer** 는 PS(Problem Solving)에서 **Stirng **객체를 컨트롤 할때 한 번씩 들어봤을 것이다. 막연하게 속도의 차이가 있다는 점만 알고 있었다. 이번 포스팅에서는 **String**, **StringBuilder**, **StringBuffer** 특징을 간략하게 알아보려한다.

먼저 요약하자면, **Stirng** 은 **immutable(불변)**, **StringBuilder**, **StringBuffer**는 **mutable(가변)** 이라는 점을 기억하자.

# String

**String** 객체는 한번 생성되면 할당 된 메모리 공간이 변하지 않는다. `+` 연산자나 `concat` 메소드를 통해 기존 **Stirng** 객체 문자열에 새로운 문자열을 붙일 수 있다. 이때, **String** 객체는 기존 문자열에 새로운 문자열을 붙이는 것이 아니라 **새로운 Stirng이 다른 메모리 공간에 적재되는 것이다.** 즉, 기존 **String** 객체는 **immutable(불변)** 한다.

예제로 살펴보자. 자바의 **hashCode()** 메소드는 각 객체의 주소값을 변환하여 생성한 객체의 고유한 정수값이다. 즉, 두 객체가 동일한지 파악할 때, 사용한다.

```java
String str = "ABCD";
String newStr=str+"E";
        
System.out.println("str: " + str.hashCode());
System.out.println("newStr: " + newStr.hashCode());

newStr=str;
System.out.println("newStr: " + newStr.hashCode());
newStr=newStr.concat("E");
System.out.println("newStr: " + newStr.hashCode());

[결과]
str: 2001986
newStr: 62061635
newStr: 2001986
newStr: 62061635
```

 `+` 연산이나 `conact` 을 사용한 경우, 기존의 **String** 객체의 공간이 아닌 새로운 공간에 새로운 문자열을 할당한다. 

![String concat +](https://user-images.githubusercontent.com/49560745/104866857-e8208d00-5982-11eb-9d7d-db20d315ffa6.png)





# StringBuilder

**StringBuilder** 는 **String** 객체와는 다르게 기존 버퍼의 크기(메모리 공간)를 늘리며 유연하게 작동한다. 

아래의 예제를 보자.

````java
StringBuilder str = new StringBuilder();

str.append("TEST1");
System.out.println("str: " + str.hashCode());

str.append("ISEQUAL");
System.out.println("str: " + str.hashCode());

[결과]
str: 2001112025
str: 2001112025
````

**hashcode**가 동일하다. 즉, 동일한 메모리 공간의 버퍼 크기를 키워 할당한 것을 알 수 있다.

![StringBuilder](https://user-images.githubusercontent.com/49560745/104869139-9ed33c00-5988-11eb-9669-cbcd5417c9ab.png)

# StringBuffer

**StringBuffer **도 마찬가지로 **String** 객체와는 다르게 기존 버퍼의 크기(메모리 공간)를 늘리며 유연하게 작동한다. 

아래의 예제를 보자.

```java
StringBuffer str = new StringBuffer();

str.append("TEST1");
System.out.println("str: " + str.hashCode());

str.append("ISEQUAL");
System.out.println("str: " + str.hashCode());

[결과]
str: 2001112025
str: 2001112025
```

**StringBuilder** 와 마찬가지로 **hashcode**가 동일하다. 즉, 동일한 메모리 공간의 버퍼 크기를 키워 할당한 것을 알 수 있다.

![StringBuffer](https://user-images.githubusercontent.com/49560745/104869230-da6e0600-5988-11eb-94de-1f2aa1a18602.png)

<br/>

# Reference

- [길은 가면 뒤에 있다 - String, StringBuilder,StringBuffer]( https://12bme.tistory.com/42)