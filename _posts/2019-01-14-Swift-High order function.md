---
layout: post
title: Swift - 고차함수 (High order function)
date: 2019-01-14
excerpt: "What is high order function?"
tag:
- ios
- swift
comments: true
---


# 고차함수 ( High Order function)

### 고차함수란?

- 하나 이상의 함수를 인자로 취하는 함수
- 함수를 결과로 반환하는 함수 
- Swift에서 대표적인 예로는 map, reduce, filter 등이 있다.

### map

콜렉션 내부의 기존 데이터를 변형하여 새로운 콜렉션 생성
다시말해  array, dictionary 등의 요소들을 함수에 넣어서 요소마다 적용시켜준다.
container.map(f(x))	// 컨테이너의 map 메서드 호출
-> return f( 컨테이너의 각 요소 ) // 새로운 컨테이너

각 원소들을 2씩 곱해주는 예를 들어보자.
~~~ swift
let num: [Int] = [0, 1, 2, 3, 4]
var doubleNums: [Int] = [Int]()

// for 문 이용
for n in num {
	doubleNums.append(n * 2)
}
print(doubleNums)	// [0, 2, 4, 6, 8]

// map 이용
doubleNums = num.map({ (number: Int) -> Int in 
	return number * 2	
})
print(doubleNums)	// [0, 2, 4, 6, 8]

// map 클로저 축약
doubleNums = num.map { $0 * 2 }
print(doubleNums)	// [0, 2, 4, 6, 8]
~~~


### filter

container 내부의 값을 걸러서 추출

마찬가지로 예를 통해 살펴보자.

~~~ swift
let num: [Int] = [0, 1, 2, 3, 4]
var evenNums: [Int] = [Int]()

// for 문 이용
for n in num {
	if n % 2 != 0 { continue }
	evenNums.append(n)
}
print(doubleNums)	// [0, 2, 4]

// filter 사용
evenNums = num.filter{(number: Int) -> Bool in
	return number % 2 == 0	
}
print(doubleNums)	// [0, 2, 4]

// filter 클로저 축약
evenNums = num.filter { $0 % 2 == 0 }
print(doubleNums)	// [0, 2, 4]
~~~

### reduce 

container 내부의 콘텐츠를 하나로 통합
모든 요소를 어떤 규칙을 가지고 하나로 합쳐준다.

예를 들면,

~~~ swift
let nums: [Int] = [2, 5, 10]
var sum: Int = 0

// for문 이용
for n in nums {
	sum += n 
}
print(sum) 	// 17

// reduce 사용
// reduce는 sum을 상수로 선언할 수 있다.
// 초기값을 0으로 지정해준다.
let sum: Int = nums.reduce(0, {(first:Int, second: Int) -> Int, 
	return first + second
})
print(sum) 	// 17

// reduce 축약
let sum: Int = nums.reduce(3) {  $0 + $1 }
~~~

print(sum)	// 20, 초기값을 3으로 줬음