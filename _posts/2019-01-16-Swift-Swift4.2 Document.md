---
layout: post
title: Swift - Swift 4.2 Document
date: 2019-01-16
excerpt: "Swift Document정리"
tag:
- ios
- swift
comments: true
---

# Swift document 	

C와 Java와 같은 다른 언어에 익숙한 나같은 사람에게 스위프트는 굉장히 생소하게 느껴질 수 있다. 도대체 왜 이 모양인지 왜 이렇게 만들었는지는 doc를 참고하는게 제일 빠른법. Stanford CS193P 강의를 참조해 필수적으로 알아야 하는 부분들을 정리해보자.

## LANGUAGE GUIDE
 
 ### The Basic
- **Type Safety and Type Inference**

스위프트는 **type-safe** 언어이다.  type-safe언어는 가능한 타입을 명확하게 명시해야 한다. 

스위프트가 type safe인 이유는 타입체크를 위해서이다. 이는 에러를 막도록 돕는다. 하지만 type safe라는 뜻이 항상 명시적으로 타입을 선언해야 한다는 뜻은 아니다. 스위프트는 타입 추론이 가능하다. 한마디로 명시하지 않아도 컴파일러가 무슨 타입인지 추정해서 타입을 정한다는 뜻이다.

예를들어, 
~~~ swift
 let meaningOfLife = 42
 // 소수점이 없는 숫자는 Int 타입으로 추정된다. 
 let pi = 3.14159
 // 소수점이 있는 숫자는 Double 타입으로 추정된다.
 let anotherPi = 3 + 0.14159
 // Int와 Double의 합은 Doublef로 추정된다.
~~~

-  **Numeric Type Conversion**

음수로 생각되더라도 Int type을 사용해라. Int type은 상황에따라 상수 또는 변수로 적용될 수 있다. 

특별히 필요한 경우에만 다른 integer type을 사용해야 하는데, 외부소스에서 명시적으로 크기가 정해진 데이터나, 성능, 메모리 사용이나 기타 필요한 최적화를 위해 필요할 때만 사용한다. 이럴 때 명시적으로 크기가 지정된 타입을 사용하면 우발적인 오버플로우를 잡아내고 데이터의 특성을 암시적으로 문서화 할 수 있다.

- **Optionals**

값이 존재하지 않을 수도 있을 때 optionals을 사용한다. optional은 값이 있거나 없거나 두 가지 상태를 나타낸다.

> optionals는 c나 object-c에는 존재하지 않는다. Object-c는 nil을 리턴하는데, nil은 유요한 object가 존재하지 않는다는 의미이다. 

아래는 String으로 선언된 상수를 Int로 변환하는 예제이다.
~~~ swift
 let possibleNumber = "123"
 let convertedNumber = Int(possibleNumber)
 // convertedNumber는 "Int?" 또는 "optional Int"타입을 갖는다.
~~~

Int?의 ?는 값이 optional을 포함하고 있음을 나타낸다. 이는 Int이거나 nil. 없거나를 뜻한다. String이나 Bool같은 다른 변수는 절대 올 수 없다.

**nil**
nil 변수는 값이 없음을 나타낸다. optinal로 타입을 지정하고 값을 지정하지 않으면 자동으로 nil값이 들어간다.

**Optional Binding**

optinal binding을 사용해 optional을 포함하고 있는 변수인지 아닌지를 찾을 수 있다. if 나 while을 사용하는데, 다음과 같이 사용한다.
~~~ swift
 if let constantName = someOptinal {
	 statements
	 }
~~~

~~~ swift
if let actualNumber = Int(possibleNumber) {
	print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
	print("The string \"\(possibleNumber)\" could not be converted to an integer")
}
// Prints "The string "123" has an integer value of 123"
~~~

**Implicitly Unwrapped Optionals**


### Basic Operators


### Strings and Characters

- **Accessing and Modifying a String**
