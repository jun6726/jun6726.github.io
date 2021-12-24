---
title: "백준 코딩 테스트 2"
permalink: /2021-12-24-CodingTest2
excerpt: "BAEKJOON 코딩 테스트 2"
date: "2021-12-24 10:50:00 +0900"
last_modified_at: 2021-12-24T16:05:18
toc: true
toc_sticky: true
categories:
  - Coding Test
---

### 10950번

A+B - 3<br/>

문제<br/>
두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.<br/>

입력<br/>
첫째 줄에 테스트 케이스의 개수 T가 주어진다.<br/>
각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 A와 B가 주어진다. (0 < A, B < 10)<br/>

출력<br/>
각 테스트 케이스마다 A+B를 출력한다.

```java
import java.util.Scanner;

public class Main {
	public static void main(String[] args){
	  Scanner sc = new Scanner(System.in);
	  int T = sc.nextInt();

    	  for(int i=0; i < T; i++){
    	      int A = sc.nextInt();
    	      int B = sc.nextInt();
	            if(A > 0 && B < 10){
	                System.out.println(A+B);
	            }
    	      }
	    
	}
}
```
### 8393번

문제<br/>
n이 주어졌을 때, 1부터 n까지 합을 구하는 프로그램을 작성하시오.<br/>

입력<br/>
첫째 줄에 n (1 ≤ n ≤ 10,000)이 주어진다.<br/>

출력<br/>
1부터 n까지 합을 출력한다.<br/>

```java
import java.util.Scanner;

public class Main {
	public static void main(String[] args){
	    Scanner sc = new Scanner(System.in);
	    int n = sc.nextInt();
	    int sum = 0;
	    
	    if(n >= 1 && n <= 10000){
	        for(int i=1; i<=n; i++){
	            sum += i;
	        }
	    }
	    System.out.println(sum);
	}
}
```

### 2741번

문제<br/>
자연수 N이 주어졌을 때, 1부터 N까지 한 줄에 하나씩 출력하는 프로그램을 작성하시오.<br/>

입력<br/>
첫째 줄에 100,000보다 작거나 같은 자연수 N이 주어진다.<br/>

출력<br/>
첫째 줄부터 N번째 줄 까지 차례대로 출력한다.

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        
        if(N > 0 && N <= 100000) {
            for(int i=1; i<=N; i++){
                System.out.println(i);
            }
        }
        
    }
}
```

### 11021번

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
            for(int i=1; i<=T; i++){
                int A = sc.nextInt();
                int B = sc.nextInt();
                        
                if(A > 0 && B < 10) {
                    System.out.println("Case #" + i + ": " + (A+B));
            }
        }
        
    }
}
```

### 11022번

문제<br/>
두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.<br/>

입력<br/>
첫째 줄에 테스트 케이스의 개수 T가 주어진다.<br/>
각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 A와 B가 주어진다. (0 < A, B < 10)<br/>

출력<br/>
각 테스트 케이스마다 "Case #x: A + B = C" 형식으로 출력한다. x는 테스트 케이스 번호이고 1부터 시작하며, C는 A+B이다.<br/>

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
            for(int i=1; i<=T; i++){
                int A = sc.nextInt();
                int B = sc.nextInt();
                        
                if(A > 0 && B < 10) {
                    System.out.println("Case #" + i + ": " + A + " + " + B + " = " + (A+B));
            }
        }
        
    }
}
```

### 2438번
문제<br/>
첫째 줄에는 별 1개, 둘째 줄에는 별 2개, N번째 줄에는 별 N개를 찍는 문제<br/>

입력<br/>
첫째 줄에 N(1 ≤ N ≤ 100)이 주어진다.<br/>

출력<br/>
첫째 줄부터 N번째 줄까지 차례대로 별을 출력한다.<br/>

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        sc.close();
        
        if(N>=1 && N<=100){
            for(int i=1; i<=N; i++){
                for(int j=1; j<=i; j++){
                    System.out.print("*");
                }
                System.out.println();
            }
        }
    }
}
```

### 2439번

문제 <br/>
첫째 줄에는 별 1개, 둘째 줄에는 별 2개, N번째 줄에는 별 N개를 찍는 문제<br/>
하지만, 오른쪽을 기준으로 정렬한 별(예제 참고)을 출력하시오.<br/>

입력<br/>
첫째 줄에 N(1 ≤ N ≤ 100)이 주어진다.<br/>

출력<br/>
첫째 줄부터 N번째 줄까지 차례대로 별을 출력한다.<br/>

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        sc.close();
        
        if(N>=1 && N<=100){
            for(int i=1; i<=N; i++){
                for(int j=1; j<=N; j++){
                    if(j<=N-i){
                        System.out.print(" "); 
                    }else if(j>N-i){
                        System.out.print("*");
                    }
                }
                System.out.println("");
            }
        }
    }
}
```

### 10871번

문제<br/>
정수 N개로 이루어진 수열 A와 정수 X가 주어진다. 이때, A에서 X보다 작은 수를 모두 출력하는 프로그램을 작성하시오.<br/>

입력<br/>
첫째 줄에 N과 X가 주어진다. (1 ≤ N, X ≤ 10,000)<br/>
둘째 줄에 수열 A를 이루는 정수 N개가 주어진다. 주어지는 정수는 모두 1보다 크거나 같고, 10,000보다 작거나 같은 정수이다.<br/>

출력<br/>
X보다 작은 수를 입력받은 순서대로 공백으로 구분해 출력한다. X보다 작은 수는 적어도 하나 존재한다.<br/>

```java

```

###10952번

문제<br/>
두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.<br/>

입력<br/>
입력은 여러 개의 테스트 케이스로 이루어져 있다.<br/>
각 테스트 케이스는 한 줄로 이루어져 있으며, 각 줄에 A와 B가 주어진다. (0 < A, B < 10)<br/>
입력의 마지막에는 0 두 개가 들어온다.<br/>

출력<br/>
각 테스트 케이스마다 A+B를 출력한다.<br/>

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int A = 1;
        int B = 1;
        
        while(A > 0 && B < 10){
            A = sc.nextInt();
            B = sc.nextInt();
            if(A == 0 && B == 0){
                return;
            }
            System.out.println(A+B);
        }
    }
}
```

### 10871번

문제<br>
정수 N개로 이루어진 수열 A와 정수 X가 주어진다. 이때, A에서 X보다 작은 수를 모두 출력하는 프로그램을 작성하시오.<br>

입력<br>
첫째 줄에 N과 X가 주어진다. (1 ≤ N, X ≤ 10,000)<br>
둘째 줄에 수열 A를 이루는 정수 N개가 주어진다. 주어지는 정수는 모두 1보다 크거나 같고, 10,000보다 작거나 같은 정수이다.<br>

출력<br>
X보다 작은 수를 입력받은 순서대로 공백으로 구분해 출력한다. X보다 작은 수는 적어도 하나 존재한다.<br>

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args){
        Scanner  sc = new Scanner(System.in);
        int N = sc.nextInt();
        int X = sc.nextInt();
        
        for(int i=0; i<N; i++){
            int A = sc.nextInt();
            if(A < X){
                System.out.println(A);
            }
        }
    }
}
```