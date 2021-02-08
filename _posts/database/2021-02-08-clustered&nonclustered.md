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



## Clustered

```
Cluster : 군집
Clustered : 군집화
Clustered Index : 군집화 된 인덱스
```

**클러스터 형** 인덱스는 데이터가 테이블에 물리적으로 저장 되는 순서를 정의(설정)한다.  즉, 특정 컬럼에 의해 데이터들이 순서를 갖는 것이다. 아래 테이블은 `id`에 의해 데이터들이 군집화 된 상태라고 할 수 있다.

![image](https://user-images.githubusercontent.com/49560745/107177426-2c98c900-6a15-11eb-9c47-087fc3212da1.png)

테이블 데이터는 오직 한 가지의 방법으로만 정렬되기 때문에 오직 테이블 당 하나의 **클러스터 형** 인덱스만 존재할 수 있다. 즉, 정렬되는 기준으로 오직 하나의 컬럼만을 선택할 수 있다. `Database`에서 `primary key`의 제약조건(constraint)은 **클러스터 된** 인덱스를 자동으로 생성하기 때문에 우리가 일반적으로 테이블을 생성할 떄, 자료가 정렬되어있는 것이다.

### 그래서 왜 **Clustered** 인가 ?

위 테이블에 `Name : 넬 , Birth : 1980` 데이터를 `ID : 2 ` 에 추가한다면, 테이블의 상태는 아래와 같을 것이다. 

![image](https://user-images.githubusercontent.com/49560745/107177408-21de3400-6a15-11eb-92fe-93e2789d46a5.png)

이것이 바로 **Clustered**이다. 순서는 오직 하나의 컬럼으로 결정되기 때문에 중간에 새로운 데이터가 삽입된다면 이후의 모든 컬럼을 한 칸씩 이동시켜줘야한다. `index`가 **군집화** 되어있기 때문이다. 이처럼 `index`는 검색 속도를 향상시킨다는 장점이 있지만, 새로운 데이터를 삽입할 때는 많은 비용이 소모되는 단점 또한 존재한다.



## NonClustered

```
NonCluster : 비 군집
NonClustered : 비 군집화
NonClustered Index: 군집화되어 있지 않은 인덱스
```

**논 클러스터 형** 인덱스는 말 그대로 **클러스터 형**의 반대인 군집화 되어있지 않은 인덱스 타입이다. 그렇기 때문에 테이블에 저장 된 물리적인 순서에 따라 데이터를 정렬하지 않는다. 

![textbook index](https://user-images.githubusercontent.com/49560745/107176299-4f75ae00-6a12-11eb-9a86-ee82b1a3df9c.png)

그리고 **논 클러스터 형** 인덱스는 테이블 데이터와 함께 테이블에 저장되는 것이 아니라 **별도의 장소**에 저장된다. 마치, 위 책에서 `index` 페이지를 따로 나눈것 처럼 말이다.



<br/>

# Reference

-  [SQLShack - INDEX](https://www.sqlshack.com/what-is-the-difference-between-clustered-and-non-clustered-indexes-in-sql-server/)
-  [10분 테코톡 - INDEX](https://www.youtube.com/watch?v=NkZ6r6z2pBg)

- [인덱스(INDEX)의 모든 것](http://blog.naver.com/PostView.nhn?blogId=webwizard83&logNo=60171496664)