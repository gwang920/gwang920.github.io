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

### 3) Issue 선택

project를 `clone`까지 해왔다면, 이제 **"어떤 부분에 `contribute`해야 되지?"** , **"잘 짜놓은 코드 혹은 대규모 프로젝트에 과연 내가 `contritbute`할 여지가 있을까 ?"** 고민될 것이다.  이럴때 확인하는 것이 `issue`이다. 대부분의 규모있는 `Open Source`프로젝트는 **이슈 트래킹 시스템**(필요에 의해 이슈 목록을 관리하고 유지보수하는 것)을 사용한다. 

처음 `Open Source`에 기여한다면,  `good first issue` 태그를 확인해보자. `good first issue` 태그에 해당하는 `issue`는 몇줄 혹은 몇자만 고치면 해결되는 간단한 이슈에 해당한다.

이번 포스팅에서는 `githubtutorial` 프로젝트 내 `issue`에서 실습해보자. 원본 `repository`에 `issues` 탭을 클릭하면 `issue`목록이 보일 것이다. 아래 처럼 보통 `issue`는  `[프로젝트이름]-[이슈번호] <이슈 제목>` 의 형식으로 구성된다. 이제 해당 `issue`를 클릭해보자.

![image](https://user-images.githubusercontent.com/49560745/104181793-b96e5800-5452-11eb-8be1-b56fa3ac2b71.png)

 이제, 우측의 `Assignees`를 통해 자기 자신에게 `assign`하도록 하자. 그렇게 되면 비로소 해당 `issue`가 자신의 `issue`가 되었다고 볼 수 있다.

해당 포스팅에서는 아직 원본 `repository`의 `collaborator`로 등록되어 있지 않아 **현재(2011-01-11) **`Assignees` 탭을 사용할 수 없습니다. 자세한 내용은 [삐멜 소프트웨어 엔지니어 - 오픈소스](https://imasoftwareengineer.tistory.com/5#recentComments ) 이 포스팅을 참고하시기 바랍니다.



![image](https://user-images.githubusercontent.com/49560745/104182622-11f22500-5454-11eb-9cba-b7d9b8178e2c.png)

### 4) Branch

`contribute`를 완벽하게 이해하고, 시작하려면 `branch` 개념 이해가 필요하다. `branch`는 말그대로 **분기**이다. 가지를 쳐서 효율적으로 개발하고, 수정사항을 `commit` 하기 위함이다. 보통 `master` 브랜치는 `release` 브랜치인 경우가 대부분이다. 즉, `master` 브랜치로 **배포**하면서, 다른 `branch`에서 기능을 분류하여 **개발하고, 수정**하는 것이다. 그렇기 때문에 `master` 브랜치에 자신이 해결하던 `issue` 혹은 개발하던 것을 직접적으로 `commit`하는 경우는 흔치 않다.

일단 아래를 보자. `master` 브랜치 이외의 두 개의 `branch`를 확인할 수 있다.

![image](https://user-images.githubusercontent.com/49560745/104183813-e2441c80-5455-11eb-83a4-fbebd897c9a4.png)

이를 그림으로 표현하면 다음과 같다.

![image](https://user-images.githubusercontent.com/49560745/104185159-ed984780-5457-11eb-9efa-0d2b3bb81b97.png)

[색이 있는 동그라미는 commit, 회색 동그라미은 branch off 또는 merge in을 의미]

- `master` 브랜치는 배포를 위한 브랜치
- `feature/develop` 개발자들이 개발하기 위한 브랜치
- `feature/develop1` 과 같이 `branch`를 생성해 그곳에 개발을 진행하면 된다. 

마스터 브랜치가 존재하고 그 이후에 branch off된 feature/develop브랜치가 존재한다. 브랜치의 이름은 오픈소스마다 다르고 어떻게 브랜치를 이용하는지도 오픈소스마다 다르다. 따라서 어떤 오픈소스에 참여 한다면 그 오픈소스의 문서를 반드시 읽어보기 바란다. 대부분의 오픈소스는 컨트리뷰터들을 위한 가이드가 준비되어있다.

# Reference

- [삐멜 소프트웨어 엔지니어 - 오픈소스](https://imasoftwareengineer.tistory.com/5#recentComments )
