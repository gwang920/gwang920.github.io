---
title: Java - class변수와 Instance 변수
toc: true
categories:	
    - Java
tags: 
- Java
- class
- instance
last_modified_at:
---



# Class변수와 Instance 변수

JAVA에는 `Class` 변수와 `Instance` 변수가 존재한다.

## 클래스와 인스턴스

```
클래스 - '설계도'
인스턴스 - 설계도에 따라 만들어진 '제품'
```

`Class`는 객체를 만들기 위한 **설계도**라고 할 수 있다. 그리고 `Instance`는 설계도에 따라 만들어진 **제품**이다. 



## 메소드화

### 메소드화 특징/장점

```
- 함수는 하나의 기능을 갖도록 만들어야한다.
- 중복이 줄어든다.
- 재사용성을 높일 수 있다.
- 유지보수성을 개선할 수 있다.
```

#### 1) Caculator1

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

#### 2) Caculator2

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

### 예제 2

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
        
        // 위 아래 코드가 반복된다.
	}
	
	public void sum(int a,int b){
		System.out.println(a+b);
	}
}
```

#### 2) Calculator2

Calculator1의 중복코드를 제거하고, 계산기라는 객체를 만들어보자

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

- 
