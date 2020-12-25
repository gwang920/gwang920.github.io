---
layout: archive
classes: layout--home
author_profile: true
title: Github 블로그 커스터마이징 - 카테고리
categories:	
    - Blog_config
tags:
    - github.io - 깃허브 블로그
last_modified_at:
---



### Github 블로그 커스터마이징 - 카테고리편

jekyll를 기반으로 깃허브 블로그를 커스터마이징해보자.

이번편은 네비게이션바에 카테고리 항목을 추가해, 게시한 글을 범주화 시키는 작업을 진행한다. 테마는 'minimal-mistakes'를 활용했다. 



##### 1. 게시글에 category 등록하기

![image](https://user-images.githubusercontent.com/49560745/103126714-85fda080-46d2-11eb-9b18-205621a70e61.png)

- title : #게시글 제목
- categories : # - 카테고리 제목
- tags : # 태그
- last_modified_at: #수정 시간



이 게시글은 _posts/2020-12-25-category-config.md로 저장되어있다. 우선, 위 사진처럼 분류 기준에 따라 YFM 설정을 완료한다.  



#### 2. categories 페이지 등록하기

![image](https://user-images.githubusercontent.com/49560745/103126697-6f574980-46d2-11eb-8d36-40c730163a75.png)

- title : #카테고리 페이지 제목
- layout:  #categoires
- permalink: #/categories/

```
categories 페이지는 _pages/category_archive.md로 저장되어있다. 
반드시 이 형식(파일명 _archive.md)과 일치하도록 파일명을 설정하고, 
해당 경로에 집어넣어줘야한다. 
참고로, permalink는 _config.yml 파일의 category_archive설정의 
path 경로와 같음을 기억하자!
```





![image](https://user-images.githubusercontent.com/49560745/103127024-94988780-46d3-11eb-950f-5a1aaf8da003.png)



#### 3. 



### Reference

- https://mmistakes.github.io/minimal-mistakes/docs/layouts/#layout-categories

- https://devinlife.com/howto%20github%20pages/category-tag/



