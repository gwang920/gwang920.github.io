---
title: Spring boot기반 Web Application 개발[12] - 의존성 주입(DI)
toc: true
categories:	
    - Spring boot
tags:
- Spring boot
- Spring Web
last_modified_at: 
---

  의존성 주입(DI)을 통해 **컨트롤러**, **서비스**, **레파지토리**의 의존관계를 설정해보자. 의존성 주입으로 컨트롤러가 서비스, 레파지토리를 사용할 수 있도록 하자.

# 의존성 주입(DI)

 이번 포스팅에서는 지금까지 구현해놓았던 **MemberService**, **MemberRepository**를 **MemberController**에서 사용할 수 있도록 의존성을 주입해보려한다.

### 의존성 주입(Dependency Injection)이란 ?

```
소프트웨어 엔지니어링에서 의존성 주입은 
하나의 객체가 다른 객체의 의존성을 제공하는 테크닉이다. 
"의존성"은 예를 들어 서비스로 사용할 수 있는 객체이다. 
클라이언트가 어떤 서비스를 사용할 것인지 지정하는 대신, 
클라이언트에게 무슨 서비스를 사용할 것인지를 말해주는 것이다.
```

[[출처] 의존성 주입 - 위키백과](https://ko.wikipedia.org/wiki/%EC%9D%98%EC%A1%B4%EC%84%B1_%EC%A3%BC%EC%9E%85)

의존성 주입은 쉽게 말해, 필요한 객체를 직접 생성하는 것이 아니라 외부에서 직접 설정하는 것이다. 즉, 외부로부터 필요한 객체를 받아서 사용한다. [이전 포스팅](https://gwang920.github.io/spring%20boot/springboot(11)-serviceTest/)에서 **생성자**를 통해 간단하게 의존성 주입 을 알아보았다. 

### 의존성 주입 장점

-  코드 재활용성이 높아진다
- 객체간의 결합도를 낮추고 코드를 유연하게 작성할 수 있다.

코드를 통해 의존성 주입을 알아보자.

## MemberController

**회원 컨트롤러**가 **회원서비스**와 **회원 리포지토리**를 사용할 수 있게 의존관계를 준비하자. `controller` 패키지에 `MemberController.java` 클래스를 생성하고, 아래 코드를 작성하자.

```
파일명 : MemberController.java
위치 :  main\java\hello.hellospring\controller\MemberController.java
```

```java
package hello.hellospring.controller;

import hello.hellospring.service.MemberService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;

@Controller
public class MemberController {

    private final MemberService memberService;

    @Autowired
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }
}
```

- `@Controller` 어노테이션은 해당 클래스가 controller 클래스라고 명시하는 것이다.
- `@Autowired` 어노테이션은 자동으로 의존관계를 만들어, memberservice와 연결시켜준다.
- 생성자에 `@Autowired` 어노테이션이 있으면 스프링이 연관된 객체를 스프링 컨테이너에서 찾아서 넣어준다.

이제, 

## MemberService

**MemberService** 에도 `@Service` 어노테이션, 생성자에는 `@Autowired`  어노테이션을 추가하자.

```
파일명 : MemberService.java
위치 : main\java\hello.hellospring\service\MemberService.java
```

```java
package hello.hellospring.service;

import hello.hellospring.domain.Member;
import hello.hellospring.respository.MemoryMemberRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.Optional;

@Service
public class MemberService {

    private final MemoryMemberRepository memberRepository;

    @Autowired
    public MemberService(MemoryMemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }


    /**
     * 중복 회원 관리
     */
    public Long join(Member member){
        validateDuplicateMember(member);
        memberRepository.save(member);
        return member.getId();
    }

    private void validateDuplicateMember(Member member) {
        memberRepository.findName(member.getName())
                .ifPresent(m->{
                    throw new IllegalStateException("이미 존재하는 회원입니다.");
                });
    }

    /**
     * 회원 전체 조회
     */
    public List<Member> findMembers(){
        return memberRepository.findAll();
    }

    /**
     * 회원 아디로 조회
     */
    public Optional<Member> findOne(Long memeberId){
        return memberRepository.findID(memeberId);
    }

}

```

## MemoryMemberRepository

**MemoryMemberRepository** 에도 `@Repository`어노테이션, 생성자에는 `@Autowired`  어노테이션을 추가하자.

```
파일명 : MemoryMemberRepository.java
위치 : main\java\hello.hellospring\repository\MemoryMemberRepository.java
```

```java
package hello.hellospring.respository;

import hello.hellospring.domain.Member;
import org.springframework.stereotype.Repository;

import java.util.*;

@Repository
public class MemoryMemberRepository implements MemberRepository{
    private static Map<Long,Member> store= new HashMap<>();
    private static long sequence =0L;

    @Override
    public Member save(Member member) {
        member.setId(++sequence);
        store.put(member.getId(),member);
        return member;
    }

    @Override
    public Optional<Member> findID(long id) {
        return Optional.ofNullable(store.get(id));
    }

    /**
     Map을 순회하기 위해, iterator() 대신에 stream()을 사용하고,
     filter()로 조건에 맞는지 판단한다.
     findAny()는 비어 있는 스트림에서는 비어있는 Optional 객체를 반환한다.

     * iterator()
     컬렉션에 저장되어 있는 요소들을 읽어오는 방법 중의 하나
     **/
    @Override
    public Optional<Member> findName(String Name) {
        return store.values().stream()
                .filter(member -> member.getName().equals(Name))
                .findAny();
    }

    @Override
    public List<Member> findAll() {
        return new ArrayList<>(store.values());
    }

    public void clearStore(){
        store.clear();
    }
}

```





<br/>

이 포스팅은 인프런 김영한님의 `스프링 입문 - 코드로 배우는 스프링 부트 강의`를 토대로 작성되었습니다.

# Reference

- [김영한님의 스프링-입문-스프링부트](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49577?tab=curriculum)

