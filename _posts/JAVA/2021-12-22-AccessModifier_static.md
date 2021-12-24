---
title: "JAVA 객체지향 6"
permalink: /AccessModifier_static/
excerpt: "객체지향 프로그래밍을 위한 [접근제어자와 정적변수]"
date: "2021-12-22 10:30:00 +0900"
last_modified_at: 2022-12-22T13:27:18-16:50
toc: true
toc_sticky: true
categories:
  - OOP
  - JAVA
---
내가 이해하기 위한 JAVA 객체지향 6
# 접근제어자 (Access Modifier)

접근제어자란? 변수/메소드의 사용 범위를 지정하는 명령어

1. private
2. defalut(생략)
3. protected
4. public

아래로 내려올수록 사용 범위가 넓다.

|접근제어자|사용범위|특징|
|:------:|:---:|---|
|private|선언된 클래스에서만 사용 가능||
|defalut|동일한 패키지에서 사용 가능|생략 가능|
|protected|동일 패키지의 클래스/다른 패키지의 상속받은 클래스||
|public|모든 클래스 사용 가능||

protected
*house/HousePark.java*
```java
package house;

public class HousePark {
    protected String lastname = "park";
}
```
*house/person/EungYongPark.java*
```java
package house.person;

import house.HousePark;

public class EungYongPark extends HousePark {
    public static void main(String[] args) {
        EungYongPark eyp = new EungYongPark();
        System.out.println(eyp.lastname);
    }
}
```

> HousePark클래스를 상속받은 EungYongPark 클래스의 패키지는 house.person으로 HousePark의 패키지인 house와 다르지만 HousePark의 lastname 변수가 protected로 설정되었기 때문에 eyp.lastname과 같은 접근이 가능하다. 만약 lastname의 접근제어자가 protected 가 아닌 default 접근제어자였다면 eyp.lastname 문장은 컴파일 에러를 낼 것이다.

# 정적(static) 변수와 메소드

### 정적 변수
static 고정된 값으로 공유가 가능하다. (공유하기 때문에 특정 부분에서 변화를 주면 다른 부분에서도 같이 변경된다) <br/>
+final 명령어는 static 앞에 선언하는 명령어로 변수를 고정하는 기능을 하며, 변경이 절대 불가능하다.(오류 발생)
final static String lastname = "최";


```java
public class Counter {
	static int count = 0;
	Counter() {
		this.count++;
		System.out.println(this.count);
	}
	
	public static void main(String[] args) {
		Counter c1 = new Counter();
		Counter c2 = new Counter();
	}
	
	// 결과 : 1
	//	2
}
```

> static이 없이 했다면 c1과 c2의 count는 각각 다른 값을 가지기 때문에 1, 1이 출력될 것을 static으로 정적 변수로 바꿔 c2를 출력할때 2가 출력된다.

### 정적 메소드

```java
public class Counter  {
    static int count = 0;
    Counter() {
        this.count++;
    }

    public static int getCount() {
        return count;
    }

    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();

        System.out.println(Counter.getCount());
    }
}
```
> static 메소드 getCount()로 객체 생성없이 Counter.getCount를 실행했다.
> static 메소드 안에서는 객체변수에 접근하지 못한다. 위의 예제에서는 count도 static 변수이기 때문에 접근이 가능하다.

### 싱글톤 패턴 (Singleton pattern)
클래스로 생성하는 객체가 단 하나(single)인 디자인 패턴이다.

*Sample.java*

```java
class Singleton {
    private Singleton() {
    }
}

public class Sample {
    public static void main(String[] args) {
        Singleton singleton = new Singleton();  // 컴파일 오류가 발생한다.
    }
}
```
> Singleton 클래스를 private로 정의했기 때문에 Sample에서 만드려는 singleton 객체때문에 오류가 발생한다.

```java
class Singleton {
	private static Singleton one;
    private Singleton() {
    }

    public static Singleton getInstance() {
		if(one==null) {
			one = new Singleton();
		}
        return one;
    }
}

public class Sample {
    public static void main(String[] args) {
        Singleton singleton1 = Singleton.getInstance();
		Singleton singleton2 = Singleton.getInstance();
		System.out.println(singleton1 == singleton2);
    }
	
	//결과 : true
}
```
> 위와 같이 static으로 getInstance 메소드를 정의하고 static 변수 one을 비교하고 Singleton 객체를 반환하면 단 하나만의 객체를 만드는 싱글톤 패턴이 완성된다.
> main 메소드에서 singleton1, singleton2이 같은 객체인지 비교하기 위해 출력해보니 true 값으로 같은 객체로 확인 할 수 있다.

출처 <br/>
[https://wikidocs.net/232](https://wikidocs.net/232)<br/>
[https://wikidocs.net/228](https://wikidocs.net/228)<br/>
