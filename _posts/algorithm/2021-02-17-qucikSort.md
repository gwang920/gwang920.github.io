---
title: QuickSort(퀵소트) - JAVA
toc: true
categories:	
    - Algorithm non PS
tags:
- 알고리즘
- 퀵소트
Contest
last_modified_at: 
---

 **QuickSort**의 개념을 간단하게 알아보고, `java`로 구현해보자.

## 퀵 소트란?

- 불안정 정렬(Unstable Sort)
- 분할 정복 알고리즘 중 하나
- 매우 빠른 수행속도를 자랑하는 정렬 알고리즘

## 퀵 소트 정렬 과정

```
1) 임의의 피벗 값(기준 값)을 설정한다.

2) 리스트의 시작점 = 0(최초) , 도착점 = n-1(최초)을 설정한다. 
시작점, 도착점에서 출발하며,
피벗 값을 기준으로 
피벗보다 작은 원소는 '왼쪽'으로
큰 원소는 '오른쪽'으로 옮겨준다.
   
3) 시작점 > 도착점이 되면
새로운 시작점과 도착점을 설정한다.
그리고 파티션을 분할해 1) - 3)의 과정을 반복한다.

만약, [시작점 - 도착점] 사이의 리스트 원소가 한개인
파티션은 더 이상 반복하지 않는다.
```

## 시뮬레이션

`[7,4,2,8,3,5,1,6,10,9]` 리스트를 **QuickSort**로 정렬해보자.

- 피벗 값과 시작점, 끝점을 설정한다.

![quickSort](https://user-images.githubusercontent.com/49560745/108142269-cabd1b00-7108-11eb-81d6-4a67540ec251.png)

- 좌측에서는 `pivot`보다 큰 값을 우측에서는 `pivot` 보다 작은 값을 찾는다.

![quickSort](https://user-images.githubusercontent.com/49560745/108142358-f5a76f00-7108-11eb-83e2-4ff75c851abe.png)

- 각각 좌,우측에서 큰 값, 작은 값을 찾았으면, 두 값을 `SWAP` 해준다.

![quickSort](https://user-images.githubusercontent.com/49560745/108142468-2daeb200-7109-11eb-8ead-32fbb35770ff.png)

- `point`를 각각 좌, 우측으로 한 칸씩 이동하고, 지금까지 과정을 반복해준다.

![quickSort](https://user-images.githubusercontent.com/49560745/108142561-5d5dba00-7109-11eb-8433-d64e4bbf8960.png)

- 마찬가지로 `pivot` 보다 큰 값, 작은 값을 찾아준다.

![quickSort](https://user-images.githubusercontent.com/49560745/108142725-a9a8fa00-7109-11eb-8858-aa4dc4f301c0.png)

- 두 값을 다시 `SWAP` 해준다.

![quickSort](https://user-images.githubusercontent.com/49560745/108142762-c0e7e780-7109-11eb-9417-2dbc2c9f44bb.png)

- `SWAP` 이후에는 `point`를 각각 좌, 우측으로 한 칸씩 이동해준다. 이때, End > Start가 되어 해당 파티션의 `sort`를 멈춰준다.

![quickSort](https://user-images.githubusercontent.com/49560745/108142810-d5c47b00-7109-11eb-9f79-baee8d90abac.png)

- 이제, 새로운 start, end 값을 설정하고, 파티션에 대해 `sort`를 재귀적으로 반복한다. 이때, 파티션이 더이상 쪼개지지 않을 때까지 위 과정을 반복한다.

![quickSort](https://user-images.githubusercontent.com/49560745/108142929-10c6ae80-710a-11eb-8833-88e45821d01f.png)



<br/>

## 구현

```java
public class qucikSort {
    private static void quickSort(int[] arr,int start, int end) {
        int part=partition(arr,start,end);
        if(start<part-1) quickSort(arr,start,part-1);
        if(end>part) quickSort(arr,part,end);
    }

    private static int partition(int[] arr,int start,int end) {
        int pivot=arr[(start+end)/2];
        while(start<=end) {
            while(arr[start]<pivot) start++;
            while(arr[end]>pivot) end--;
            if(start<=end) {
                swap(arr,start,end);
                start++;
                end--;
            }
        }
        return start;
    }

    private static void swap(int[] arr,int start,int end) {
        int tmp=arr[start];
        arr[start]=arr[end];
        arr[end]=tmp;
        return;
    }


    public static void main(String[] args) {
        int[] arr= {0,3,4,1,9,5,8,6,7,2};
        quickSort(arr,0,arr.length-1);
        for(int i=0;i<arr.length;i++) {
            System.out.print(arr[i]+",");
        }
    }

}
```

<br/>

# Reference

- [퀵정렬에 대해 알아보고 자바로 구현하기 - Youtube](https://www.youtube.com/watch?v=7BDzle2n47c)