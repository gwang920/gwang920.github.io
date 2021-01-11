---
title: Spring boot기반 Web Application 개발[8] - 회원 리포지터리 테스트(Junit)
toc: true
categories:	
    - Spring boot
tags:
- Spring boot
- Spring Web
last_modified_at: 
---



  자바는 테스트를 할 때, 주로 테스트 프레임워크인 `Junit`을 활용한다. 그런데 한 가지 의문이 든다. 자바의 main 메서드를 이용하거나 웹 애플리케이션의 컨트롤러를 통해 충분히 테스트가 가능한데, 왜 테스트 프레임워크를 이용해서 테스트를 진행할까? 

그 이유는 바로 위와 같은 방법들은 준비하고, 실행하는데 시간이 오래걸리기 때문이다. 그뿐만 아니라 반복실행이 어렵다는 단점이 있다. 그렇기 때문에, 여러 테스트를 한번에 실행하기에는 곤란하다. 따라서,  현업에서 규모있는 프로젝트를 구축하거나 많은 사람이 참여하는 프로젝트에서는 `Junit`을 활용해 애플리케이션을 테스트한다. 

# Junit 장점

```
- 테스트 준비시간을 단축할 수 있다.
- 한 번에 여러 테스트를 진행할 수 있다.
```

<br/>

# Save() Test

 그럼 이제, 앞서 구현했던 회원 `repository`를 테스트해보자. 테스트는 `Junit`으로 진행한다. 우선, `main` 디렉토리가 아닌 `test` 디렉토리에 `respository` 패키지를 생성하자. 그리고 `MemoryMemberRepositoryTest.java` 클래스를 생성하자.

![image](https://user-images.githubusercontent.com/49560745/104150231-91fc9880-541c-11eb-8e5d-4db77a4fcc2b.png)

```
파일명 : MemoryMemberRepositoryTest.java
위치 : \src\test\java\hello.hellospring.repository\MemoryMemberRepositoryTest.java
```

```java
package hello.hellospring.repository;

import hello.hellospring.domain.Member;
import hello.hellospring.respository.MemoryMemberRepository;
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.Test;

import java.util.Optional;

public class MemoryMemberRepositoryTest {

    MemoryMemberRepository memoryMemberRepository= new MemoryMemberRepository();

    @Test
    public void save(){
        Member member=new Member();
        member.setName("spring");

        memoryMemberRepository.save(member);

        Member result = memoryMemberRepository.findID(member.getId()).get();
        Assertions.assertThat(result).isEqualTo(result);
    }

}

```

- save() 기능을 테스트
- `MemoryMemberRepository`객체로 저장소 생성
- `Member` 객체를 생성해 저장할 회원 정보를 **setting**
- 저장했던 객체의 `id`와 실제로 `findID()` 메서드를 통해 찾아온 `id`가 일치하는지 확인 
- `Assertions(org.junit.jupiter.api)`을 활용해 두 값이 일치 확인 

테스트는 `15 line` 초록색 세모 아이콘을 클릭하자. 메서드 별로 실행 가능

![image](https://user-images.githubusercontent.com/49560745/104150683-02f08000-541e-11eb-8f01-b221ced6d448.png)

![image](https://user-images.githubusercontent.com/49560745/104150194-73969d00-541c-11eb-87a3-491aee0e93d2.png)

정상적으로 테스트가 완료되었음을 확인할 수 있다.

# FindByName() Test

이름으로 회원정보가 정상적으로 이루어지는 확인해보자. 아래 코드를 `MemoryMemberRepositoryTest.java`파일에 추가하자.

````java
    @Test
    public void findByName(){
        Member member1=new Member();
        member1.setName("spring1");
        memoryMemberRepository.save(member1);

        Member member2=new Member();
        member2.setName("spring2");
        memoryMemberRepository.save(member2);

        Member result=memoryMemberRepository.findName(member1.getName()).get();
        Assertions.assertThat(result).isEqualTo(member1);
    }
````

```
파일명 : MemoryMemberRepositoryTest.java
위치 : \src\test\java\hello.hellospring.repository\MemoryMemberRepositoryTest.java
```

```java
package hello.hellospring.repository;

import hello.hellospring.domain.Member;
import hello.hellospring.respository.MemoryMemberRepository;
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.Test;

import java.util.Optional;

public class MemoryMemberRepositoryTest {

    MemoryMemberRepository memoryMemberRepository= new MemoryMemberRepository();

    @Test
    public void save(){
        Member member=new Member();
        member.setName("spring");

        memoryMemberRepository.save(member);

        Member result = memoryMemberRepository.findID(member.getId()).get();
        Assertions.assertThat(result).isEqualTo(result);
    }

    @Test
    public void findByName(){
        Member member1=new Member();
        member1.setName("spring1");
        memoryMemberRepository.save(member1);

        Member member2=new Member();
        member2.setName("spring2");
        memoryMemberRepository.save(member2);

        Member result=memoryMemberRepository.findName(member1.getName()).get();
        Assertions.assertThat(result).isEqualTo(member1);
    }

}

```

- `member1`, `member2` 객체를 생성하고 각각 `spring1` , `spring2`로 이름 설정
- `repository`에 저장하고, 마찬가지로 `Assertions(org.junit.jupiter.api)`로 테스트 진행



<br/>

이 포스팅은 인프런 김영한님의 `스프링 입문 - 코드로 배우는 스프링 부트 강의`를 토대로 작성되었습니다.

# Reference

- [김영한님의 스프링-입문-스프링부트](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49577?tab=curriculum)

- [Accept - MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Accept)

  

