---
title: Spring boot기반 게시판 만들기[4] - 빌드하기
toc: true
categories:	
    - Spring boot
tags:
- Spring boot
- Spring Web
last_modified_at:
---



Spring boot기반 프로젝트를 빌드하는 방법에 대해 알아보자.

**Build란?**

```
컴퓨터 소프트웨어 분야에서 소프트웨어 빌드는 소스 코드 파일을 컴퓨터나 휴대폰에서 실행할 수 있는 독립 소프트웨어 가공물로 변환하는 과정을 말하거나 그에 대한 결과물을 일컫는다. 
출처 - 위키백과
```

Build란 소스 코드파일을 컴퓨터 혹은 휴대폰에서 실행할 수 있도록 독립적인 형태로 변환하는 과정이라고 할 수 있다. Spring boot에서 build를 하는 방법은 두 가지가 있다.

1) IDEA(IntelliJ)내에서 Build하기

2) cmd(혹은 Git bash)로 Build하기



두 방법 모두 실행하는 방법은 동일하다. 그 전에 환경 설정이 필요하다

bash를 실행할 수 있는 환경을 만들어주는 방법은

1) [IntelliJ & Gitbash 연동하기](https://gwang920.github.io/intellij/intellij&gitbash/)

2) [cmd - bash 환경설정](https://devms.tistory.com/58)

위 링크를 참고하자.



build하는 과정은 다음과 같다.

```
1) ./gradlew build
2) cd build/libs
3) java -jar hello-spring-0.0.1-SNAPSHOT.jar
4) 실행확인
```



![image](https://user-images.githubusercontent.com/49560745/103506005-10968a80-4e9f-11eb-92fe-c1ead0873b1d.png)

 command에서 프로젝트 폴더로 이동

![image](https://user-images.githubusercontent.com/49560745/103506221-8995e200-4e9f-11eb-9bf9-366a372d7b69.png)

기본 폴더구조는 위와 같다.

![image](https://user-images.githubusercontent.com/49560745/103506091-3c197500-4e9f-11eb-85c6-d5c111014727.png)

**./gradlew build** 입력

![image](https://user-images.githubusercontent.com/49560745/103506195-78e56c00-4e9f-11eb-89cb-f51aba82d958.png)

**./gradlew build**를 실행하고, ls를 입력하면 build 폴더에 **libs** 폴더가 생성되어있음을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/49560745/103508194-f7dca380-4ea3-11eb-86a0-6d4878469824.png)

마지막으로 **java -jar hello-spring-0.0.1-SNAPSHOT.jar** 명령어를 실행하고, 위와 같은 화면이 출력되면 성공이다!



```
Exception in thread "main" java.lang.UnsupportedClassVersionError: hello/hellospring/HelloSpringApplication has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0

        at java.lang.ClassLoader.defineClass1(Native Method)

        at java.lang.ClassLoader.defineClass(Unknown Source)

        at java.security.SecureClassLoader.defineClass(Unknown Source)

        at java.net.URLClassLoader.defineClass(Unknown Source)

        at java.net.URLClassLoader.access$100(Unknown Source)

        at java.net.URLClassLoader$1.run(Unknown Source)

        at java.net.URLClassLoader$1.run(Unknown Source)

        at java.security.AccessController.doPrivileged(Native Method)

        at java.net.URLClassLoader.findClass(Unknown Source)

        at java.lang.ClassLoader.loadClass(Unknown Source)

        at org.springframework.boot.loader.LaunchedURLClassLoader.loadClass(LaunchedURLClassLoader.java:151)

        at java.lang.ClassLoader.loadClass(Unknown Source)

        at java.lang.Class.forName0(Native Method)
        at java.lang.Class.forName(Unknown Source)
        at org.springframework.boot.loader.MainMethodRunner.run(MainMethodRunner.java:46)
        at org.springframework.boot.loader.Launcher.launch(Launcher.java:109)
        at org.springframework.boot.loader.Launcher.launch(Launcher.java:58)
        at org.springframework.boot.loader.JarLauncher.main(JarLauncher.java:88)
```





# Reference

- https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/48553?tab=curriculum&q=107977