---
title: 정규표현식
toc: true
categories:	
    - etc
tags: 
- 정규표현식
- regular Expression
last_modified_at:
---

 [정규표현식 실습 site](https://regexr.com)



```
숫자 0 - 9 선택
[0-9]

숫자 135선택
[135]

숫자 잡을 때
[\d]

숫자 3개
\d{3}

숫자 3개 혹은 4개
\d{3,4}

전화번호 (010-1234-1234)
\d{2,3}[\s-]?\d{3,4}[*-]?\d{4}

숫자 아닌 것(대문자는 항상 반대)
[\D]
```



```
문자(숫자,영대소문자)
[\w]

영소문자
[a-z]

영대문자
[A-Z]

한글
[가-힣]

특수문자,한글
[\W]

공백
[\s]
[\s]* (공백이 0개 이상)

- .
임의의 한 문자

ex)
a와 c 사이의 한개의 문자가 있는것
a.c

- ?
0개 혹은 1개의 문자


ex)
ab?
a나b가 한개인경우

- ab?c

0개 혹은 1개 이상의 문자
*

- ab*c

ac 가능
abc 가능
abbbbc 가능



```



<br/>

# Reference

- [youtube - 정규표현식 15분만에 이해하기](https://www.youtube.com/watch?v=Gg0tlbrxJSc)
