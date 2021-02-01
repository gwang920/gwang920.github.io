---
title: Java - 자바 코딩테스트 문법 정리
toc: true
categories:	
    - Java
tags: 
- Java
- 문법
last_modified_at:
---

   코딩테스트에서 자주 사용되는 `Java` 문법 정리, `Daily Update`

## 깊은 복사(deep copy)

#### ArrayList

- `ArrayList`를 깊은 복사하고 싶다면, `복사되는배열.addAll(복사할배열)` 메서드를 사용하면된다.

- `ArrayList` **w**를 `ArrayList` **copy_w**에 깊은복사

```java
ArrayList<Integer> w=new ArrayList<Integer>();
ArrayList<Integer> copy_w=new ArrayList<Integer>();
copy_w.addAll(w);
```





<br/>

# Reference

