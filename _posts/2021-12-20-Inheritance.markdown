---
title: "JAVA 객체지향 3"
permalink: /2021-12-20-Inheritance
excerpt: "객체지향 프로그래밍을 위한 [상속]"
date: "2021-12-20 09:40:00 +0900"
last_modified_at: 2021-12-20T09:40:18
toc: true
toc_sticky: true
categories:
  - OPP
  - JAVA
---
내가 이해하기 위한 JAVA 객체지향 3
# 상속

다른 java 파일에서 구현된 클래스와 그 기능을 가져올 수 있는 상속에 대해 살펴보자

*Animal.java*

```java
public class Animal {
	String name;
	
	public void setName(String name) {
		this.name = name;
	}
}
```

<br/>*Dog.java*
```java
public class Dog extends Animal {
}
```

클래스 상속을 위해 <mark>extends</mark> 를 사용한다.

*Dog.java*는 *Animal.java*를 상속받았으며, *Dog.java* 클래스에서는 구현되지 않은 name과 setName이라는 메소드를 *Animal.java*에서 가져와서 사용하는 것이다.

```java
public class Dog extends Animal {
	public static void main(String[] args) {
		Dog dog = new dog();
		dog.setName("poppy");
		System.out.println(dog.name);
		
		//결과 : poppy
	}
}
```
### 상속과 확장
상속받은 클래스는 부모클래스의 기능에서 추가해서 사용할 수 있다. (확장이라고 한다)

예를 들어 자동차라는 클래스에서는 '주행' 기능만 구현되있다면, 테슬라라는 클래스가 자동차 클래스를 상속받고, '자율 주행' 기능을 추가로 구현 할 수 있는 것이다.
즉, 기능을 <mark>구체화</mark>할 수 있는 것이다.

```java
public class Dog extends Animal {
	public void sleep() {
		System.out.println(this.name+" zzz");
		}
	
	public static void main(String[] args){
		Dog dog = new Dog();
		dog.setName("poppy");
		System.out.println(dog.name);
		dog.sleep();
		}
}
```

> Dog 클래스에 sleep이라는 메소드를 확장한 것이다. Animal 클래스보다 더 많은 기능을 가진다

### IS-A 관계
Dog 클래스는 Animal 클래스를 상속했다. Dog는 Animal의 하위 개념이며, "Dog <mark>is  a</mark> Animal" 과 같이 표현 할 수 있기 때문에 **IS-A 관계**라고 한다.

**IS-A 관계일때, 자식 클래스의 객체는 부모 클래스의 자료형인 것처럼 사용 할 수 있다.**

`Animal dog = new Dog(); //자료형은 Animal이고 객체가 Dog이다.`

> 부모 클래스의 자료형으로 자식 클래스의 객체를 구현했을때, 자식 클래스에서 확장시킨 sleep 메소드는 사용 할 수 없다.

##### Object 클래스
자바의 모든 클래스는 Object 클래스를 자동으로 상속받는다.<br/>
따라서 자바에서는 모든 객체가 Object 자료형으로 사용 할 수 있다.

`Object animal = new animal();`
`Object dog = new Dog();`

### 메소드 오버라이딩 (Method overriding)

메소드 오버라이딩은 이름 그대로 메소드를 재정의하는 것이다.<br/>
하위 클래스에서 동일한 형태의 메소드(같은 메소드에 같은 입력값을 넣지만)를 구현하는 것. **부모 클래스의 메소드와는 조금 다른 기능을 하도록 재 구현하는 것이다.**

*HouseDog.java*

```java
public class HouseDog extends Dog {
	public static void main(String[] args) {
		HouseDog houseDog = new HouseDog();
		houseDog.setName("happy");
		houseDog.sleep();
		
		//결과 : happy zzz
	}
}
```

> 위의 코드가 Dog 클래스에서 상속받아 sleep이라는 메소드를 사용한 코드이고, 아래의 코드가 메소드 오버라이딩해서 `HouseDog zzz in house`가 나오도록 수정한 것이다.

```java
public class HouseDog extends Dog {
	public void sleep() {
		System.out.println(this.name+" zzz in house");
	}
	
	public static void main(String[] args) {
		HouseDog houseDog = new HouseDog();
		houseDog.sleep();
	}
	
	//결과 : houseDog zzz in house
}
```

### 메소드 오버로딩 (Method overloading)
**메소드 오버로딩**은 오버라이딩과 다르게 다른 형태의 메소드(동일한 이름의 메소드에 입력값이 다를 경우)를 **추가**하는 것이다.

```java
public class HouseDog extends Dog {
	public void sleep() {
		System.out.println(this.name+ " zzz in house");
	}
	
	public void sleep(int hour) {
		System.out.println(this.name+ " zzz in house for " + hour + " hours");
	}
	
	public static void main(String[] args) {
		HouseDog houseDog = new HouseDog();
		houseDog.setName("happy");
		houseDog.sleep();
		houseDog.sleep(3);
	}
	
	//결과 : happy zzz in house
	//		happy zzz in house for 3 hours
}
```

> 먼저 구현된 sleep 메소드는 ~~입력값 x, 출력값 x~~ 상속받은 Dog 클래스에서 오버라이딩하여 "zzz in house"로 **변경**된 메소드이고,
> 다음에 구현된 sleep 메소드는 ~~입력값 O, 출력값 O~~ 오버로딩하여 입력값이 있는(다른 형태) 메소드를 **추가** 한 것이다.

### 다중 상속

클래스가 동시에 하나 이상의 클래스를 상속받는 것을 뜻한다.
하지만 자바는 다중 상속이 지원되지 않고, 파이썬이나 c++에서 다중 상속이 지원되며, 우선순위를 적용하여 해결한다.

출처<br/>
[https://wikidocs.net/280](https://wikidocs.net/280)