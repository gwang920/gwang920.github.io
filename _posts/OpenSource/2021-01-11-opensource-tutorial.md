---
title: 오픈소스 기여하기(Contributor) - 튜토리얼
toc: true
categories:	
    - Open Source
tags:
- Open Source
last_modified_at: 
---

  오픈소스에 기여하는 방법을 실습해보자. 이번 포스팅은 **Test Repository**를 활용해 오픈소스 **Fork** 부터 **Pull Request** 까지의 방법을 실습을 통해 알아보려한다.

# 오픈소스 기여하기 - 튜토리얼

### 1) Fork 하기

`Fork`는 "이 프로젝트에 **Contribute** 해보고 싶은데, 이거 일단 내 저장소로 복사해갈게." 라고 이해하면 쉬울 것이다.

![image](https://user-images.githubusercontent.com/49560745/104179225-dc970880-544e-11eb-9cc8-d695546e541e.png)

 **Contribute** 하고자 하는 프로젝트를 Fork한다. 우측 상단에 `Fork` 버튼을 눌러 본인의 `Github Repository`에 복사한다. 이때, `Fork`한 저장소는 원본(Repository)와 연결되어있다. 따라서, 원본 저장소에 변화가 발생하면 `Forked`된 , 즉 내 저장소로 복사 된 `respository`에 변경 사항을 반영할 수 있다.

![image](https://user-images.githubusercontent.com/49560745/104177225-c50a5080-544b-11eb-9783-be4020d565aa.png)

`Fork`가 완료되면 `본인 Github아이디 / Fork한 repository`에 새로운 저장소가 생긴 것을 확인할 수 있다. `Fork`를 통해 내 버전의 `repository`가 생성된 것이다. 이제야 비로소 해당 `repository`에 `Clone` 및 `Commit`할 권한이 생겼다고 할 수 있다.

![image](https://user-images.githubusercontent.com/49560745/104178326-79f13d00-544d-11eb-835c-7cde348a149d.png)



### 2) Clone 하기

 이제, `Remote` 공간 (본인의 `Github repository`)에 있는 `repository`를 본인의 `local` 환경(본인의 컴퓨터)로 `Download` 하는 것을 `clone`이라 한다. 

![image](https://user-images.githubusercontent.com/49560745/104179503-4ca58e80-544f-11eb-9a5f-11230e248b7a.png)

`clone`을 하려면 `repository` 주소가 필요하다. `repository` 주소는 `fork`한 본인 `repository` 우측 상단에 `Code`에서 찾을 수 있다. 클릭 후에 `repository`경로를 복사하자. 

![image](https://user-images.githubusercontent.com/49560745/104179808-c6d61300-544f-11eb-9637-10496b5fbaba.png)

경로한 주소는 다음과 같다. `$ git clone https://github.com/본인 아이디/githubtutorial.git`

`Git Bash`를 실행하기전에 `clone`한 `repository`를 저장할 공간인 폴더를 원하는 경로에 하나 생성하자. `cd`명령어를 통해 해당 폴더로 이동 한후 `git clone`을 입력하고 복사한 명령어를 붙여넣고, 실행하자.

![image](https://user-images.githubusercontent.com/49560745/104180487-8a56e700-5450-11eb-95f0-b69c6224a1bd.png)

해당 폴더에 `githubtutorial`폴더가 생성되어있다면, 정상적으로 `clone`이 완료된 것이다.

![image](https://user-images.githubusercontent.com/49560745/104180549-a5295b80-5450-11eb-8f5f-7af63e7989d4.png)



# Reference

- Techtonic 2020 - Open Source ssession
