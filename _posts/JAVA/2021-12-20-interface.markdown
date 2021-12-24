---
title: "JAVA 객체지향 5"
permalink: /Interface/
excerpt: "객체지향 프로그래밍을 위한 [인터페이스]"
date: "2021-12-20 11:32:00 +0900"
last_modified_at: 2021-12-21T15:32:18-16:50
toc: true
toc_sticky: true
categories:
  - OOP
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
}
```

> **기존 클래스와 상속과 구현**을 이용한다면 <U>포식자 > 동물 > 호랑이(사자)</U>로 IS-A 관계가 성립되며, 
> 포식자의 객체 동물 또는 호랑이(사자)로 생각할 수 있으며, predator나 Animal의 자료형으로 
> 호랑이와 사자 모두를 정의 할 수 있다. 
> 이와 같이 객체가 하나 이상의 자료형 타입을 갖게되는 특성을 다형성이라고 하고, 다형성을 가진 클래스는 여러가지 자료형으로 표현 할 수 있다.

`호랑이같이 다형성을 가진 클래스는 Tiger/Animal/Predator/Barkable 등의 자료형으로 표현가능하다.`

### 인터페이스의 메소드

위의 인터페이스에서 문제점은 어떤 자료형이 오더라도 같은 결과값을 도출한다는 것이다.
문제점을 해결하기 위해서는 인터페이스에 메소드를 정의하고 실제 클래스에서 메소드를 구현(구체화) 해줘야한다.

*Predator.java*
```java
public interface Predator {
    public String getFood();
}
```

> 인터페이스에 getFood()라는 몸통만 있는 메소드를 추가했다
> **인터페이스는 규칙이기 때문에 입출력에 대한 정의**만 있는 것이다.
> (메소드의 존재만 선언하고, 기능은 상속받은 클래스에서 구현)

*Tiger.java*

```java
public class Tiger extends Animal implements Predator {
    public String getFood() {
        return "apple";
    }
}
```

> ~~호랑이 클래스에서 동물을 상속받고 포식자를 구현한다~~
<br/>포식자 인터페이스에서 선언했던 getFood() 메소드를 오버로딩하여 사과를 반환하도록 하면
> ZooKeeper 클래스에 있던 feed에 호랑이가 들어가면서 사과를 던져준다.

### 인터페이스의 핵심

**인터페이스의 핵심**은 메소드가 줄어들었다는 점이 아니라 ZooKeeper클래스가 Animal종류에 **의존적인 클래스에서 독립적인 클래스가 되었다는점이다.** 

### 상속과 인터페이스의 차이

인터페이스는 **강제성**을 가진다.
상속은 자식 클래스가 부모 클래스의 메소드를 오버라이딩하지 않고 사용할 수 있지만, 인터페이스를 정의할 때 메소드를 정의하고 클래스에서 인터페이스에서 정의된 메소드를 구체화해야하는 강제성을 지니기 때문이다.

## 추상 클래스

추상클래스는 인터페이스 역할도 하면서 실제 메소드도 가지고 있다.
위에서 정의했던 Predator 인터페이스를 변형해서 추상 클래스를 확인해보자

*predator.java*

```java
public abstract class Predator extends Animal {
    public abstract String getFood();
}
```

> 추상 클래스와 추상 메소드를 위해 **abstract**를 붙여준다. 인터페이스의 메소드와 같이 몸통이 없다.([설명](https://jun6726.github.io/2021-12-20-interface#%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EB%A9%94%EC%86%8C%EB%93%9C))
> 추상 클래스는 인터페이스와 같이 상속받아 사용하고, 추상 메소드도 인터페이스 메소드처럼 구현(구체화)해야한다.
> 인터페이스와 다른 점은 실제 메소드도 정의할 수 있다.

### 추상 클래스 vs 인터페이스

##### 클래스 / 추상클래스 / 인터페이스

클래스를 설계도라고 하면, 추상 클래스는 미완성 설계도(추상 메소드를 포함 - 상속받은 클래스에서 구현(구체화)해줘야함)이고, 인터페이스는 설계도 중 한 곳의 밑그림 같은 느낌이다.

추상화/구체화 정도로 비교해보자면 `추상적) 인터페이스 > 추상 클래스 > 클래스 (구체적` 라고 생각된다.

##### 추상클래스와 인터페이스의 공통점
1. 추상메소드를 정의하고 있으며 상속받은 클래스에서 구현해야한다.
2. 혼자만으로 인스턴스화(객체화)를 할 수 없다. (클래스에 상속한다)


##### 추상클래스와 인터페이스의 차이점
1. 추상 클래스는 추상메소드와 실제메소드를 가질 수 있지만 인터페이스는 추상메소드만 가진다. **(인터페이스는 모든 메소드를 오버라이딩해야함)**
2. 추상 클래스는 클래스이기때문에 다중상속이 안되지만 인터페이스는 다중상속이 가능하다.
3. 추상 클래스는 IS-A 관계, 인터페이스는 HAS-A 관계에 가깝다. 무슨 뜻이냐면 추상클래스는 "~이다"에 가깝고, 인터페이스는 "~를 할 수 있는"에 가깝다.
4. 인터페이스에서는 모든 변수가 public static final, 모든 메소드가 public abstract로 고정이다.
5. **중요한 것은 추상클래스는 객체들의 공통점을 찾아 추상화시킨 것이고, 인터페이스는 조상 클래스가 다르더라도 같은 기능을 할 때 사용한다.**	

##### 추상클래스와 인터페이스 사용 케이스

+ 추상 클래스
	- 관련성이 높은 클래스 간에 코드를 공유하고 싶은 경우
	- 추상 클래스를 상속 받을 클래스들이 공통으로 가지는 메소드와 필드가 많거나, public이외의 접근자(protected, private) 선언이 필요한 경우 non-static, non-final 필드 선언이 필요한 경우 (각 인스턴스에서 상태 변경을 위한 메소드가 필요한 경우)
+ 인터페이스
	- 서로 관련성이 없는 클래스들이 인터페이스를 구현하게 되는 경우.
		- ex) Comparable, Cloneable 인터페이스는 여러 클래스들에서 구현되는데, 구현클래스들 간에 관련성이 없다.
	- 특정 데이터 타입의 행동을 명시하고 싶은데, 어디서 그 행동이 구현되는지는 신경쓰지 않는 경우.
	- 다중상속을 허용하고 싶은 경우
	
		
<img data-action="zoom" src='{{ "/assets/image/abstract_class_vs_interface.png" | relative_url }}' alt='absolute'>

**실제 구현한 코드가 있는 결과, 설명은 세번째 출처에서 꼭 확인바란다.**


출처 <br/>
[https://wikidocs.net/217](https://wikidocs.net/217) <br/>
[https://wikidocs.net/219](https://wikidocs.net/219) <br/>
[https://myjamong.tistory.com/150](https://myjamong.tistory.com/150) <br/>
	  
[https://velog.io/@new_wisdom/Java-%EC%B6%94%EC%83%81-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%99%80-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%B0%A8%EC%9D%B4](https://velog.io/@new_wisdom/Java-%EC%B6%94%EC%83%81-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%99%80-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%B0%A8%EC%9D%B4)
	  