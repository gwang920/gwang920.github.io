---
title: OS 기술 면접 정리
toc: true
categories:	
    - Interview
tags:
- OS
last_modified_at: 
---



`Daily Update`

## OS

### 로드벨런서

- 부하를 분담해주는 역할을 한다.
- **scale up** : 서버의 성능을 높이는 것
  - 인스턴스를 업데이트하는동안 서비스를 할 수 없다.
- **scale out** : 서버의 대수를 늘리는 것
  - 서버가 늘어날 때 마다 도메인이 새로 필요하다.

### Proxy

- 클라이언트와 서버간의 중계서버로, 통신을 대리 수행하는 서버

### Forward Proxy

```java
Clients => Forward Proxy => Internet => Servers
```

- 캐시 : 동일한 요청은 캐시로 처리할 수 있다. (클라이언트가 요청한 내용을 캐싱)
- 익명성 : 누가 요청을 보내는지 서버가 알 수없다. (클라이언트가 보낸 요청을 감춤)

### Reverse Proxy

```java
Clients => Internet => Reverse Proxy => Servers
```

- 캐시 (Forward proxy와 동일)
- 익명성 (Forward proxy와 동일)
- 로드밸런서 기능 : 부하 분산(요청을 나눠줌)

