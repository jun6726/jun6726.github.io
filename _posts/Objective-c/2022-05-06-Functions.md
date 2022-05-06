---
title: "Functions"
permalink: /Functions/
last_modified_at: 2022-05-06 T10:56:18-14:00
toc: true
toc_sticky: true
categories:
  - Objective-c
---
내가 이해하기 위한 Objective-c
# Functions

Objective-c 에서 함수를 선언하는 방법은 두 가지가 있다
함수명 앞에 (-), (+)을 붙이는거에 따라 인스턴스 함수와 클래스 함수로 나눠진다

-(반환 유형) 메소드명: (매개변수 타입1) 매개변수명1   결합인수명1: (매개변수 타입2) 매개변수명2 ...
 * 반환 유형에 대한 설명은 링크[https://jun6726.github.io/Method/](https://jun6726.github.io/Method/) 에서 확인 바랍니다

작동 가능한 코드로 에시를 들면

```objective-c
    #import <Foundation/Foundation.h>

    @interface SampleClass:NSObject
    /* method declaration */
    -(int) max: (int)num1 andNum2: (int)num2;
    
    @end
    
    @implementation SampleClass
    
    - (int)max: (int)num1 andNum2:(int)num2 {
        int result;
        
        if(num1 > num2) {
            result = num1;
        } else {
            result = num2;
        }
        return result;
    }   
    @end
    
    int main() {
        int a = 100;
        int b = 200;
        int ret;
        
        SampleClass *sampleClass = [[SampleClass alloc] init];
        
        ret = [sampleClass max:a andNum2:b];
        
        return 0;
    }
```

 
