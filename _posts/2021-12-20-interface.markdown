---
title: "JAVA 객체지향 5"
permalink: /2021-12-20-interface
excerpt: "객체지향 프로그래밍을 위한 [인터페이스]"
date: "2021-12-20 11:32:00 +0900"
last_modified_at: 2021-12-20T11:32:18-12:28
toc: true
categories:
  - OPP
  - JAVA
---
내가 이해하기 위한 JAVA 객체지향 5
# 인터페이스(interface)

인터페이스란? 반복되는 메소드 오버로딩을 최소화하기 위해 존재하는 것.

*Animal.java*
```java
public class Animal {
    String name;

    public void setName(String name) {
        this.name = name;
    }
}
```

*Tiger.java*

```java
public class Tiger extends Animal {

}
```

*Lion.java*

```java
public class Lion extends Animal {

}
```

*ZooKeeper.java*

```java
public class ZooKeeper {
    public void feed(Tiger tiger) {
        System.out.println("feed apple");
    }

    public void feed(Lion lion) {
        System.out.println("feed banana");
    }

    public static void main(String[] args) {
        ZooKeeper zooKeeper = new ZooKeeper();
        Tiger tiger = new Tiger();
        Lion lion = new Lion();
        zooKeeper.feed(tiger);
        zooKeeper.feed(lion);
    }
}
```

앞에서 정의한 것과 같은 Animal 클래스에 호랑이와 사자가 추가되면서 사육사(ZooKeeper)클래스를 정의하였다.

[메소드 오버로딩](https://ansohxxn.github.io/categories/cpp) 에 의해 호랑이에게는 사과를 사자에게는 바나나를 던져준다.

동물원에 새로운 종류의 동물들이 들어올 것이며, 매번 사육사 클래스의 feed 메소드를 오버로딩해야하는 것이다.

### 인터페이스 작성

*Predator.java*

```java
public interface Predator {
}```
>포식자 인터페이스 정의

class가 아닌 **interface**로 작성한다.
그리고 구현할 호랑이와 사자 클래스에 동물을 상속하고, **implements(구현)**로 인터페이스를 구현한다.

*Tiger(Lion).java*

```java
public class Tiger(Lion) extends Animal implements Predator {

}
```
>포식자 인터페이스로 구현한 호랑이와 사자

```java
public void feed(Tiger tiger) {
    System.out.println("feed apple");
}

public void feed(Lion lion) {
    System.out.println("feed banana");
}
```
위의 코드는 인터페이스를 사용하기 전이고, 아래의 코드는 인터페이스를 이용하여 변경한 feed 메소드를 살펴보면된다.

```java
public void feed(Predator predator) {
    System.out.println("feed apple");
}```
> **기존 클래스와 상속과 구현**을 이용한다면 *포식자>동물>호랑이(사자)*로 IS-A 관계가 성립되며, 
> 포식자의 객체 동물 또는 호랑이(사자)로 생각할 수 있으며, predator나 Animal의 자료형으로 
> 호랑이와 사자 모두를 정의 할 수 있다. (이와 같이 객체가 하나 이상의 자료형 타입을 갖게되는 특성을 다형성이라고 한다)

### 인터페이스의 메소드

위의 인터페이스에서 문제점은 어떤 자료형이 오더라도 같은 결과값을 도출한다는 것이다.
문제점을 해결하기 위해서는 인터페이스에 메소드를 정의하고 구현된 클래스에서 메소드를 구체화(?) 해줘야한다.

*Predator.java*
```java
public interface Predator {
    public String getFood();
}```

> 인터페이스에 getFood()라는 몸통만 있는 메소드를 추가했다
> **인터페이스는 규칙이기 때문에 입출력에 대한 정의**만 있는 것이다.

*Tiger.java*
```java
public class Tiger extends Animal implements Predator {
    public String getFood() {
        return "apple";
    }
}```

> ~~호랑이 클래스에서 동물을 상속받고 포식자를 구현한다~~
<br/>포식자 인터페이스에서 선언했던 getFood() 메소드를 오버로딩하여 사과를 반환하도록 하면
> ZooKeeper 클래스에 있던 feed에 호랑이가 들어가면서 사과를 던져준다.

### 인터페이스의 핵심

**인터페이스의 핵심**은 메소드가 줄어들었다는 점이 아니라 ZooKeeper클래스가 Animal종류에 **의존적인 클래스에서 독립적인 클래스가 되었다는점이다.** 

### 상속과 인터페이스의 차이

인터페이스는 **강제성**을 가진다.
상속은 자식 클래스가 부모 클래스의 메소드를 오버라이딩하지 않고 사용할 수 있지만, 인터페이스를 정의할 때 메소드를 정의하고 클래스에서 인터페이스에서 정의된 메소드를 구체화해야하는 강제성을 지니기 때문이다.

출처 : https://wikidocs.net/217


