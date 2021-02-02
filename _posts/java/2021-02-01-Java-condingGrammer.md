---
title: Java - 자바 코딩테스트 문법 정리
toc: true
categories:	
    - Java
tags: 
- Java
- 문법
last_modified_at:
---

   코딩테스트에서 자주 사용되는 `Java` 문법 정리, `Daily Update`

## ArrayList

### 깊은 복사

- `ArrayList`를 깊은 복사하고 싶다면, `복사되는배열.addAll(복사할배열)` 메서드를 사용하면된다.

- `ArrayList` **w**를 `ArrayList` **copy_w**에 깊은복사

```java
ArrayList<Integer> w=new ArrayList<Integer>();
ArrayList<Integer> copy_w=new ArrayList<Integer>();
copy_w.addAll(w);
```

### Sort

- `ArrayList` 를 정렬하고 할 때, `리스트명.sort()` 메소드를 사용한다.

```java
ArrayList<Integer> ArrList=new ArrayList<Integer>();
ArrList.sort(null);
```



<br/>

## List

### set => List 변경

- 생성자에 값을 넣어주면,  `set -> List`로 변경할 수 있다.

```java
Set<String> set = new HashSet<String>();
List<String> menuList = new ArrayList<>(set);
```



### Sort

- `List` 를 정렬하고자 할 때, `Collections.sort(리스트명)` 메소드를 사용한다.

```java
List<Stirng> list = new ArrayList<>();
Collections.sort(menuList);
```



### Add

- `List` 에 값을 넣을 때, `리스트명.add(넣을 값)` 메소드를 사용한다.

```java
ArrayList<Integer> list = new ArrayList<Integer>();
list.add(1);
```

### remove

- `List` 의 값을 삭제할 떄, `리스트명.remove()` 메소드를 사용한다.
- `리스트명.remove(삭제할 값의 index)`

```java
ArrayList<Integer> list = new ArrayList<Integer>();
list.remove(list.size()-1); // list의 마지막 값이 리스트에서 제거된다.
```

<br/>

## Array

### Sort

- `Array` 를 정렬하고자 할 때, `Arrays.sort(배열명)` 메소드를 사용한다.

```java
int [] Arr=new int[5];
Arrays.sort(Arr);
```

<br/>

## Set

### 값 넣기(Add)

- `Set` 에 값을 넣을 때는, `set명.add(넣을 값)` 메소드를 사용한다.

```java
Set<String> set = new HashSet<String>();
set.add("combMenu");
```

### 값 삭제(Remove)

- `Set` 에서 값을 삭제할 때는, `set명.remove(삭제할 값)` 메소드를 사용한다.

```java
Set<String> set = new HashSet<String>();
set.remove("combMenu");
```



### Iterator

- `set` 의 값을 조회할 떄, `set명.iterator()`를 사용해 반복자를 생성한다.
- `반복자.hasNext()` 메소드로 다음 값이 존재하는지 확인한다.
- `반복자.next()` 메소드로 참조값을 가져온다.

```java
Set<String> set= new HashSet<String>();

set.add(1);
set.add(2);
set.add(3);

Iterator<String> it= set.iterator();
while(it.hasNext()){
	String a= it.next();
	System.out.println(a);
}

[결과]
1
2
3
```

<br/>

## Map

### 값 넣기(Put)

- `Map`에 `{key : value}` 값을 설정할 때, `map명.put(key,value)` 메소드를 사용한다.

```java
static Map<String,Integer> map=new HashMap<>();
map.put("str",1);
```

### 값 가져오기(Get)

- `Map`의 `{key:value}`쌍의 value` 값을 가져올 때`,  `map명.get(key값)` 메소드를 사용한다.

```java
static Map<String,Integer> map=new HashMap<>();
map.get("str");
```



### Key 값 존재 확인(ContainsKey)

- `Map` 에 해당하는 `key` 값이 존재하는지 확인할 때, `map명.containsKey(key값)` 메소드를 사용한다.
- `Key` 값이 존재하면 `true`, 존재하지 않으면 `false`를 반환한다.

```java
static Map<String,Integer> map=new HashMap<>();
map.containsKey("str",1);
```

<br/>

## String

### String to Array

- `String` 문자열을 `Array`로 만들 때, `스트링명.split()` 메소드를 사용한다.

```java
String str = "12345";
String[] Arr = str.split("");
//[1,2,3,4,5]
```

### 문자열 자르기(SubString)

- `String` 문자열 일부를 추출할 때, `스트링명.substring()` 메소드를 사용한다.
- `스트링명.substring(idx)` : `idx`를 포함한 위치부터 문자열 끝까지 추출한다.
- `스트링명.substring(시작값,끝 값)` : `시작값` 부터 `끝 값 -1` 까지의 문자열을 추출한다.

```java
String str="1234567";
str.substring(3); // "4567"
str.substring(2,5) // "345"
```



<br/>

