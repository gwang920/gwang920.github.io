---
title: Spring boot기반 Web Application 개발[8] - 요구사항
toc: true
categories:	
    - Spring boot
tags:
- Spring boot
- Spring Web
last_modified_at:

---



 지금까지 Spring boot 기반 Web 개발에 대한 기초를 알아봤다. 이제 본격적으로 간단한 회원시스템을 만들어보자. 개발은 항상 **요구사항**을 토대로 진행된다. 개발할 시스템의 요구사항은 다음과 같다.

# 요구사항

```
데이터: 회원ID, 이름
기능: 회원 등록, 조회
아직 데이터 저장소가 선정되지 않음(가상의 시나리오)
```

 여기서 **가상의 시나리오**는 실제 현업에서 개발할 때, `NoSQL` , `RDB`등 저장소를 선정하기전에 개발을 진행해야 할때가 있어 설정한 것이다. 간단하게 회원 ID와 이름만을 가지고 백엔드 시스템을 설계해보자.

**일반적인 웹 애플리케이션의 계층 구조**

![image](https://user-images.githubusercontent.com/49560745/103983127-1d312080-51c8-11eb-8e3c-94fa415c942e.png)

- 컨트롤러: 웹 MVC의 컨트롤러 역할 
- 서비스: 핵심 비즈니스 로직 구현 
- 리포지토리: 데이터베이스에 접근, 도메인 객체를 DB에 저장하고 관리 
- 도메인: 비즈니스 도메인 객체, 예) 회원, 주문, 쿠폰 등등 주로 데이터베이스에 저장하고 관리됨

 **컨트롤러**는 웹 MVC에서 말하는 **컨트롤러**와 같다. **모델**과 **뷰**사이에서 모든 요청을 관리해준다. **서비스**에는 핵심 비즈니스 로직이 구현된다. **서비스**의 예로는 회원가입 시 중복체크나 로그인 비밀번호 일치 확인 등이 있다. 아직 `Database`가 결정되지 않았기 때문에 **리포지토리**를 사용해 간단하게 데이터를 주고 받도록 요구사항이 설계되었다.

**클래스 의존관계**

