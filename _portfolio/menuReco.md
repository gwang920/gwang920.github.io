---
title: 오늘 뭐 먹지?
excerpt: Spring Framework을 기반으로 룰렛을 도입해 재미요소를 더 하고, 식당 검색 및 평점/리뷰 기능을 도입해 식당을 추천해주는 웹 서비스
header:
  image: /assets/images/whateat.jpg
  teaser: /assets/images/whateat.jpg
sidebar:
  - title: "담당 역할"
    text: "Front-End & Back-End"
  - title: "기여도"
    text: "30%, 4인 프로젝트"
gallery:
  - url: /assets/images/MenuRecommend/메뉴메인.jpg
    image_path: assets/images/MenuRecommend/메뉴메인-th.jpg
    alt: "placeholder image 1"
  - url: /assets/images/MenuRecommend/메뉴회원가입.jpg
    image_path: assets/images/MenuRecommend/메뉴회원가입-th.jpg
    alt: "placeholder image 2"
  - url: /assets/images/MenuRecommend/메뉴로그인.jpg
    image_path: assets/images/MenuRecommend/메뉴로그인-th.jpg
    alt: "placeholder image 3"
  - url: /assets/images/MenuRecommend/메뉴메뉴추가.jpg
    image_path: assets/images/MenuRecommend/메뉴메뉴추가-th.jpg
    alt: "placeholder image 4"
  - url: /assets/images/MenuRecommend/메뉴룰렛돌리기.jpg
    image_path: assets/images/MenuRecommend/메뉴룰렛돌리기-th.jpg
    alt: "placeholder image 5"
  - url: /assets/images/MenuRecommend/메뉴위치검색.jpg
    image_path: assets/images/MenuRecommend/메뉴위치검색-th.jpg
    alt: "placeholder image 6"
  - url: /assets/images/MenuRecommend/메뉴리뷰.jpg
    image_path: assets/images/MenuRecommend/메뉴리뷰-th.jpg
    alt: "placeholder image 7"
  
layout: archive
classes: layout--home
toc: true
---



## On This Page

```
- 주제 및 기획의도
- 기능 개요
- 시스템 구조도 및 시나리오
- 개발 환경
- ERD 설계
- 화면 설계
```





## 주제 및 기획의도

```
- 주제 : Spring Framework기반 메뉴추천 시스템
- 기획의도 : 식사 시간마다 고민되는 메뉴 선택을 돕는 웹서비스 개발
```





## 기능 개요

```
- 회원가입을 통해 사용자를 인식하여 관심 메뉴 / 기피 메뉴 선택권한을 이용자에게 부여
- 위치 검색 기능을 도입하여 룰렛에서 선정 된 메뉴에 대한 식당 추천
- 댓글 기능, 별점 평점 기능, 5가지 표현 기능 구현
```





## 시스템 구조도 및 시나리오

[![image](https://user-images.githubusercontent.com/49560745/101629531-d9ca8180-3a64-11eb-9787-5cfe40075abd.png)](https://user-images.githubusercontent.com/49560745/101629531-d9ca8180-3a64-11eb-9787-5cfe40075abd.png)

[![image](https://user-images.githubusercontent.com/49560745/102046855-861eb600-3e1f-11eb-91fa-54911180a94c.png)](https://user-images.githubusercontent.com/49560745/102046855-861eb600-3e1f-11eb-91fa-54911180a94c.png)

```
1. 회원가입/로그인
2. 메뉴 선정(선호메뉴/비선호메뉴 선택 가능)
3. 선택된 메뉴 데이터 룰렛 적재
4. 룰렛 돌리기(최종 메뉴 선정)
5. 선정메뉴 + 검색(사용자가 원하는 위치) = 식당 리스트업
6. 해당 식당 별점 및 리뷰
```





## 개발 환경

[![image](https://user-images.githubusercontent.com/49560745/101629583-efd84200-3a64-11eb-9793-8a3312ee1664.png)](https://user-images.githubusercontent.com/49560745/101629583-efd84200-3a64-11eb-9793-8a3312ee1664.png)



## ERD 설계

**사진 Click!**

[![image](https://user-images.githubusercontent.com/49560745/101631109-2dd66580-3a67-11eb-8ee2-5a6c955b6d58.png)](https://user-images.githubusercontent.com/49560745/101631109-2dd66580-3a67-11eb-8ee2-5a6c955b6d58.png)

## 화면 설계

{% include gallery caption="프로젝트 화면 Site 맵 - 이미지를 클릭해보세요!" %}

#### 소스코드

https://github.com/gwang920/MenuRecommandationSystemProject