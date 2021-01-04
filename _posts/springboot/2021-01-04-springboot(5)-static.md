---
title: Spring boot기반 Web 구축하기[5] - 정적 컨텐츠
toc: true
categories:	
    - Spring boot
tags:
- Spring boot
- Spring Web
last_modified_at:
---



Spring boot기반 **정적 컨텐츠**에 대해 간단하게 알아보자.

# 정적 컨텐츠란?

```
변화가 없는 컨텐츠를 말한다. 보통 HTML,CSS,Img,javascript 파일 등 미리
서버에 저장해두고, 요청을 받으면 그저 응답만 해주면 되는 것들이다.
초창기 Web에서는 서버의 성능이 떨어져, Web 어플리케이션을
정적 컨텐츠로만 구성했다.

하지만, 최근에는 'FaceBook 친구 추천'이나 '유튜브 동영상 추천'기능
처럼 동적으로 컨텐츠를 생성하는 경우가 많아,
대부분 정적 + 동적 컨텐츠로 Web 어플리케이션을 구축하고 있다.
```

Spring boot에서는 정적 컨텐츠 기능을 제공한다.

자세한 내용은 [Spring Boot Features](https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-static-content)에서 "static content"를 검색해보자.

<br/>

# 정적 컨텐츠 생성

정적 컨텐츠를 생성하는 방법은 정말 간단하다.

**/static** 폴더 내에 파일을 생성하고, 해당 위치로 접근하면 정적 컨텐츠가 로드된다.

```
파일명 : hello-static.html
위치 : resources/static/hello-static.html
```

```html
<!DOCTYPE HTML>
<html>
<head>
 <title>static content</title>
 <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
정적 컨텐츠 입니다.
</body>
</html>
```

```
실행 : localhosts:8000/hello-static.html
```

![image](https://user-images.githubusercontent.com/49560745/103514425-ee593880-4eaf-11eb-92d9-1513505d909f.png)

# 정적 컨텐츠 동작 원리

**정적 컨텐츠**가 사용자 요청으로부터 로드되는 과정은 다음과 같다.

![image](https://user-images.githubusercontent.com/49560745/103514630-5c9dfb00-4eb0-11eb-8f92-98e15afdc9f0.png)

```
1) 웹 브라우저 요청
ex) localhost:8000/hello-static.html

2) 내장 톰캣 서버, 컨텐츠 찾기 
  1 - 스프링 컨테이너 접근
  => hello-static 관련 컨트롤러가 존재하지 않음
  
  2 - static 폴더 접근
  => hello-static.html 존재
  
3) "hello-static.html" 브라우저로 전송
```

<br/>

# 정적 컨텐츠 더 알아보기

## 정적 리소스 mapping URL 패턴

![image](https://user-images.githubusercontent.com/49560745/103527492-ca085680-4ec5-11eb-9574-2e7709e46362.png)



![image](https://user-images.githubusercontent.com/49560745/103526482-56b21500-4ec4-11eb-9daa-0480519d9475.png)



정적 리소스는 기본적으로 `/**(루트)` 부터 매핑이 된다. 따라서, 위 예시처럼 `localhost:8000/hello-static.html`을 요청하면 정적 리소스의 location(위치)에서 정적 컨텐츠를 찾아 응답한다.



### mapping 패턴 변경하기

`/resources/appication.properties` 파일에서 정적 리소스 매핑 패턴을 설정할 수 있다.

![image](https://user-images.githubusercontent.com/49560745/103527310-7dbd1680-4ec5-11eb-837e-fea53e950c65.png)

`srping.mvc.static-path-pattern=/` 이후에 경로를 지정할 수 있다. (default는 `srping.mvc.static-path-pattern=/**`)이다. 

mappig 패턴을 `/static/**`으로 변경해보자.



![image](https://user-images.githubusercontent.com/49560745/103527665-0b990180-4ec6-11eb-8037-c0a3cdbdb48d.png)

`hello-static.html` 파일은 여전히 `/static` 에 위치하고 있지만, `localhost:8000/hello-static.html` 을 요청하면 Errop page 가 로드된다.



![image](https://user-images.githubusercontent.com/49560745/103526597-7f3a0f00-4ec4-11eb-8d75-1f149582f135.png)

**appication.properties**에 설정한 매핑 패턴으로 접근하면 `hello-static.html`이 로드됨을 확인할 수 있다.





## 정적 리소스 Location

기본적으로 Spring boot는 정적 컨텐츠를 `/staic` or`/public` or `/resources` or `/META-INF/resources` 로 부터 불러온다. 즉,  4가지 경로는 정적 리소스의 위치를 뜻한다.

```
classpath:/META-INF/resources/
classpath:/resources/
"classpath:/static/"
"classpath:/public/"
```





# Reference

- https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49576?tab=curriculum

- https://armontad-1202.tistory.com/entry/%EC%9B%B9%EC%9D%98-%EC%A0%95%EC%A0%81-%EB%8F%99%EC%A0%81-%EC%BD%98%ED%85%90%EC%B8%A0-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EC%A0%95%EC%A0%81-%EB%8F%99%EC%A0%81-%EC%BD%98%ED%85%90%EC%B8%A0
- https://atoz-develop.tistory.com/entry/spring-boot-web-mvc-static-resources