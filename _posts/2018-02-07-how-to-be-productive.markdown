---
layout: post
title: How to be productive?
image: 9.jpg
date: 2018-02-07 17:50:18 +0200
tags: [workflow, programming]
categories: elasticsearch
---
# Lambda

Created: April 30, 2022 7:19 PM
Tags: Java

<aside>
💡 April 30, 2022 에 작성된 게시글 입니다.
이후 변경된 점이 있을 수도 있고, 
잘못 적은 부분이 있을수도 있습니다.  
댓글에 작성 부탁드립니다.

</aside>

## Lambda(람다식)이란?

---

- 익명함수를 지칭하는 용어
- 함수를 보다 단순하게 표현하는 방법

### 장점

- 코드의 간결성
- 지연연상 수행 - 람다는 지연연상을 수행 함으로써 불필요한 연산을 최소화 할 수 있다.
- 병렬처리 가능 - 멀티쓰레드를 활용하여 병렬처리를 사용 할 수 있다.

### 단점

- 람다식의 호출이 까다롭다.
- 람다 stream 사용시 단순 for문 혹은 while문 사용 보다 성능이 떨어진다.
- 불필요하게 사용하게 되면 가독성을 떨어 뜨릴 수 있다.

## 람다 표현식 작성법

```java
(매개변수목록) -> {함수 몸체}

//기존 표현식
int min(int x, int y){
	return x<y ? x: y;
}

//람다 표현식
	(x, y) -> x < y ? x : y;
```

- 유의 사항
    - 매개변수의 타입을 추론할 수 있는 경우 타입을 생략할 수 있다.
    - 매개변수가 하나인 경우에는 괄호(())를 생략할 수 있다.
    - 함수의 몸체가 하나의 명령문만으로 이루어진 경우에는 중괄호({})를 생략할 수 있다.(이 때 세미콜론(;)을 붙이지 않음)
    - 함수의 몸체가 하나의 return 문으로만 이루어진 경우에는 중괄호({})를 생략할 수 없다.
    - return 문 대신 표현식을 사용할 수 있으며, 이 떄 반환값은 표현식의 결과값이 된다.(이 때 세미콜론(;)은 붙이지 않음)
        
        ```java
        new Thread(new Runnable() {
        		public void run(){
        			System.out,println("전통적인 방식의 스레드 생성");
        			}
        }).start();
        
        new Thread(()->{
        		System.out.println("람다 표현식을 사용한스레드 생성");
        }).start();
        ```
        

### 함수형 인터페이스(functional interface)

- 람다 표현식을 사용할 때는 람다 표현식을 저장하기 위한 참조 변수의 타입을 결정해야만 합니다.
- 참조변수의타입 참조변수의이름 = 람다표현식
- 함수형 인터페이스는 추상 클래스와는 달리 단 하나의 추상 메소드만을 가져야 한다.
- @FunctionalInterface를 사용하여 함수형 인터페이스임을 명시 할 수 있다.

```java
@FunctionalInterface
interface Calc { //함수형 인터페이스의 선언
		public int min(int x, int y);
}

public class Lambda02{
	public static void main(String[] args){
			Calc minNum = (x, y) -> x < y ? x : y; //추상 메소드의 구현
			System.out.println(minNum.min(3,4)); //함수형 인터페이스의 사용
}
```

## Reference

[코딩교육 티씨피스쿨](http://www.tcpschool.com/java/java_lambda_concept)

[[JAVA] 람다식(Lambda)의 개념 및 사용법](https://khj93.tistory.com/entry/JAVA-%EB%9E%8C%EB%8B%A4%EC%8B%9DRambda%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%82%AC%EC%9A%A9%EB%B2%95)

---