![image](https://user-images.githubusercontent.com/49560745/103983531-bceeae80-51c8-11eb-8cef-68317644cd9a.png)

- 아직 `Database`가 선정되지 않아서, 우선 인터페이스로 구현 클래스를 변경할 수 있도록 설계
- 데이터 저장소는 `RDB`, `NoSQL` 등등 다양한 저장소를 고민중인 상황으로 가정 
- 개발을 진행하기 위해서 초기 개발 단계에서는 구현체로 가벼운 메모리 기반의 데이터 저장소 사용

<br/><br/><br/><br/><br/>

# API 방식

**API** 방식은 `@ResponseBody`를 사용한다는 점을 기억하고, 실습을 진행해보자.



## 1) String 형식반환

이전에 진행했던 `HelloController.java`파일에 이어서 아래 코드를 작성하자.

```java
@GetMapping("hello-string")
@ResponseBody
public String helloString(@RequestParam("name") String name){
    return "hello" + name;
}
```

- `url` 매핑 "hello-string"
- `@ResponseBody` 태그 : 메소의 반환 값을 그대로 브라우저에게 반환한다.

```
파일명 : HelloController.java
위치 : src\main\java\hello.hellospring\controller\HelloController.java
```

```java
package hello.hellospring.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {

    @GetMapping("hello")
    public String Hello(Model model){
        model.addAttribute("data","hello!!");
        return "hello";
    }

    @GetMapping("hello-mvc")
    public String helloMVC(@RequestParam("name") String name,Model model){
        model.addAttribute("name",name);
        return "hello-template";
    }
	
    // 추가된 코드
    @GetMapping("hello-string")
    @ResponseBody
    public String helloString(@RequestParam("name") String name){
        return "hello" + name;
    }
}
```



 `http://localhost:8000/hello-string?name=spring!!!!!!!!` 접속해보자.

![image](https://user-images.githubusercontent.com/49560745/103976878-4d25f700-51bb-11eb-82bf-1388c6f802be.png)

정상적으로 로드된다. 그렇다면 `템플릿엔진` 혹은 `정적 컨텐츠` 방식과는 어떤차이가 있을까?

화면에서 우클릭을하고 **페이지 소스 보기**를 눌러보자.

![image](https://user-images.githubusercontent.com/49560745/103976988-8d857500-51bb-11eb-90f4-ce1191caf9c4.png)

`HTML` 코드가 보이지 않는다. 이게 바로 Spring boot에서 이야기하는 **API** 방식이다.

## 2) JSON 형식 반환

한 가지 예제를 더 들어보자.

```java
@GetMapping("hello-api")
@ResponseBody
public Hello helloApi(@RequestParam("name") String name){
      Hello hello =new Hello();
      hello.setName(name);
      return hello;
    }

static class Hello{
    private String name;

    public String getName() {
            return name;
    }

	public void setName(String name) {
           this.name = name;
       }
    }
```

**Hello**라는 Class를 만들고(`static` : Class내 Class 선언 가능), 객체를 생성한 후 반환해보자.

```
파일명 : HelloController.java
위치 : src\main\java\hello.hellospring\controller\HelloController.java
```

````java
package hello.hellospring.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {

    @GetMapping("hello")
    public String Hello(Model model){
        model.addAttribute("data","hello!!");
        return "hello";
    }

    @GetMapping("hello-mvc")
    public String helloMVC(@RequestParam("name") String name,Model model){
        model.addAttribute("name",name);
        return "hello-template";
    }

    @GetMapping("hello-string")
    @ResponseBody
    public String helloString(@RequestParam("name") String name){
        return "hello " + name;
    }

    @GetMapping("hello-api")
    @ResponseBody
    public Hello helloApi(@RequestParam("name") String name){
        Hello hello =new Hello();
        hello.setName(name);
        return hello;
    }

    static class Hello{
        private String name;

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }
}

````

서버를 재실행하고, 위 `http://localhost:8000/hello-api?name=spring!!!!!!!!`에 접속해보자.

![image](https://user-images.githubusercontent.com/49560745/103977220-1b616000-51bc-11eb-9a65-e8b71a22051d.png)

`{key: value}`쌍의 `JSON` 데이터 반환되는 것을 확인할 수 있다. 이처럼 **API** 방식은 객체 자체를 return 해줄 수 있고, 이를 `JSON` 형식으로 변환해준다.



## @ResponseBody 원리

`@ResponseBody`는 HTTP의 BODY에 문자 내용을 직접 반환한다. `@ResponseBody`가 동작하는 원리는 다음과 같다.

![image](https://user-images.githubusercontent.com/49560745/103977627-00432000-51bd-11eb-9e10-4a706e76904c.png)

```
1) 웹 브라우저 요청
ex) localhost:8000/hello-string?name=spring
	localhost:8000/hello-api?name=spring
	
2) 내장 톰캣 서버, 컨텐츠 찾기 
  스프링 컨테이너 접근
  => helloController에 "hello-string" / "hello-api" 매핑 존재
  => @ResponseBody 태그 발견
  
3) return 형태에 따라 
	HttpMessageConverter 선택
	
	객체 : JsonConverter 동작
	문자열 : StringConverter 동작
	
* [참고] - 클라이언트의 HTTP Accept 해더와 서버의 컨트롤러 반환 타입 정보 
둘을 조합해서 HttpMessageConverter 가 선택된다.

4) 객체 혹은 문자열을 브라우저에 그대로 반환

```

이외에도 사용자 설정에 따라 `XML`, Google의 `Gson`형식으로 return 할 수 있다. 현업에서는 이 부분은 거의 건드리지 않고, `default`로 사용한다고 한다. `default` 설정은 아래와 같다. 참고로 `Jackson2`는 범용적으로 사용되는 검증된 `JSON`라이브러리이다.

```
기본(default) 문자처리 : StringHttpMessageConverter 동작
기본(default) 객체처리 : MappingJackson2HttpMessageConverter 동작
```

<br/>

**[참고] Accept 요청 HTTP 헤더**

Accept 요청 HTTP 헤더는 MIME 타입으로 표현되는,클라이언트가 이해 가능한 타입이 무엇인지 알려준다. MIME(Multiple Internet Mail Extensions)은 바이트의 문서, 파일, 형식의 표준이다.

- 문법

```
Accept: <MIME_type>/<MIME_subtype>
Accept: <MIME_type>/*
Accept: */*

// Multiple types, weighted with the quality value syntax:
Accept: text/html, application/xhtml+xml, application/xml;q=0.9, */*;q=0.8
```

- 예제

```
Accept: text/html
Accept: image/*
Accept: text/html, application/xhtml+xml, application/xml;q=0.9, */*;q=0.8
```



<br/>

# Reference

- [김영한님의 스프링-입문-스프링부트](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49577?tab=curriculum)

- [Accept - MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Accept)

  

