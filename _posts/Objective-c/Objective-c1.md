---
title: "12JAVA 배열"
permalink: /test/
<!-- excerpt: "객체지향 프로그래밍을 위한 [쓰레드]" -->
date: "2022-05-06 09:40:00 +0900"

toc: true
toc_sticky: true
categories:
  - Objective-c
---
내가 이해하기 위한 JAVA
# 배열 (Array)

```java
public class Main {
    public static void main(String[] args) throws Exception {
       int[] array1 = new int[5];
       int array2[] = new int[5];
       
       int[] array3 = {3, 2, 1};
       int[] array4 = new int[]{4, 5, 6};
       
        // 오류 : array1 = {0, 1, 2};  //이미 선언된 배열은 이렇게 초기화 X
        array2 = new int[]{2, 3, 4}; //이미 선언된 배열은 객체 생성하듯이 초기화 O
        
    }
}
```

출처
[http://www.tcpschool.com/java/java_array_oneDimensional](http://www.tcpschool.com/java/java_array_oneDimensional)
