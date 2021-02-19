---
title: Java 기술 면접 정리
toc: true
categories:	
    - Interview
tags:
- Java
last_modified_at: 
---



`Daily Update`

## JAVA

### 객체지향(OOP)?

구현하고자 하는 대상을 하나의 객체로 바라보며 프로그래밍하는 기법이다. 객체에 상태와 행위를 부여하고, 이 객체들간의 상호작용을 통해 로직을 구현하는 프로그래밍 패러다임 중 하나이다.

### 객체지향의 장/단점

#### 장점

- 코드의 재사용성

이미 만들어 놓은 객체를 마치 조립을 하듯이 갈아끼울 수 있다. 재사용성이 높아진다.

- 대규모의 프로젝트에 적합하다.

객체 단위로 분류해서 담당하는 부분만 개발하고, 개발이 이루어진 후 객체들간의 관계만 설정해주면 되기때문에 대규모의 프로젝트에서 업무를 분담하여 개발하기 쉽다.

- 유지보수가 쉽다.

절차지향같은 경우에는 코드를 수정할 때, 해당 부분을 직접찾아 수정해야하는 불편함이있지만,
객체지향은 수정하고자하는 객체 내부의 클래스 변수나 메소드를 수정해주면 되기때문에
유지보수에 장점이있다.

#### 단점

- 절차지향보다 속도가 느리다.
- 설계에 많은 시간이 투자된다.

### OOP 4대 특징

- 추상화

불필요한 정보들은 숨기고 **공통의 속성이나 기능**을 묶어놓은 것 (EX. 카트라이더 - 기본 카트)
다시말하면, 객체지향 관점에서 클래스를 정의하는 것

동일한 메소드를 가진 서브 클래스 여러개를 만들기위해서 사용한다.

- 캡슐화

캡슐화의 주요 목적은 중요한 데이터를 **보존, 보호**이다.

```
캡슐화는 api를 사용하는 "클라이언트" 입장에서 생각하면 됩니다.
클라이언트가 커피머신을 이용한다고 가정할 때,
"코드 꼽고, 물 넣고, 원두 채우고, ... , 만약 커피 찌꺼기가 있으면 비우고, 
..., 아메리카노 내리는 버튼 누르기" 보다 
그냥 "아메리카노 한잔 내려" 라고 하는 게 원래 의도겠죠.
```

[[출처] Okky](https://okky.kr/article/653658)

- 상속

기존의 클래스의 기능을 **확장**하거나 **수정**할 수 있는 객체지향의 특성을 가장 잘 나타내는 요소 중 하나이다. 상속을 통해 코드의 중복을 줄이고, 유지보수성을 높일 수 있다.

- 다형성

하나의 변수명, 함수명 등이 상황에 따라 **다른 의미로 해석**될 수 있는 것을 뜻함
다형성의 예로는 **오버로딩**, **오버라이딩**이 있다.

### 인터페이스

- 공통적으로 개발해야 할 기능이나 규격 등의 구현을 **강제**하는 역할을 한다.
- **동일한 목적 하에 동일한 기능을 보장하게 하기 위함!**
- 코드의 수정을 줄이고, 유지보수성을 높일 수 있다.

-  `interface` -> `interface` 상속 가능
- `interface` -> `객체` `implements`로 반드시 구현 

### "==" 과 "equals" 차이

- "==" : 주소값을 비교한다. 만약 같은 값을 가지고 있어도 참조하고 있는 주소값이 다르다면 `false`를 리턴한다.
- "equals" : 단순히 값만을 비교한다. 

```java
String s1="Cat";
String s2="Cat";
String s3=new String("Cat");

System.out.println(s1==s2); // true
System.out.println(s1.equals(s2)); // true
System.out.println(s1==s3); // false
System.out.println(s1.equals(s3)); // true
```

![string pool](https://user-images.githubusercontent.com/49560745/107731916-6da51c00-6d3a-11eb-8189-e6b459e9c0f8.png)

#### Ref.

[String vs StringBuilder vs StringBuffer](https://gwang920.github.io/java/stringType/)

https://richong.tistory.com/122

### Call by Value vs Call by Reference

- `Java`는 기본적으로 `Call by Value` 이다.

- `pimitive type`이 아닌 것에 대해서는 `call by reference`와 유사한 효과를 취하게 될 뿐이다.

[Call by value vs Call by reference](https://gwang920.github.io/java/CallbyValue-CallbyReference/)

### Collection

```
컬렉션이란 객체의 그룹을 조작하고 저장할 수 있는 자료구조이다.  
Java Collection 같은 경우 같은 타입의 자료를 관리할 수 있는 
유용한 하위 인터페이스들의 집합이다. 
```

### 메모리 구조

#### Ref.

[자바 JVM 메모리구조](https://m.blog.naver.com/PostView.nhn?blogId=kywpcm&logNo=30170981872&proxyReferer=https:%2F%2Fwww.google.com%2F)

### super

- 자식 클래스가 부모 클래스로부터 상속받은 멤버들을 참조할 때 사용하는 참조변수이다.
- 부모 클래스와 자식 클래스의 멤버 이름이 같을 때 `super`를 사용해 접근할 수 있다.
