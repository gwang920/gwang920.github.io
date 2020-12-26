---
title: Github 블로그 커스터마이징 - Posts
categories:	
    - Blog_config
tags:
- github.io
- 깃허브블로그
last_modified_at: 
---



### Github 블로그 커스터마이징 - Posts편

jekyll를 기반으로 깃허브 블로그를 커스터마이징해보자. 

이번편은 **블로그에 글을 게시하는 방법에 대해 아주아주 간단한 적용법**만을 알아보려 한다.  

테마는 **minimal-mistakes**를 적용했다.



순서는 다음과 같다

**1) md 파일 형식으로 게시글을 작성한다.**

**2) _posts 폴더에 게시글을 저장한다.**



우선 첫번째과정부터 살펴보자.

md 파일은 github를 사용해봤다면 익숙할 것이고, github.io에서도 사용하는 방식은 동일하다. 단, 아래 처럼 한가지 설정이 필요하다.

```
파일명 : 2020-12-26-posts-config.md
위치 : /_posts/2020-12-26-posts-config.md
```

```
---
layout: archive
classes: layout--home
author_profile: true
---
```



**layout**

jekyll 테마에는 다양항 layout이 포함되어있다. (_layousts 폴더에서 확인할 수 있다.) layout은 게시글의 형식 즉, Frame이라 할 수 있다. 이 레이아웃을 적용하지 않고, 블로그에 글을 게시한다면 네비게이션바나 프로필과 같이 부가적인 요소들이 나타나지 않고, 순수한 md 파일 내용만이 블로그에 기재된다.



**classes**

classes는 HTML, CSS를 다뤄봤다면 익숙할 것이다. 게시글에 원하는 클래스를 적용해 게시글을 꾸밀 수 있다. 



**author_profile**

author_profile은 사진의 좌측 프로필을 표시할 것이냐의 여부를 결정해준다. default는 false이고, 항상 표시하고 싶을경우 true로 설정해주자.





### Reference

- https://mmistakes.github.io/minimal-mistakes/docs/layouts/#layout-categories


