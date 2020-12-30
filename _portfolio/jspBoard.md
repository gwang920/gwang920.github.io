---
title: JSP 게시판
excerpt: JSP를 활용한 게시판 서비스
header:
  image: /assets/images/board.jpg
  teaser: /assets/images/board.jpg
sidebar:
  - title: "담당 역할"
    text: "Front-End & Back-End"
  - title: "기여도"
    text: "100%, 개인 토이프로젝트"
layout: archive
classes: layout--home
toc: true
---



## On This Page

```
- 주제 및 기획의도
- 기능 개요
- 개발 환경
- ERD 설계
- 화면 설계
```





## 주제 및 기획의도

```
- 주제 : JSP를 활용한 게시판 제작
- 기획의도 : Spring MVC 패턴과 MVC1 패턴의 차이 알아보기
```



## 기능 개요

```
- 회원가입, 로그인 기능
- 게시판 기능
- 댓글 기능
- 클라이언트 삭제 요청 수행 시, isAvailable을 통해 DB에 데이터 보존
```





## 개발 환경

[![image](https://user-images.githubusercontent.com/49560745/103338477-e5d4bc80-4ac1-11eb-8488-69edd37d19f3.png)](https://user-images.githubusercontent.com/49560745/103338477-e5d4bc80-4ac1-11eb-8488-69edd37d19f3.png)



## ERD 설계

[![image](https://user-images.githubusercontent.com/49560745/103337133-a86e3000-4abd-11eb-8759-97a877f21512.png)](https://user-images.githubusercontent.com/49560745/103337133-a86e3000-4abd-11eb-8759-97a877f21512.png)



## 화면 설계



### 회원가입

[![image](https://user-images.githubusercontent.com/49560745/98510044-bd8cc680-22a5-11eb-95c4-709d265b03b9.png)](https://user-images.githubusercontent.com/49560745/103337306-39450b80-4abe-11eb-8aa9-1dd1d5467df3.png)

### 로그인

[![image](https://user-images.githubusercontent.com/49560745/98513962-15c6c700-22ac-11eb-8b0a-04a4bd85bb42.png)](https://user-images.githubusercontent.com/49560745/103337322-4661fa80-4abe-11eb-9c18-5476b1b8dc11.png)

### 게시판 목록

[![image](https://user-images.githubusercontent.com/49560745/98535043-ccd13b80-22c8-11eb-82a4-b941f59d247b.png)](https://user-images.githubusercontent.com/49560745/103337335-537ee980-4abe-11eb-99db-e76662aaecb9.png)

### 게시판 글쓰기

[![image](https://user-images.githubusercontent.com/49560745/98516195-891e0800-22af-11eb-865a-5136b9783c44.png)](https://user-images.githubusercontent.com/49560745/103337349-61346f00-4abe-11eb-9ac0-c2f646311d1b.png)

### 게시판 글보기

[![image](https://user-images.githubusercontent.com/49560745/98537750-158af380-22cd-11eb-962f-3804a91b6dcc.png)]((https://user-images.githubusercontent.com/49560745/103337362-6e515e00-4abe-11eb-86f9-acf3c8c2b87a.png))

## 게시판 글 수정

[![image](https://user-images.githubusercontent.com/49560745/98539819-4ae51080-22d0-11eb-8c85-2ce0186a9b09.png)](https://user-images.githubusercontent.com/49560745/98539819-4ae51080-22d0-11eb-8c85-2ce0186a9b09.png)

## 소스코드
https://github.com/gwang920/TIL/tree/master/JSP%20%EA%B2%8C%EC%8B%9C%ED%8C%90%20%EB%A7%8C%EB%93%A4%EA%B8%B0