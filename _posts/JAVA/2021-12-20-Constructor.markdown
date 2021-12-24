---
title: "JAVA 객체지향 4"
permalink: /JAVA/2021-12-20-Constructor
excerpt: "객체지향 프로그래밍을 위한 [생성자]"
date: "2021-12-20 10:50:00 +0900"
last_modified_at: 2021-12-20T10:50:18
toc: true
toc_sticky: true	
categories:
  - OOP
  - JAVA
---
내가 이해하기 위한 JAVA 객체지향 4
# 생성자(Constructor)

생성자는 객체가 생성될때 필수로 입력받아야하는 데이터를 정의하는 메소드

```java
public HouseDog(String name) {
	this.setName(name);
}
```

**리턴 자료형을 정의하지 않고, 클래스 명과 동일한 이름을 가지는 메소드.**

생성자의 규칙
1. 클래스명 = 메소드명
2. 리턴타입 X (void와 다름)

> 생성자는 객체가 생성될 때 호출, 즉 `new 클래스명(입력인수, ...)` 과 함께 호출된다.
> 위의 코드를 이어 쓴다면 아래와 같이 new 키워드로 객체를 만들때 문자열(name)을 꼭 전달해야한다.

ex)
`HouseDog dog = new HouseDog("happy");`

아래와 같이 코딩한다면 오류가 발생한다.
HouseDog dog = new HouseDog();
{: .notice--danger}

> 생성자가 선언된 경우 생성자의 규칙대로만 객체를 생성 할 수 있다.

**생성자는 필수적인 행동(데이터 입력과 같은..)을 객체 생성시에 제어할 수 있는 장점이 있다.**


### 디폴트(Default) 생성자

아무 내용이 없는 생성자를 **디폴트 생성자**라고 한다.

```java
public class Dog extends Animal {
	public Dog() {
	}
	
	public void sleep() {
		System.out.println(this.name + " zzz");
	}
}
```

> 클래스가 생성될 때 생성자가 선언되어 있지 않다면, 자동으로 시스템에서 위와 같은 디폴트 생성자가 실행된다.
> 만약 생성자가 하나라도 구현되어 있다면 컴파일러는 디폴트 생성자를 추가하지 않는다.

### 생성자 오버로딩

하나의 클래스에 여러개의 생성자를 만들 수 있다. (각각 입력항목이 다름)

```java
public class HouseDog extends Dog {
	public HouseDog(String name) {
		this.setName(name);
	}
	
	public HouseDog(int type) {
		if (type == 1) {
			this.setName("yorkshire");
		} else if (type == 2) {
			this.setName("bulldog");
		}
	}
	
	public void sleep() {
		System.out.println(this.name + " zzz in house");
	}
	
	public void sleep(int hour) {
		System.out.println(this.name + "zzz in house for" +hour+"hours");
	}
	
	public static void main(String[] args) {
		HouseDog happy = new HouseDog("hapyy");
		HouseDog yorkshire = new HouseDog(1);
		System.out.println(happy.name);
		System.out.println(yorkshire.name);
	}
	
	//결과 : happy, yorkshire
}
```

> 두 가지 방법으로 HouseDog을 분류하는 생성자들이다.
> 1. String으로 입력 받아서 이름을 직접 입력하는 방법과
> 2. int 값으로 type 변수에 넣어 1과 2로 구분하여 yorkshire/bulldog 중 선택하는 생성자이다.

이렇게 여러개의 생성자를 만드는게 생성자 오버로딩이다.

출처<br/>
[https://wikidocs.net/281](https://wikidocs.net/281)
