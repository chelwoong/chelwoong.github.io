---
layout: post
title: Swift - Dictionary
date: 2019-01-16
excerpt: "Swift Dictionary"
tag:
- ios
- swift
comments: true
---

## 사전(Dictionaries)

> Swift의 Dictionary타입은 Foundation 클래스의 NSDictionary를 bridge한 타입입니다.

### 축약형 Dictionary

[Key: Value] 형태로 Dictionary를 선언해 사용할 수 있습니다.

### 빈 Dictionary의 생성
```swift
var namesOfIntegers = [Int: String]()
```
```swift
namesOfIntegers[16] = "sixteen"
namesOfIntegers = [:]
// 빈 배열
```
### 리터럴를 이용한 Dictionary의 생성

[key 1: value 1, key 2: value 2, key 3: value 3] 형태로 사전 선언 가능
```swift
var airports: [String: String] = = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
```
### Dictionary의 접근과 변경
```swift
print("The airports dictionary contains \(airports.count) items.")
// The airports dictionary contains 2 items.
```
빈 Dictionary 확인
```swift
if airports.isEmpty {
    print("The airports dictionary is empty.")
} else {
    print("The airports dictionary is not empty.")
}
// The airports dictionary is not empty.
```
값 할당
```swift
airports["LHR"] = "London"
// the airports dictionary now contains 3 items
```

참고  
[Swift document(한국어) - 콜렉션 타입](https://jusung.gitbook.io/the-swift-language-guide/untitled-1)  