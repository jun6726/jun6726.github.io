---
title: "JAVA 객체지향 7"
permalink: /Exception/
excerpt: "객체지향 프로그래밍을 위한 [예외]"
date: "2021-12-22 13:25:00 +0900"
last_modified_at: 2021-12-22T13:50:18
toc: true
toc_sticky: true	
categories:
  - OOP
  - JAVA
---
내가 이해하기 위한 JAVA 객체지향 7
# 예외처리 (Exception)
프로그램 오작동을 위한 컴파일 오류를 제어하기 위해 try catch, throw 구문을 이용한다.
Exception 상황은 단순한 프로그래머의 실수가 아닌 파일 오픈같은 경우에 생기는 오류를 뜻한다.
다음처럼 존재하지 않는 파일은 열려고 시도하거나 0으로 나누려고 할 때 등 시스템적으로 처리 할 수 없을 때 발생한다.

```java
1.
BufferedReader br = new BufferedReader(new FileReader("나없는파일"));
br.readLine();
br.close();
2.
int c = 4 / 0;
```
> 해당 코드들은 아래와 같은 에러메시지를 출력한다.

&nbsp; 1. <br/>
Exception in thread "main" java.io.FileNotFoundException: 나없는파일 (지정된 파일을 찾을 수 없습니다)<br/>
    &nbsp; at java.io.FileInputStream.open(Native Method)<br/>
    &nbsp; at java.io.FileInputStream.<init>(Unknown Source)<br/>
    &nbsp; at java.io.FileInputStream.<init>(Unknown Source)<br/>
    &nbsp; at java.io.FileReader.<init>(Unknown Source)<br/>
    ...<br/>
&nbsp; 2.<br/>
Exception in thread "main" java.lang.ArithmeticException: / by zero<br/>
    &nbsp; at Test.main(Test.java:14)	<br/>
{: .notice--danger}

### 예외 처리하기

try, catch 기본문
```java
try{
	...
	} catch(예외 1) {
		...
	} catch(예외 2) {
		...
	}
...
}
```
예외(위에서 말한 시스템적인 오류)가 발생할만한 내용을 try문 안에 작성하고, 그로 인해 생기는 예외(Exception)를 catch문 뒤에 넣고 처리할 방법을 catch문 안에 정의하면 된다.

ex)
```java
int c;
try {
	c = 4 / 0; // ArithmeticException 발생
	} catch(ArithmeticException e) { // 발생할 Exception에 대해 미리 정의
		c = -1; // 0으로 나눌 수 없는 예외발생으로 c를 다른 방법으로 처리
	}
}
```

##### finally	
try문에서 예외가 발생해도 **반드시 실행**되어야 하는 부분을 정의하는 부분이다.

```java
public class Sample {
    public void shouldBeRun() {
        System.out.println("ok thanks.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        int c;
        try {
            c = 4 / 0;
        } catch (ArithmeticException e) {
            c = -1;
        } finally {
            sample.shouldBeRun();  // 예외에 상관없이 무조건 수행된다.
        }
    }
}
```
> finally 문은 예외 여부에 상관없이 항상 실행되기 때문에 항상 ok thanks는 출력 될 것이다.

##### RuntimeExeption과 Exception
RuntimeExeption은 실행시 발생하는 예외이고, Exception은 컴파일시 발생하는 예외이다.
RuntimeExeption은 실행 중에 사용자의 입력에 따라 발생 여부가 달라지는 경우에 작성한다.

그래서 아래 코드를 실행할때 RuntimeException 말고 Exception을 상속받으면<br/>

throw new FoolException으로 예외를 처리할 것을 try, catch문으로 예외 처리방법에 대해 정의해둬야할 것이다.

```java
public class Sample {
    public void sayNick(String nick) {
        if("fool".equals(nick)) {
            return;
        }
        System.out.println("당신의 별명은 "+nick+" 입니다.");
    }

    public static void main(String[] args) {
        Sample test = sample Sample();
        sample.sayNick("fool");
        sample.sayNick("genious");
    }
}
```

> 위의 코드는 fool이라는 별명은 출력하지 않고, genious라는 별명만 출력하는 예제이다.
> 아래 코드에서 fool이라는 별명에 대해서는 강제로 예외를 발생시키는 예제를 보겠다.

```java
class FoolException extends RuntimeException {
}

public class Sample {
    public void sayNick(String nick) {
        if("fool".equals(nick)) {
            throw new FoolException(); // 예외 처리를 위해 throws - 바로 다음에 설명할 것이다.
        }
        System.out.println("당신의 별명은 "+nick+" 입니다.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious");
    }
}
```

