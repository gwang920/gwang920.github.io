---
title: SQL 쿼리 실행 과정 (6 STEP)
toc: true
categories:	
    - Database
tags:
- 데이터베이스
- sql
- 쿼리 실행 과정
last_modified_at: 
---

 

 이번 포스팅에서는 `SQL` 쿼리의 실행과정에 대해 알아보려 한다. `SQL` 쿼리의 실행과정을 이해한다면, 앞으로 쿼리문을 조금 더 수월하게 작성할 수 있을거라 생각한다.



##  쿼리 프로세스

`SQL`의 쿼리문 실행 프로세스는 크게 **6 단계**로 구분할 수 있다.

```
1. 데이터 가져오기 (From, Join)
2. 조건문 행 필터링 (Where)
3. 그룹핑 (Group by)
4. 그룹핑 결과 필터링 (Having)
5. 결과 리턴 (Select)
6. 결과 정렬 (Order by & Limit / Offset)
```

기본적인 흐름을 눈대중으로 파악했다면, 예제를 통해 실제로 어떻게 동작되는지 확인해보자. 예제 테이블은 아래와 같다.

<br/>

![쿼리프로세스-table](https://user-images.githubusercontent.com/49560745/107364626-08291380-6b1f-11eb-97c3-8a1549ac47f3.png)



**Empyolee** 테이블에는 직원의 **성**과 직무의 **ID 번호**가 하나의 행으로 데이터가 저장되어있다. 그리고 **JOB** 테이블에는 직무의 **ID 번호**와 이에 해당하는 **직무 이름**으로 데이터가 구성되어있다. 

이제, 두 테이블에서 

직무가 **Front-End** 이거나 **Back-End** 이면서,

같은 **Name**을 가진 사람이 두명 이상인 **Name** 데이터를 

**Name** 오름차순으로 정렬하는 쿼리문을 실행해보자.

```javascript
SELECT Emplyoee.Name
FROM Emplyoee
JOIN job
ON Emplyoee.jobid= job.jobid 
WHERE job.jobName != 'AI'
GROUP BY Emplyoee.Name 
HAVING COUNT(*) >= 2
ORDER BY Emplyoee.Name ASC
```

 

## 1. 데이터 가져오기









<br/>

# Reference

-  [towards - The 6 Steps of a SQL Select Statement Process](https://towardsdatascience.com/the-6-steps-of-a-sql-select-statement-process-b3696a49a642)
