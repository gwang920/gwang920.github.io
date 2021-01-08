---
title: Java - class와 Instance
toc: true
categories:	
    - Java
tags: 
- Java
- class
- instance
last_modified_at:
---



# Class와 Instance, Object

```
객체 - 소프트웨어 세계에서 '구현할 대상'
클래스 - '설계도'
인스턴스 - 설계도에 따라 만들어진 '제품'
```

`Class`는 객체를 만들기 위한 **설계도**라고 할 수 있다. `Object`는 소프트웨어 세계에서 **구현해야 할 대상**이다. 그리고 `Instance`는 설계도에 따라 만들어진 **제품**이라고 할 수 있다. 

`Class`와 `Instance`, `Object` 를 설명할 떄, 붕어빵에 비유하곤 한다. 추상적인 붕어빵 자체는 **객체이고**,  틀은 붕어빵을 제품으로 만들기 위한 **설계도**이며, 붕어빵은 만들어진 구체적인 실체, 즉 **제품**인셈이다.

Java 프로그래밍 관점에서보자면, 

- **객체**는 구현해야 할 요구사항
- **클래스**는 객체를 구현하기 위한 설계도
- **인스턴스**는 클래스 생성자를 통해 생성되어, 실제 메모리 공간에 존재하는 객체이다.

<br/>

- [참고] Class 변수와 Instance 변수, local 변수

```java
public class variable{
	int instanceVariable; // Instance 변수
	static int classVariable; // Class 변수
    
    void method(){
        int localVariable; // local 변수
    }
}
```

|     변수 종류      |                    선언 위치                    |       생성시기(메모리 할당)       |     소멸시기(메모리 해제)      |
| :----------------: | :---------------------------------------------: | :-------------------------------: | :----------------------------: |
| Class 변수(static) |                   클래스 영역                   |   클래스가 메모리에 올라 갈 때    |        프로그램 종료 시        |
|   Instance 변수    |                   클래스 영역                   |     인스턴스가 생성되었을 때      |     해당 인스턴스 소멸 시      |
|     local 변수     | 클래스 이외의 영역(생성자, 메서드, 초기화 블럭) | 메서드, 생성자 등이 수행되었을 때 | 메서드, 생성자 등 수행 종료 후 |



<br/> 이제, 예제를 통해 `Class`와 `Instance`에 대해 알아보자.

이번 예제에서 구현해야할 대상인 객체는 계산기다. 객체지향 프로그래밍에서 `class`를 만드는 이유는 `class`들 간의 관계를 효율적으로 설계하여, 현실의 요구사항을 해결하기 위함이라고 생각한다. 부수적으로는 코드의 중복을 줄이고, 코드의 유지보수성을 높이는 것에 있다. 그리고 이는 `메소드화`부터 시작된다. `메소드화`의 특/장점을 단계적으로 살펴보며, 학습해보자.

<br/>

## 메소드화

### 메소드화 특징/장점

```
- 함수는 하나의 기능을 갖도록 만들어야한다.
- 중복이 줄어든다.
- 재사용성을 높일 수 있다.
- 유지보수성을 개선할 수 있다.
```

#### 1) Caculator1

 덧셈을  출력하는 코드이다. 동일한 출력문이 중복되고 있다. 단순한, `println()`문을 넘어 몇십 혹은 몇백줄짜리의 코드가 중복된다면, 프로그램을 설계하고, 관리하기 쉽지 않을 것이다.

```java
public class Caculator1{
	public static void main(String[] args){
		System.out.println(10+20);
		System.out.println(20+30);
			.
			.
			.
		System.out.println(2000+2010);
	}
}
```

<br/>

#### 2) Caculator2

Calculator1을 메소드화 시킨 코드이다. 단순히 sum() 이라는 간단한 메소드이지만 만약 sum() 이라는 메소드안에 수십, 수백줄의 코드가 있다고 생각해보자. 이를 메소드화 함으로써 코드를 간결하고, 효율적으로 설계할 수 있다.

```java
public class Caculator2{
	public static void main(String[] args){
		sum(10,20);
        sum(20,30);
	}
	
	public void sum(int a,int b){
		System.out.println(a+b);
	}
}
```

<br/>

## 중복제거

#### 1) Caculator1

```java
public class Caculator1{
	public static void main(String[] args){
		int a=10;
		int b=20;
		sum(a,b);
		
		a=20;
		b=30;
        sum(20,30);
        
        // 코드가 반복된다.
	}
	
	public void sum(int a,int b){
		System.out.println(a+b);
	}
}
```

#### 2) Calculator2

Calculator1의 중복코드를 제거하고, 계산기라는 객체를 만들어보자.

```java
class Calculator2{
    int left, right;
      
    // 인스턴스의 변수 값 설정
    public void setOprands(int left, int right){
        this.left = left;
        this.right = right;
    }
      
    public void sum(){
        System.out.println(this.left+this.right);
    }
      
    public void avg(){
        System.out.println((this.left+this.right)/2);
    }
}
  
public class CalculatorDemo {
      
    public static void main(String[] args) {
          
        Calculator c1 = new Calculator();
        c1.setOprands(10, 20);
        c1.sum();       
        c1.avg();       
          
        Calculator c2 = new Calculator();
        c2.setOprands(20, 40);
        c2.sum();       
        c2.avg();
    }
  
}
```

## 인스턴스

```
cacluclator : 설계도
c1 : 계산기 1
c2 : 계산기 2

여기서 c1,c2가 인스턴스이다.
즉, 클래스를 통해 만들어진 구체적인 제품이 인스턴스인 것이다.

객체를 만드는 것, 클래스를 만드는 것
=> 사용자 정의 데이터 타입을 만드는 것
```



# Reference

- [Class vs Object vs Isatnce [영문]](https://alfredjava.wordpress.com/2008/07/08/class-vs-object-vs-instance/)


- [IT 마이닝 - 자바의 변수](https://itmining.tistory.com/20)
- [생활코딩 - 클래스와 인스턴스 그리고 객체](https://www.opentutorials.org/course/1223/5400)