> sayNick 메소드에서 return으로 메소드를 종료하던 것을 `throws new FoolException` 으로 예외 처리를 하려고 했으나

Exception in thread "main" FoolException
    &nbsp; at Sample.sayNick(Sample.java:7)
    &nbsp; at Sample.main(Sample.java:14)
{: .notice--danger}	

> 위와 같은 오류를 출력한다. 

RuntimeException을 상속받던 것을 Exception으로 변경한 코드를 보자

###### sayNick 메소드에서 예외처리

```java
class FoolException extends Exception {
}

public class Sample {
    public void sayNick(String nick) {
        try {
            if("fool".equals(nick)) {
                throw new FoolException();
            }
            System.out.println("당신의 별명은 "+nick+" 입니다.");
        }catch(FoolException e) {
            System.err.println("FoolException이 발생했습니다.");
        }
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious");
    }
}
```
> Exception으로 변경만 하면 Sample클래스에서 컴파일 오류가 발생할 것이다. (Exception은 Checked Exception이기 때문
> 정상적인 컴파일을 위해 Exception으로 변경하면서 try, catch문으로 FoolException을 예외처리 했다.


##### throws

throws를 이용하면 sayNick 메소드에서 직접 예외처리하지 않고, 호출한 곳에서 처리하도록 **위로 던질(throws)** 수 있다.


```java
public class Sample {
    public void sayNick(String nick) throws FoolException { // throws
        if("fool".equals(nick)) {
            throw new FoolException();
        }
		System.out.println("당신의 별명은 "+nick+" 입니다.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        sample.sayNick("fool");
        sample.sayNick("genious");
    }
}
```

> 예외가 발생하는 메소드 이름 뒤에 **throws (예외명)** 으로 정의함으로 메소드를 호출하는 부분에서 예외처리를 해야한다.
> 이 예제의 경우 main 메소드에서 컴파일오류가 발생하니 예외처리를 해줘야한다.

###### main 메소드에서 예외처리

```java
class FoolException extends Exception {
}

public class Sample {
    public void sayNick(String nick) throws FoolException {
        if("fool".equals(nick)) {
            throw new FoolException();
        }
        System.out.println("당신의 별명은 "+nick+" 입니다.");
    }

    public static void main(String[] args) {
        Sample sample = new Sample();
        try {
            sample.sayNick("fool");
            sample.sayNick("genious");
        } catch (FoolException e) {
            System.err.println("FoolException이 발생했습니다.");
        }
    }
}
```
> main 메소드에서 try, catch 문으로 예외 처리를 했다.

**예외 처리는 1. 예외가 발생하는 구문과 2. 예외가 발생하는 구문을 호출하는 메소드** 두 곳에서 모두 가능하다.

> 그렇다면 어디서 예외 처리를 하는 것이 더 좋은 것일까

1. [sayNick 메소드에서 예외처리](https://jun6726.github.io/2021-12-22-Exception#saynick-%EB%A9%94%EC%86%8C%EB%93%9C%EC%97%90%EC%84%9C-%EC%98%88%EC%99%B8%EC%B2%98%EB%A6%AC) 를 한다면 fool과 genious 두 문장 모두 수행한다.

2. [main 메소드에서 예외처리](https://jun6726.github.io/2021-12-22-Exception#main-%EB%A9%94%EC%86%8C%EB%93%9C%EC%97%90%EC%84%9C-%EC%98%88%EC%99%B8%EC%B2%98%EB%A6%AC) 를 한다면 fool에서 FoolException이 발생하고 catch 문으로 genious도 수행하지 못한다.

**Exception 처리 위치는 프로그램 수행 여부와 트랜잭션 처리와 관계있기 때문에 매우 중요하다.**


### 트랜잭션 (Transaction)

트랜잭션은 하나의 작업 단위로 "상품발송"으로 예를 들면 상품발송에는 (포장 > 영수증발행 > 발송)으로 이루어지고 3가지의 일 중 하나라도 실패하면 "상품발송"을 취소한다.
> 모두 취소하지 않으면 정상적인 작업이 아니기 때문에 롤백(Rollback) 한다고 말한다.


```
상품발송() {
	try {
		포장();
		영수증발행();
		발송();
	} catch(예외) {
		모두취소(); // 하나라도 실패하면 모두 취소
	}
}

포장() throws 예외{
	...
}

영수증발행() throws 예외 {
	...
}
	
발송() throws 예외 {
	...
}
```

위와 같이 **각 메소드에서 예외를 상품발송으로 throws하고 상품발송 메소드에서 모든 예외를 처리**하는것이 완벽한 트랜잭션 처리 방법이다.

출처
[https://wikidocs.net/229](https://wikidocs.net/229)