---
layout: post
title: Swift - Singleton 패턴
date: 2019-01-15
excerpt: "Singleton Pattern 알아보기"
tag:
- ios
- swift
comments: true
---


# Singleton 패턴

많은 프로젝트에서 사용되는 싱글톤 패턴에 대해 알아보자. 

싱글톤 패턴은 특정 클래스에 대해서 객체가 하나만 생성되도록 보장하는 방법이다. 특정 클래스의 값을 여러 클래스에서 공유해야 한다거나, 하나씩 순서대로 처리할 때 주로 사용된다. 사용자 설정값은 여러 객체에서 각각의 값을 저장하기 보다는 앱 전체에서 하나의 값으로 관리되어야 한다. 

싱글톤 패턴 작성 방법에 대해 알아보자.

~~~ swift
class Singleton {
	static let sharedInstance = Singleton()
	fileprivate init() {
	}
}
~~~

싱글톤 패턴은 말그대로 매우 씸플하다. 어느 곳에서든 하나의 값만 존재하는 static 정적 객체를 하나 생성하고 그곳에 클래스 생성을 선언한다.

~~~ swift
// 일반적인 형태
let a = ClassName()
a.normalVar
a.normallet
a.normalFunction()

// 정적 요소 사용시
ClassName.staticVar
ClassName.staticLet
ClassName.staticfuntion()
~~~

좀 더 구체적인 예시를 살펴보자.

~~~ swift
class Singleton {
	static let sharedInstance = Singleton()
	let height: Int
	let weight: Int
	
	private init() {
		self.height = 100
		self.weight = 200
	}
}
~~~

다음과 같은 클래스가 있다면 사용법은 매우 간단하다.

~~~ swift
// singleton 상수에 Singleton 클래스의 객체를 대입한다.
let singleton = Singleton.sharedInstance

print("\(singleton.height), \(singleton.weight)") 	// 100, 200
~~~

싱글톤 패턴의 좋은 점은 현재의 객체를
보고 있는 다른 클래스에서도 싱글톤 객체가 공유되는 것이다.


출처: [알짜배기 예제로 배우는 iOS 프로그래밍](http://blog.eedler.com/27)