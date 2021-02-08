---
title: Clustered vs NonClustered (index 개념)
toc: true
categories:	
    - Database
tags:
- 데이터베이스
- Clustered 
- NonClustered 
last_modified_at: 
---

 

 이번 포스팅에서는 `Database`의 `index` 와 관련된 **Clustered**와 **NonClustered**의 개념을 알아보자.



##  인덱스(Index)란 ?

```
데이터베이스 분야에서 테이블에 대한 동작 속도를 높여주는 자료구조
```

![index](https://user-images.githubusercontent.com/49560745/107173438-200f7300-6a0b-11eb-88f7-4d7fc78a8c3c.png)

`Database`에서 말하는 `index`는 일반적인 책에서 말하는 **목차**에 비유할 수 있다. 만약 책에서 특정 챕터를 찾아보고 싶다면, 책의 목차(index)를 찾고 목차에 적힌 페이지로 이동하면된다. `index`도 마찬가지이다. 데이터의 **위치를 가리키는 지표**와 같은 것이다. 따라서, 빠른 시간내에 원하는 자료를 찾을 수 있다는 장점이있다. 

`Database`에서 `index`의 구조는 크게 `Clustered` 와 `NonClustered`로 나뉜다. 이제 이 두 가지 **타입**의 개념에 대해 살펴보자.

<br/>

## Clustered

```
Cluster : 군집
Clustered : 군집화
Clustered Index : 군집화 된 인덱스
```

**클러스터 형** 인덱스는 데이터가 테이블에 물리적으로 저장 되는 순서를 정의한다.  즉, 특정 컬럼에 의해 데이터들이 순서를 갖는 것이다. 아래 테이블은 `id`에 의해 데이터들이 군집화 된 상태라고 할 수 있다.

| id   | name   |
| ---- | ------ |
| 1    | 김범수 |
| 2    | 나얼   |
| 3    | 박효신 |
| 4    | 이수   |

테이블 데이터는 오직 한 가지의 방법으로만 정렬되기 때문에 오직 테이블 당 하나의 **클러스터 형** 인덱스만 존재할 수 있다. `Database`에서 `primary key`의 제약조건(constraint)은 **클러스터 된** 인덱스를 자동으로 만든다. 쉽게 말해,  `id`를 `primary key` 로 설정했을 때, 아래와 같은 군집화 된 구조를 갖게 된다.

```sql
CREATE DATABASE schooldb
          
CREATE TABLE student
(
    id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    gender VARCHAR(50) NOT NULL,
    DOB datetime NOT NULL,
    total_score INT NOT NULL,
    city VARCHAR(50) NOT NULL
 )
```





## NonClustered





<br/>

# Reference

-  [SQLShack - INDEX](https://www.sqlshack.com/what-is-the-difference-between-clustered-and-non-clustered-indexes-in-sql-server/)
-  [10분 테코톡 - INDEX](https://www.youtube.com/watch?v=NkZ6r6z2pBg)

- [인덱스(INDEX)의 모든 것](http://blog.naver.com/PostView.nhn?blogId=webwizard83&logNo=60171496664)