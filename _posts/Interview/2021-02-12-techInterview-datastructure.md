---
title: Datastructure 기술 면접 정리
toc: true
categories:	
    - Interview
tags:
- Spring
last_modified_at: 
---



`Daily Update`

## Datastructure

### Map vs HashTable

#### Map

- `Map`은 레드블랙트리 기반의 자료구조로 모든 자료가 정렬되어 저장된다.
- `Olog(n)`을 보장하며 자료를 정렬한다.
- 키 값의 분포가 고르지 않을 때 `insert`, `delete` 성능이 저하될 수 있다.

#### HashTable

- `Table`을 통해 데이터를 참조하므로 정렬이 필요없다.
- 그렇기 때문에 `search`, `insert`, `delete` 의 성능이 `O(1)`으로 보장된다.

