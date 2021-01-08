---
title: Spring boot기반 Web Application 개발[7] - API
toc: true
categories:	
    - Spring boot
tags:
- Spring boot
- Spring Web
last_modified_at:
---



Spring boot Web 개발에서 이야하기는 **API**방식을 알아보자.

이전에 살펴봤던 [정적컨텐츠](https://gwang920.github.io/spring%20boot/springboot(5)-static/), [템플릿 엔진](https://gwang920.github.io/spring%20boot/springboot(6)-mvc/)으로 사용자에게 보여질 데이터를 반환하는 방식 중 하나를 **API** 방식이라고한다.

```
정적컨텐츠 - 정적으로 HTML 파일을 그대로 Client(브라우저)에 리턴한다.
템플릿엔진(MVC) - View를 랜더링 된 HTML을 Client(브라우저)에 전달해준다.
API 방식 - 주로 객체를 JSON형태로 리턴하고자할 떄 사용하는 방식이다.
```

# API 방식

이제, 실습을 통해 **API**방식을 알아보자.

<br/>

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

![image](https://user-images.githubusercontent.com/49560745/103977627-00432000-51bd-11eb-9e10-4a706e76904c.png)

# Controller

기존에 작성했던 `HellocController.java`파일에 아래코드를 구현하자.

```java
@GetMapping("hello-mvc")
    public String helloMVC(@RequestParam("name") String name,Model model){
        model.addAttribute("name",name);
        return "hello-template";
    }
```

- `url`매핑은 `@GetMapping`어노테이션을 활용해 "hello-mvc"로 설정했다. 

- `@RequestParam`어노테이션을 활용해 `url`의 name 값을 가져온다. 

- `model.addAttrubute`로 'name' 값을 Html 파일에 넘겨준다.

- hello-template라는 View 파일을 return 해준다.

<br/>

```
파일명 : HellocController.java
위치 : src\main\java\hello\hellospring\controller\HelloController.java
```

```java
package hello.hellospring.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class HelloController {

    @GetMapping("hello")
    public String Hello(Model model){
        model.addAttribute("data","hello!!");
        return "hello";
    }
	// 추가된 코드
    @GetMapping("hello-mvc")
    public String helloMVC(@RequestParam("name") String name,Model model){
        model.addAttribute("name",name);
        return "hello-template";
    }
}

```

<br/>

# View

Controller에서 return 해주는 View 파일을 만들어보자. `resources > templates`에 `hello-template.html`파일을 생성하고, 아래 코드를 작성하자.

```
파일명 : hello-template.html
위치 : src\main\resources\templates\hello-template.html
```

````html
<html xmlns:th="http://www.thymeleaf.org">
<body>
<p th:text="'hello ' + ${name}">hello! empty</p>
</body>
````

- <html xmlns:th="http://www.thymeleaf.org">  : thymeleaf 템플릿 엔진을 사용하기 위함이다.
- `${name}`은 `HellocController.java1`의 helloMVC 메소드에서 구현 한 model.addAttribute("name",name); 으로 설정된다.

<br/>

# 실행

우선, https://http://localhost:8000/hello-mvc에 접속해보자. 

![image](https://user-images.githubusercontent.com/49560745/103727961-f20bcd00-501f-11eb-8f65-469a51d196e2.png)

**Error Page**가 로드될 것이다. 매핑된 "hello-mvc"에 접근했지만, `@RequestParam`에서 설정한 name값이  `url`에존재하지 않기 때문이다.

<br/>

다시, https://http://localhost:8000/hello-mvc?name=spring 으로 접속해보자. 여기서 name은 파라미터 인 "spring"으로 설정되었다.

![image](https://user-images.githubusercontent.com/49560745/103728125-778f7d00-5020-11eb-84c4-b29b795dd7cc.png)

이제, 정상적으로 html 파일이 로드되는 것을 확인할 수 있다.

<br/>

# API 동작 원리

**API** 방식이 동작하는 과정은 다음과 같다.

![image](https://user-images.githubusercontent.com/49560745/103728221-b6bdce00-5020-11eb-8c72-f6011c6e84ab.png)

```
1) 웹 브라우저 요청
ex) localhost:8000/hello-mvc

2) 내장 톰캣 서버, 컨텐츠 찾기 
  스프링 컨테이너 접근
  => helloController에 "hello-mvc" 매핑 존재
  
3) model을 viewResolver에 전달 (파라미터 => name: spring)

4) hello-template.html 반환 (Theymeleaf 템플릿 엔진 처리) 
```



<br/>

# Reference

- [위키백과 MVC패턴](https://ko.wikipedia.org/wiki/%EB%AA%A8%EB%8D%B8-%EB%B7%B0-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC)

- [김영한님의 스프링-입문-스프링부트](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49577?tab=curriculum)

  

