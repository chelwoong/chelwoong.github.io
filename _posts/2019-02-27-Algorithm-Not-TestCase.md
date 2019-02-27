---
layout: post
title: Algorithm-Not-TestCase
date: 2019-02-27
excerpt: "테스트 케이스가 주어지지 않은 경우의 문제"
tag:
- Algorithm
- swift
- C++
comments: true
---

# 테이스 케이스가 주어지지 않은 문제

  
테스트 케이스가 주어지지 않은 문제는 Input을 받을 때 입력값이 없다면 종료하면 된다.  

말은 간단하지만 어떻게 해야할까..?

### C++

먼저 대표적인 `C++`의 경우부터 알아보자.

scanf의 리턴값을 사용해 풀어보자.

scanf함수는 EOF(end of file)을 만나게 되면 리턴값을 -1로 리턴한다. 따라서 입력을 받았는데 리턴값이 -1이라면 종료하면 된다.  
또는 scanf는 입력받는 개수를 리턴하기 때문에 2개를 입력 받는다면 리턴값이 2가 아닐때 종료하면 된다.  

해당 문제를 풀어보자. [문제링크](https://www.acmicpc.net/problem/10951)  

두 정수 A와 B를 입력받은 다음, A+B를 출력하는 프로그램을 작성하시오.  

라는 간단한 문제이다. 단 테스트 케이스가 주어지지 않았다. 

앞서 설명한대로 scanf값이 2가 아니거나 -1이라면 종료하면 된다.
```c++
# include<iostream>
using namespace std;

int main(int argc, const char * argv[]) {
	int a, b;

	while(scanf("%d%d", &a, &b) != EOF) {
		printf("%d", a+b);
	}
	
	return 0;
}
```

또는

```c++
# include<iostream>
using namespace std;

int main(int argc, const char * argv[]) {
	int a, b;

	while(scanf("%d%d", &a, &b) == 2) {
		printf("%d", a+b);
	}
	
	return 0;
}
```

### swift

다음으로 swift의 경우를 알아보자.  
c++과 원리는 같다. swift의 경우 nil이 아닐 경우 종료하면 된다.


```swift 
while true {
	let input = readLine()?.split(separator: " ").map{Int($0) ?? 0}

	if input != nil {
		if let a = input[0], let b = input[1] {
			print(a+b)
		}
		else {
			break
		}
	}
}
```

이렇게 하지 않고 바로 C++처럼 while의 조건문에 input을 받아 처리할 수도 있다.
이렇게 되면 unwrapping도 바로 할 수 있어서 코드를 간단하게 줄일 수 있다.

```swift
while let input = readLine()?.split(separator: " ").map({Int($0) ?? 0}) {
	print(input[0] + input[1])
}
```

참고  
[박트리님 블로그](https://baactree.tistory.com/28)