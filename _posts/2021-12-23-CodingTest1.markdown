---
title: "백준 코딩 테스트 1"
permalink: /2021-12-23-CodingTest1
excerpt: "BAEKJOON 코딩 테스트 1"
date: "2021-12-23 16:50:00 +0900"
last_modified_at: 2021-12-23T16:05:18
toc: true
toc_sticky: true
categories:
  - Coding Test
---

### 9498번<br/>
문제<br/>
시험 점수를 입력받아 90 ~ 100점은 A, 80 ~ 89점은 B, 70 ~ 79점은 C, 60 ~ 69점은 D, 나머지 점수는 F를 출력하는 프로그램을 작성하시오.<br/>

입력<br/>
첫째 줄에 시험 점수가 주어진다. 시험 점수는 0보다 크거나 같고, 100보다 작거나 같은 정수이다.<br/>

출력<br/>
시험 성적을 출력한다.<br/>

```java
import java.util.Scanner;

public class Main {
	public static void main(String[] args){
		Scanner sc = new Scanner(System.in);
		int multi = sc.nextInt();

		for(int i=1; i<=9; i++){
			System.out.println(multi + " * " + i + " = " + (multi*i));
		}
	}
}
```

### 2753번<br/>

문제<br/>
연도가 주어졌을 때, 윤년이면 1, 아니면 0을 출력하는 프로그램을 작성하시오.<br/>
윤년은 연도가 4의 배수이면서, 100의 배수가 아닐 때 또는 400의 배수일 때이다.<br/>
예를 들어, 2012년은 4의 배수이면서 100의 배수가 아니라서 윤년이다. 1900년은 100의 배수이고 400의 배수는 아니기 때문에 윤년이 아니다. 하지만, 2000년은 400의 배수이기 때문에 윤년이다.<br/>

입력<br/>
첫째 줄에 연도가 주어진다. 연도는 1보다 크거나 같고, 4000보다 작거나 같은 자연수이다.<br/>

출력<br/>
첫째 줄에 윤년이면 1, 아니면 0을 출력한다.

```java
import java.util.Scanner;

public class Main {
	public static void main(String[] args){
	    System.out.println("1에서 4000까지의 년도를 입력해주세요.");
	    System.out.println("윤년은 1을 윤년이 아니면 0을 출력합니다.");
		Scanner sc = new Scanner(System.in);
		int year = sc.nextInt();

        if(year >= 1 && year <= 4000){
    		if((year % 4 == 0 && year % 100 != 0) || year % 400 == 0){
    		    System.out.println("1");
    		}else{
    		    System.out.println("0");
    		}
        }else {
            System.out.println("정상적인 연 수가 아닙니다.");
        }
	}
}
```