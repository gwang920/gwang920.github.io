---
title: 개발자 기술 면접 정리
toc: true
categories:	
    - Interview
tags:
- Java
- Spring
- Database
- DataStructure
last_modified_at: 
---

# 기술면접

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

<br/>

## Spring

### 구조

![springcontainer](https://user-images.githubusercontent.com/49560745/108300423-a41fe280-71e3-11eb-9a6d-6025138a8103.png)

- `Core` : DI 기능을 제공
- `Context` : 컨텍스트라는 정보를 제공하는 설정을 관리한다.
- `DAO` : DB와 관련된 JDBC 코딩 부분을 처리해 주기 위한 JDBC 추상화 레이어를 제공
- `ORM` : JDO, Hibernate, iBATIS 등 O-R Mapping API를 위한 레이어를 제공
- `AOP` : 관점지향 프로그래밍을 제공
- `Web` : 웹 기반의 여러 기능 제공

#### Ref.

[springio](https://docs.spring.io/spring-framework/docs/4.3.x/spring-framework-reference/html/overview.html)

### 의존성 주입(DI)

- Unit Test 가 용이해진다.
- 코드의 재활용성이 높아진다.
- 객체간의 의존성(종속성)을 줄이거나 없앨 수 있다.
- 객체 간의 결합도를 낮추면서 유연한 코드를 작성할 수 있다.



필요한 객체를 직접 클래스에 생성하지 않고, 생성자를 통해 외부에서 주입해준다.

#### Ref.

[의존성 주입](https://velog.io/@wlsdud2194/what-is-di)

### Primitive Type vs Reference Type

`Primitive Type`

- 산술 연산이 가능함
- `null`로 초기화 할 수 없음

```java
byte
short
int
long
float
double
char
boolean
void
```

`Reference Type`

- 산술 연산 불가능
- `null`로 초기화 할 수 있음
- **DB와 연동시 DTO 객체에 null이 필요한 경우 사용 할 수 있음**

```java
Byte 
Short 
Integer 
Long 
Float 
Double 
Charater 
Boolean 
Void
```

- 사용 이유

```
1. 매개변수로 객체가 요구 될때.
2. 기본형 값이 아닌 객체로 저장해야 할 때.
3. 객체간의 비교가 필요할 때.
```



#### Ref.

[java119 - primitive vs reference](https://java119.tistory.com/41)

### 서블릿 & 서블릿 컨테이너

- 자바를 사용하여 웹을 구현하기 위한 기술
- 클라이언트의 요청을 처리해 결과를 반환해주는 역할
- **서블릿 컨테이너**는 웹서버와 통신하기 위해 웹 소켓을 생성하고, 특정 포트에 리스팅하고, 스트림을 생성하는 등의 복잡한일들을 할 필요 없게 만들어준다.
- **서블릿 컨테이너**의 대표적인 예는 `Tomcat`이다. 컨테이너는 요청이 들어올 때마다 자바 스레드를 만든다.

### 스프링 컨테이너

- 스프링 컨테이너는 `Bean`들의 생명주기를 관리한다.
- `IoC`를 사용해 `Bean`들을 관리한다.

### dispatcher servlet

#### 개념

- `dispatch` : 보내다.
- 프론트 컨트롤러
- 클라이언트로부터 요청이오면 `Tomcat`과 같은 서블릿 컨테이너가 요청을 받는다.
  - 이때, 제일 앞에서 서버로 들어오는 모든 요청을 처리하는 것이 `dispatcher servlet`이다.

### 장점

- 기존에는 `URL` 매핑을 사용하기 위해서 모든 서블릿을 `web.xml`에 등록해줘야했지만 `dispatcher servlet`이 애플리케이션으로 들어오는 모든 요청을 핸들링해주어 작업을 편리하게 처리할 수 있게 되었다. 

### 발생할 수 있는 문제

- `dispatcher servlet`이 모든 요청을 처리하다보면 `image`나 `HTML` 파일을 불러오는 요청마저 전부`Controller`로 넘겨버릴 것이다.
- 이를 해결하기 위한 방법은 ` <mvc:resources />`를 이용하는 것이다. 
  - 해당 요청에 컨트롤러를 찾을 수 없는 경우, 2차적으로 설정된 경로에서 요청을 탐색하여 자원을 찾아낸다.

### Context Parameter

- **Context parameter**는 같은 웹 어플리케이션의 서블릿들이 같이 공유할 수 있는 매개변수이다.
- 여러 서블릿에서 공통으로 참조하는 값이 있을 경우 **context parameter**로 정의하면 유지보수하기 좋은 코드를 작성할 수 있다.

### Context

- **Context는 system을 핸들링 하기위해 존재**한다. 즉, 리소스 값 처리, 데이터베이스 및 기본 설정에 대한 액세스 권한 획득 등과 같은 서비스를 제공한다. Context는 현재 application이 동작하는 동안의 모든 환경을 핸들링한다고 생각하면 쉽다.

#### Ref.

[Context](https://www.crocus.co.kr/1696)

### MVC1 vs MVC2 vs SPRING MVC

**MVC1**

- `html` 코드내에 자바코드가 공존하는 방식
- 간단한 프로그램을 설계하는데 적합
- `view`와 `controller`를 한 곳에서 처리하는 것

**MVC2**

- `view`, `controller`, `model`을 분리해서 처리하는 것
- 보여지는 화면을 구성하는 `view(JSP)` 페이지, 요청을 처리하는 `model(빈, 클래스)`, 제어하는 `controller(서블릿)`으로 확실하게 나뉜다.
- 구조가 복잡하여 학습하기 어렵고, 설정 및 작업 분량이 많다.
- `back-end`와 `front-end`가 나누어져 분업이 편리하다.

**SPRING MVC**

![image](https://user-images.githubusercontent.com/49560745/100300508-83c3fb80-2fd9-11eb-8142-4d10d3072020.png)

```
1) 처리요청(URL) - Dispatcher Servlet
2) HandlerMapping (URL과 매핑되는 컨트롤러 검색)
3) HandlerMapping (URL과 매핑되는 컨트롤러 반환)
4) controller (처리요청)
5) modelAndView 리턴
6) 실행결과 view에 요청
7) 실행결과 리턴
8) 응답생성 출력 요청
9) JSP 생성 후 사용자에게 전달
```

```
Request 
-> DispatcherServlet 
-> HandlerMapping 
-> Controller 
-> Service 
-> DAO 
-> DB 
-> DAO 
-> Service 
-> Controller 
-> DispatcherServlet 
-> ViewResolver 
-> View 
-> Response
```



<br/>

## Database

### JDBC

- 자바에서 DB의 종류에 상관없이 데이터베이스에 쉽게 접근할 수 있도록 하는 API

### DBCP

- `DataBase Connection Pool`의 약자
- 애플리케이션에서 `DB`로 요청할 때, 가장 많은 비용이 소모되는 **커넥션 객체 생성** 비용을 줄일 수 있다.
- `Pool` 에 미리 `Connection` 객체를 생성해두고, 필요할 때마다 가져와 사용하고 반납하는 구조이다.
- `Tomcat(서버)`의 스레드 하나 당 하나의 커넥션 객체가 일대일로 매칭된다.
  - 커넥션 객체를 모두 사용하고 있을 때, 요청이 들어오면 스레드는 대기열에서 대기한다.
  - `Tomcat(서버)` 스레드 풀의 스레드가 모두 소진되면 `Tomcat` 은 오류를 뱉는다.
    - Q. 커넥션 객체를 가능한 많이 만들어 놓으면?
    - A. 일반적으로 `DBMS`의 리소스는 다른 서비스와 공유해 사용하는 경우가 많기에 무조건 커넥션 개수를 늘리는게 답이아니다.
  - 사용자가 인내할 수 없는 `MaxWait` 값은 쓸모 없다.
  - 그렇다고 `MaxWait`를 너무 작게 설정하면 과부하 시 커넥션 풀에 여분의 객체가 없을 때 너무 자주 오류 메시지를 보게된다.

#### Ref.

[naver D2 - DBCP](https://d2.naver.com/helloworld/5102792)

### statement preparation

- `RDBMS` 실행에 있어 비용이 많이 드는 작업이며, 복잡한 `SQL`일 수록 더욱 높은 비용 소모

```
문법 오류 검증
컬럼 참조의 유효성 검증
최적화 된 접근경로
execution plan의 식별
```



### prepared statement pool

- 자주 사용되는 `statement` 를 사전에 `prepare` 하여 `pool`에 저장해놓는 것
- `pool`에서 `Prepare`된 statement을 갖고 오는 방법을 Prepared Statement Pooling
- statement preparation에 소모되는 비용을 최소화 할 수 있음

#### 생성 방법

- `connection pool` 이 있다면 `pool`에서 connection을 얻어 온다.
- `preparedstatement pool` 생성하기

![image](https://user-images.githubusercontent.com/49560745/108307551-501bfa80-71f1-11eb-8c6d-fda40c5f6bf7.png)



#### 사용하는 이유

- `RDBMS`가 `statement`를 준비하는 시간을 줄여주기때문에 애플리케이션이 `RDBMS`로부터 데이터를 로딩하는 시간이 향상됨
- `Statement caching`이 자동으로 수행됨
- `Statement pooling`과 `Connection pooling`을 함께 사용하면 `Connection pooling`을 단독으로 사용하는 것보다 큰 성능향상을 가져옴

#### connection pool과 preparedstatement pool을 같이 사용했을 때 장점

- 커넥션 풀을 사용하지 않으면 애플리케이션이 `disconnect` 되었을 때 `prepared statement pool`이 사라진다.
- 하지만, 커넥션 풀을 사용한다면 `prepared statement pool`이 사라지지 않고,`disconnect` 될 때 `connection pool`과 `prepared statement pool`이 함께 return 된다.
- 이후에 애플리케이션이 `connect` 했을 때 `Statement prepare`를 하지않고, `prepared statement pool`에 있는 `prepared statement`를 재사용할 수 있다.

#### Ref.

[prepared statement pool](https://zzikjh.tistory.com/entry/DBCP-%EC%82%AC%EC%9A%A9%EC%8B%9C-poolPreparedStatements-%EC%86%8D%EC%84%B1%EC%9D%B4-%EC%84%B1%EB%8A%A5%EC%97%90-%EB%AF%B8%EC%B9%98%EB%8A%94-%EC%98%81%ED%96%A5)

### statement

- `SQL` 구문을 실행하는 역할
- 구문 실행 후 결과를 반환하는 역할



### perpared statement vs statement

**[참고]**  `SQL` 실행과정

```
1) 쿼리 문장 분석
2) 컴파일
3) 실행
```

- 둘의 가장 큰 차이점은 `캐싱` 사용 여부이다.

- `statement`는 쿼리를 실행할 때 마다 1) ~ 3)의 과정을 거친다
- `prepared statement`는 컴파일을 미리 준비해두기 때문에 `statement`보다 성능상 이점이있다.
- 동일한 쿼리에서는 `prepared statement` 유리
  - select * from a    => 10만건이상의 데이터 가져오기
- 조건절이 매번 바뀌는 쿼리는 `statement` 유리



### 인덱스에는 왜 Hashtable 보다 B Tree 인가?

`Hashtable`의 `search` 시간복잡도는 `O(1)`이다. 그 어떤 자료구조보다 검색을 할 때 빠르다. 그럼에도 불구하고 `Database`의 `index`의 구조로 왜 `B Tree`를 선택했을까?

그 이유는 바로 데이터베이스의 데이터 구조 특성때문이다. 

데이터베이스에서 자료를 **조회**할 떄 특정 데이터만을 추출하기도 하지만, 범위 설정이 필요한 경우가 많다.

예를들어, 키가 180이상인 사람의 데이터를 추출하고 싶다면 조건문에 부등호 `>=`  기호를 사용해야한다. 이 부등호는 `Hashtable`에서는 사용할 수 없다. `Hashtable`은 `{key : vlaue}` 쌍의 구조로 특정 데이터를 가리키는 `key` 값만 가지고 있을 뿐 부등호 연산을 할 수 없는 것이다. 그렇기 때문에 부등호 연산에 적합한 `B Tree`를 사용한다. 조회 시간복잡도도 `log(n)`으로 준수하다.

### 인덱스 성능 고려할 점

`SELECT` 쿼리의 성능을 향상시키는 `INDEX`는 항상 좋지만은 않다.

- `INSERT`의 경우 `INDEX`에 대한 데이터를 추가해야하므로 그만큼 성능에 손실이있다.
- `DELETE`의 경우 `INDEX`에 존재하는 값을 삭제하는 것이 아닌 사용하지 않는다는 표시가 남는다.
  - 즉, row 수는 그대로이다. 실제 데이터는 1000건인데 데이터가 10만이되는 결과를 낳을 수 있다.
- `UPDATE`의 경우 `INSERT`, `DELETE` 두 경우의 문제점을 모두 수반한다.
  - `UPDATE`는 이전 데이터를 삭제하고, 새 데이터를 삽입하는 개념이기 때문이다.

### 인덱스 활용법

- 전체 데이터 중 10~15% 이내의 데이터를 검색할 때 사용하면 효율적이다.
- 두 개이상의 컬럼이 `WHERE`절이나 `JOIN` 조건으로 자주 사용되는 경우 인덱스를 생성하는 것이 효율적이다.
- 한 테이블에 저장된 데이터 용량이 상당히 클 경우 유리하다.
- 가능 한 수정이 빈번하게 일어나지 않는 컬럼을 설정한다.

### 트랜잭션 격리 수준(isolation)



### UNDO, REDO

- `UNDO`는 실행취소, `REDO`는 다시하다 라는 뜻을 갖는다.

- `REDO`와 `UNDO`의 공통점은 복구이다.
  - `REDO`는 복구할 때, 사용자가 했던 작업을 그대로 다시한다.
  - `UNDO`는 복구할 떄, 사용자가 했던 작업을 반대로 한다. 즉, 작업을 원상태로 되돌린다.

#### Ref.

https://brownbears.tistory.com/181

### Primary key , Foreign key

- `Primary key` : 테이블에서 각 행(row)를 유일하게 구분하는 key
- `Foreign key` : 하나의 테이블에 있는 열(column)으로는 그 의미를 표현할 수 없는 경우, 다른 테이블의 `Primary key` 열(column)을 반드시 참조해야하는 key



<br/>

## 자료구조

<br/>

## 알고리즘

### 퀵소트

시간복잡도

- 평균 : nlog(n) (파티션을 나누는 횟수 n * 데이터 탐색횟수는 매번 절반으로 줄어듬)

- 최악 : n^2 (자료가 모두 정렬되어있을 경우)

<br/>

## OS

### 로드벨런서

- 부하를 분담해주는 역할을 한다.
- **scale up** : 서버의 성능을 높이는 것
  - 인스턴스를 업데이트하는동안 서비스를 할 수 없다.
- **scale out** : 서버의 대수를 늘리는 것
  - 서버가 늘어날 때 마다 도메인이 새로 필요하다.

### Proxy

- 클라이언트와 서버간의 중계서버로, 통신을 대리 수행하는 서버

### Forward Proxy

```java
Clients => Forward Proxy => Internet => Servers
```

- 캐시 : 동일한 요청은 캐시로 처리할 수 있다. (클라이언트가 요청한 내용을 캐싱)
- 익명성 : 누가 요청을 보내는지 서버가 알 수없다. (클라이언트가 보낸 요청을 감춤)

### Reverse Proxy

```java
Clients => Internet => Reverse Proxy => Servers
```

- 캐시 (Forward proxy와 동일)
- 익명성 (Forward proxy와 동일)
- 로드밸런서 기능 : 부하 분산(요청을 나눠줌)

