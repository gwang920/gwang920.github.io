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

### Size

- `ArrayList` 의 크기는 `리스트명.size()` 메소드를 사용한다.

```java
ArrayList<Integer> ArrList=new ArrayList<Integer>();
ArrList.size();
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

### Size

- `List` 의 크기는 `리스트명.size()` 메소드를 사용한다.

```java
ArrayList<Integer> list = new ArrayList<Integer>();
list.size();
```



<br/>

## Array

### Sort

- `Array` 를 정렬하고자 할 때, `Arrays.sort(배열명)` 메소드를 사용한다.

```java
int [] Arr=new int[5];
Arrays.sort(Arr);
```

### length

- `Array` 의 길이는 `배열명.length` 를 사용한다.

```java
int [] Arr=new int[5];
Arr.length;
```



<br/>

## Set

### 값 넣기(add)

- `Set` 에 값을 넣을 때는, `set명.add(넣을 값)` 메소드를 사용한다.

```java
Set<String> set = new HashSet<String>();
set.add("combMenu");
```

### 값 삭제(remove)

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

### size

- `set` 의 크기는 `set명.size()` 메소드를 사용한다.

```java
Set<String> set= new HashSet<String>();
set.size();
```





<br/>

## Map

### 값 넣기(put)

- `Map`에 `{key : value}` 값을 설정할 때, `map명.put(key,value)` 메소드를 사용한다.

```java
Map<String,Integer> map=new HashMap<>();
map.put("str",1);
```

### 값 가져오기(get)

- `Map`의 `{key:value}`쌍의 value` 값을 가져올 때`,  `map명.get(key값)` 메소드를 사용한다.

```java
Map<String,Integer> map=new HashMap<>();
map.get("str");
```



### Key 값 존재 확인(containsKey)

- `Map` 에 해당하는 `key` 값이 존재하는지 확인할 때, `map명.containsKey(key값)` 메소드를 사용한다.
- `Key` 값이 존재하면 `true`, 존재하지 않으면 `false`를 반환한다.

```java
Map<String,Integer> map=new HashMap<>();
map.containsKey("str",1);
```

### size

- `Map`의 크기는 `map명.size()` 를 사용한다.

```java
Map<String,Integer> map=new HashMap<>();
map.size();
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

### 문자열 자르기(substring)

- `String` 문자열 일부를 추출할 때, `스트링명.substring()` 메소드를 사용한다.
- `스트링명.substring(idx)` : `idx`를 포함한 위치부터 문자열 끝까지 추출한다.
- `스트링명.substring(시작값,끝 값)` : `시작값` 부터 `끝 값 -1` 까지의 문자열을 추출한다.

```java
String str="1234567";
str.substring(3); // "4567"
str.substring(2,5) // "345"
```

### 문자열 뒤집기(Reverse)

- `String` 문자열을 뒤집기 할 때, `StringBuilder(문자열).reverse().toString()` 메소드를 사용한다.

```java
String str = "Reverse";
String str = new StringBuilder(words).reverse().toString();
System.out.println(str); 

[출력]
esreveR
```

### length

- `String` 의 길이는 `문자열명.length()` 를 사용한다.

```java
String str="123";
str.length();
```

<br/>

## StringBuilder

- `StringBuilder` 클래스로 문자열에 문자를 추가하거나, 삭제할 수 있다.

### 추가(append)

- **추가**할 때는, `빌더명.append(넣을문자)` 메소드를 사용한다.

```java
StringBuilder sb=new StringBuilder();

sb.append('a');
sb.append('b');
sb.append('c');

System.out.println(sb);

[출력]
abc
```



### 삭제(deleteChartAt)

- **삭제**할 때는, `빌더명.deletCharAt(삭제할문자의 인덱스)` 메소드를 사용한다.

```java
StringBuilder sb=new StringBuilder();

sb.append('a');
sb.append('b');
sb.append('c');

System.out.println(sb);

sb.deleteCharAt(1);

System.out.println(sb);

[출력]
abc
ac
```



<br/>

## 입/출력

### BufferdReader

- `BurredReader` 클래스는 `Enter`를 경계로 입력값을 인식한다.
- `readLine()` 메소드는  개행문자(`Enter`)를 포함해 `String` 형식으로 입력을 받아온다.
  - 따라서, `int`형으로 `readLine()` 을 받아오려면 `Integer.pareseInt()` 로 형변환이 필요하다.

```
[입력]
100
```

```java
import java.io.InputStreamReader;
import java.io.BufferedReader;
import java.io.IOException;
public class InputOuputTest {
    public static void main(String args[])throws IOException{
        BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
        int N=Integer.parseInt(br.readLine()); 
        System.out.prin(N);
    }
}

[출력]
100
```



### StringTokenizer

- `StringTokenizer` 클래스는 지정한 형식에 따라 문자열을 쪼개주는 클래스이다.
- `new StringTokenizer(문자열,기준)` 형식으로 `StringTokenizer` 객체를 생성할 수 있다.

```
[입력]
123 456
```

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class InputOuputTest {
    public static void main(String args[])throws IOException{
        BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st= new StringTokenizer(br.readLine());

        int N= Integer.parseInt(st.nextToken());
        int M= Integer.parseInt(st.nextToken());

        System.out.print(N+" "+M);
    }
}

[출력]
123 456
```



### 예시 

#### 1)

```
[입력]
3 3
111
222
333
```

```java
import java.util.*;
import java.io.*;

public class InputOuputTest {
    public static void main(String args[])throws IOException{
        BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st= new StringTokenizer(br.readLine());

        int N= Integer.parseInt(st.nextToken());
        int M= Integer.parseInt(st.nextToken());

        int [][]arr= new int[N][M];
        for(int i=0;i<N;i++){
            String str=br.readLine();
            for(int j=0;j<M;j++){
                arr[i][j]=Integer.parseInt(String.valueOf(str.charAt(j)));
            }
        }
        System.out.print(N+" "+M);
        for(int i=0;i<N;i++){
            for(int j=0;j<M;j++){
                System.out.print(arr[i][j]);
            }
            System.out.println();
        }
    }
}

    
[출력]
3 3
111
222
333
```

#### 2)

```
[입력]
5
1
2
3
4
5
```

```java
import java.util.*;
import java.io.*;

public class InputOuputTest {
    public static void main(String args[])throws IOException{
        BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
        int N=Integer.parseInt(br.readLine());
        for(int i=0;i<N;i++){
			int M=Integer.parseInt(br.readLine());
            System.out.println(M);
        }
    }
}

[출력]
1
2
3
4
5
```

