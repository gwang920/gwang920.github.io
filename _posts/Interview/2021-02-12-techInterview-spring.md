---
title: Spring 기술 면접 정리
toc: true
categories:	
    - Interview
tags:
- Spring
last_modified_at: 
---



`Daily Update`

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

## IoC(Inversion of Control)

- 프로그램의 흐름을 프레임워크가 주도하는 것
- 객체의 생성부터 생명주기 관리를 컨테이너가 도맡아하는 것
- `IoC`의 예로는 `@Autowired` 로 `Bean`을 주입하는 것
- 스프링에서 객체를 `Bean`이라한다.

### 의존성 주입(DI)

- Unit Test 가 용이해진다.
- 코드의 재활용성이 높아진다.
- 객체간의 의존성(종속성)을 줄이거나 없앨 수 있다.
- 객체 간의 결합도를 낮추면서 유연한 코드를 작성할 수 있다.
- 생성자에 `@Autowired` 어노테이션이 있으면 스프링이 연관된 객체를 스프링 컨테이너에서 찾아서 넣어준다.



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

#### 장점

- 기존에는 `URL` 매핑을 사용하기 위해서 모든 서블릿을 `web.xml`에 등록해줘야했지만 `dispatcher servlet`이 애플리케이션으로 들어오는 모든 요청을 핸들링해주어 작업을 편리하게 처리할 수 있게 되었다. 

#### 발생할 수 있는 문제

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

### HTTP

- 웹 상에서 클라이언트와 서버 간에 요청/응답으로 데이터를 주고 받을 수 있는 프로토콜
- `HTTP` 요청에 포함되는 `HTTP` 메소드는 서버가 요청을 수행하기 위해 해야할 행동을 표시하는 용도로 사ㅛㅇ한다.
  - 대표적으로 `GET`, `POST`가 있다.

### Get

- `GET`은 서버로부터 정보를 조회하기 위해 설계된 메소드
- `GET`은 요청을 전송할 때 필요한 데이터를 `BODY`에 담지 않고 쿼리스트링을 통해 전송한다.
  - 쿼리스트링 : `URL`의 끝에 `?`와 함께 이름과 값으로 쌍을 이루는 요청 파라미터
  - 요청 파라미터가 여러개이면 `&` 를 이용해 연결한다.

- 예시

````
www.example-url.com/resources?name1=value1&name2=value2
````

`name1`, `name2`를 파라미터로 각각 `value1`, `value2` 값이 담겨 전송된다.

- `GET`은 불필요한 요청을 제한하기 위해 요청이 캐시될 수 있다.
  - 즉, 데이터양이 크고 변경될 일이 적은 `js`, `css`, `이미지` 같은 정적컨텐츠는 동일하게 반복 요청을 보낼 필요가없다.
  - 따라서, 동일한 요청이 발생하면 요청을 캐시해두고 캐시된 데이터를 반환한다.
  - 가끔, 프론트엔드 개발을 하다보면 정적 컨텐츠가 캐시되어 컨텐츠가 변경되지 않는 경우가 있다. 이때, 브라우저의 캐시 값을 지워주고 다시 실행해야 원하는 결과를 얻을 수 있다.

### POST

- `POST`는 **리소스를 생성/변경하기 위해 설계** 되었다. 그렇기 때문에 `HTTP` 요청시 필요한 데이터를 `BODY`에 담아 전송한다.
- `BODY`의 데이터는 길이제한없이 전송가능하다. 따라서, `GET`과 달리 대용량의 데이터를 전달할 수 있다.
- 이처럼 `POST`는 전송할 데이터를 `BODY`를 통해 전송하기 때문에 `GET`보다는 보안측면에서 안전하다.
  - 하지만, 크롬 개발자도구와 같은 툴로 요청내용을 확인할 수 있기 때문에 민감한 데이터는 **반드시 암호화**해 전송해야한다.
- `POST` 요청 시에는 요청 헤더의 `Content-Type`에 요청 데이터 타입을 표시해야한다.
  - 데이터 타입을 표시하지 않으면 서버는 내용이나 `URL`에 포함된 리소스의 확장자명 등으로 데이터 타입을 유추한다.
  - . 만약, 알 수 없는 경우에는 `application/octet-stream`로 요청을 처리

### Get vs Post

#### Get

- `Get`은 동일한 요청을 여러 번 수행하더라도 동일한 결과가 나오도록 설계되어있다.
- 서버에 동일한 요청을 여러번 보내더라도 동일한 응답이 돌아와야한다는 것을 의미한다.
- 그렇기 때문에 주로 조회를 할 때, 사용한다.

#### Post

- `POST`는 서버에게 동일한 요청을 여러 번 전송해도 응답은 항상 다를 수 있도록 설계되어있다.
- 그렇기 때문에 **서버의 상태**나 **데이터를 변경**할 때 사용한다.
  - `POST`는 생성, 수정, 삭제가 가능하지만 생성에는 `POST`, 수정은 `PUT` 또는 `PATCH`, 삭제는 `DELETE`를 사용하는 것이 일반적이다.

#### Ref.

[GET - POST](https://hongsii.github.io/2017/08/02/what-is-the-difference-get-and-post/)

### 어노테이션

- 어노테이션은 **메타데이터(Metadata)**이다. 메타데이터는 다른 데이터를 설명하기 위한 데이터이다. 그래서 어노테이션은 코드를 설명하기 위한 데이터라고 정의할 수 있다.

