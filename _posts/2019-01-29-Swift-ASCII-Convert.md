---
layout: post
title: Swift-ASCII-Unicode
date: 2019-01-28
excerpt: "Swift Unicode Code Convert"
tag:
- swift
- Algorithm
- BOJ
- 문자열 처리
comments: true
---

문자열을 처리할 때 많이 쓰이는 ASCII((American Standard Code for Information Interchange, 미국 정보 교환 표준 부호)변환! 이번에 항상 헷갈리는 이녀석들 이번에 제대로 정리해고자 한다.

ASCII코드는 7비트, 즉 128개의 고유값만 사용한다. 한글만 생각해도 128개로는 택도 없다. 따라서 나온 것이 `unicode` ! 

### Unicode

유니코드는 다른 시스템에서 쓸 수 있도록 하는 국제 표준이다. 거의 모든 문자와 언어를 표현 가능하다. 

당연히 Swift에도 문자열 타입과 문자 타입은 모든 유니코드와 호환된다. 따라서 우리도 unicode를 사용해 ASCII코드 변환을 정복해보자.


### Unicode Scalars

Swift의 네이티브 문자열 타입은 유니코드 스칼라 값에서 만들어진다. 유니코드 스칼라는 21-bit.

이론은 그만하고 바로 구체적인 사용법을 알아보자.

### Unicode to Int

~~~swift
var char = "A"

print(UnicodeScalar(char)?.value) // 65: UInt32
~~~

### Int to Unicode

~~~swift
var int = 65

print(UnicodeScalar(int)?.value) // A: UInt32
~~~

Swift에서 Int -> Unicode 혹은 Unicode -> Int 로 변환하는 방법은 `UnicodeScalar`를 사용해 같은 방법으로 해결할 수 있다.

### String to Unicode

문자열의 경우 간단한 방법으로 ASCII코드를 뽑아낼 수 있다.

~~~swift
let a = "Aasdf"

for i in a.utf16 {
    print(i) 
    // 65
    // 97
    // 115
    // 100
    // 102
}
~~~

한 가지 더 사용팁이 있는데 **Character**를 `extension`해서 해당 유니코드가 ASCII코드인지, 맞다면 ASCII코드로 변환시켜주도록 만들 수도 있다. 문자열의 경우 **StringProtocol**을 이용한다.

### to Unicode with extension
~~~ swift
extension Character {
    var isAscii: Bool {
        return unicodeScalars.first?.isASCII == true
    }
    var ascii: UInt32? {
        return isAscii ? unicodeScalars.first?.value : nil
    }
}
~~~
~~~ swift 
extension StringProtocol {
    var ascii: [UInt32] {
        return compactMap { $0.ascii }
    }
}
~~~

참고
[민소네님 블로그](http://minsone.github.io/mac/ios/swift-string-and-characters-summary)
[Zedd님 블로그](https://zeddios.tistory.com/340)
[stackoverflow](https://stackoverflow.com/questions/29835242/whats-the-simplest-way-to-convert-from-a-single-character-string-to-an-ascii-va)
