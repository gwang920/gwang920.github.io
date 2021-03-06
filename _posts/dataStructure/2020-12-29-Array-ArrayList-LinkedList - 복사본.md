---
title: Array vs ArrayList vs LinkedList
toc: true
categories:	
    - DataStructure
tags:
- 자료구조
- Array
- ArrayList
- LinkedList
last_modified_at: 
---



자료구조를 공부할 때, **Array와 ArrayList**의 혹은 **ArrayList 와 LinkedList**의 차이를 비교하는 글이 많았다. 그런데 항상 위 3개 자료구조의 쓰임새가 명확하게 와닿지 않았고, 때로는 헷갈리기도 했다. 그래서 한 번에 비교하며, 정리해보려 한다.



## 1) Array

![image](https://user-images.githubusercontent.com/49560745/103251594-a3758780-49bc-11eb-9b5e-365288cd3c6a.png)

Array는 우리가 흔히 알고 있는 배열이라 할 수 있다. 가장 기본적인 자료구조이며, 순차자료구조라고 할 수 있다. **논리적인 저장순서**와 **물리적인 저장순서**가 **일치**한다는 특징을 가지고 있다. 따라서, 인덱스로 해당 원소에 접근 할 수 있다. 그렇기 때문에 찾고자 하는 원소의 인덱스 값을 알고 있다면 **Big-O(1)**에(참조시간이 상수) 해당 원소로 접근할 수 있다. 즉 **Random Access**가 가능하다.

하지만, **삽입** 또는 **삭제** 과정에서는 해당원소에 접근하여 작업을 완료한 뒤(Big-O(1)) 또 한가지의 작업이 필요하다. 만약 배열의 어떤 요소에 삽입 또는 삭제를 했다면 배열의 연속적인 특징이 깨진다. 따라서 삽입 또는 삭제한 원소보다 큰 인덱스를 갖는 원소들을 shift해줘야하는 비용이 발생하고, 이 경우 시간복잡도는(O(N))이 된다. 따라서 Array 자료구조의 시간복잡도의 **worst case**는 **O(N)**이 된다.

처음에는 **정적인 자료구조**인 Array에 데이터를 삽입하고, 삭제한다는 개념이 와닿지 않았다. 실제로 코딩을 해보면 데이터의 삽입, 삭제가 이루어지는 Vector나 Queue와는 다르지않나? 라는 생각이 들기도 했다. 사실, Array에서 삽입 삭제는 데이터의 교환이라고 할 수 있다. 인덱스를 유지하면서(정적) 값을 추가하고, 삭제해야하기 때문이다. 

시간복잡도

```
1) 원소 찾기 : O(1)
2) 원소 추가/삭제 : O(N)
4) List의 크기 구하기 : O(N)
```



## 정리

1. Array는 논리적인 저장순서와 물리적인 저장순서가 일치한다.

2. 데이터에 접근하는 서치 시간복잡도는 O(1)이다.

3. 삽입,삭제는 데이터의 교환과도 같다. 시간복잡도는 shift 비용으로 worst case는 O(N)이 된다.



## 2) ArrayList

Array와 ArrayList의 가장 결정적인 차이는 사이즈가 동적이냐 정적이냐이다. ArrayList는 사이즈가 **동적인 배열**이다. 이외에는 Array와 동일하다고 할 수 있다. 그렇다면 ArrayList에 element **삽입**은 어떻게 이루어질까?

ArrayList는 기존 크기를 초과하지 않는다면, 가장 마지막 노드에 element가 삽입된다. 반대로, ArrayList가 기존의 크기를 초과한다면 **기존의 크기 + 기존의 크기/2** 만큼 늘어난 배열에 기존 elements를 copy한다. 

예를들어,

```
size=4 인 ArrayList에 
	[1][2][3][4]
element 5를 추가한다면
	[1][2][3][4][5][] 로 배열이 현재배열크기/2 만큼 늘어난 배열에 기존 element가 copy된다.
```

ArrayList는 빈 엘리먼트를 허용하지 않기 떄문에 element의 **삭제**가 일어나면 빈 공간을 메꾸기 위해 뒤 원소들을 앞으로 당겨오는 작업이 이루어진다. 이 때문에 시간복잡도는 최악의 경우 O(N)이 발생하게 된다.

이러한 ArrayList의 특성에 따라 **시간복잡도**를 정리할 수 있다. ArrayList의 특징을 잘 생각해보며, 아래의 시간복잡도를 계산해보면 좋을 것 같다.

시간복잡도

```
1) 원소 찾기 : O(1)
2) 마지막 노드에 원소 추가/삭제 : O(1) or O(N)
3) 마지막 노드 이외의 위치에 원소 추가/삭제하기 : O(N)
4) List의 크기 구하기 : O(N)
```



## 정리

1. ArrayList는 사이즈가 동적인 Array다.

2. ArrayList 삽입 시 기존의 크기를 초과하면 **기존의 크기 + 기존의 크기/2**의 배열에 원소들이 복사된다. 대량의 원소를 추가/삭제 하는 경우에는 그만큼의 복사가 일어나 성능 저하를 일으킬 수 있다. 



## 3) LinkedList

![image](https://user-images.githubusercontent.com/49560745/103252274-74ace080-49bf-11eb-9279-d9115869c4d0.png)

Array의 문제점을 해결하기 위한 자료구조가 **Linked List**이다. Linked List의 각각 원소들은 자기 자신다음에 어떠 원소인지만을 기억한다. 따라서 이 부분만 다른 값으로 바꿔주면 삭제와 삽입을(O(1))만에 해결 할 수 있다.

하지만 Linked List 역시 한가지 문제가 있다. 원하는 위치에 삽입을 하고자하면 원하는 위치를 Search하는 과정에서 첫번째 원소부터 다 확인해봐야한다는 것이다. Array와 달리 **논리적 저장순서**와 **물리적 저장순서**가 **다르기** 때문이다. 이것은 일단 삽입하고 정렬하는것과 마찬가지다. 이 과정 때문에 어떠한 원소를 삭제 또는 추가하고자 했을 때 그 원소를 찾기 위해 O(n)의 시간이 추가적으로 발생한다.

결국 Linked List 자료구조는 search에도 O(N)의 시간복잡도를 갖고 삭제에 대해서도 O(n)의 시간복잡도를 갖는다. Linked List는 Tree 구조의 근간이 되는 자료구조이며 Tree에서 사용되었을 때 그유용성이 드러난다.

시간복잡도

```
1) 임의의 위치 원소 찾기 : O(N)
2) 마지막 노드에 원소 추가/삭제 : O(1)
3) 마지막 노드 이외의 위치에 원소 추가/삭제하기 : O(1)
4) List의 크기 구하기 : O(1) or O(N)
```



## 정리

1. LinkedList는 데이터 정렬로인해 삽입,삭제 시간복잡도는 결국 O(N)이다.

2. 논리적 저장순서와 물리적 저장순서가 다르다.

# Reference

-  https://zorba91.tistory.com/287
- http://www.nextree.co.kr/p6506/
- https://manducku.tistory.com/33

