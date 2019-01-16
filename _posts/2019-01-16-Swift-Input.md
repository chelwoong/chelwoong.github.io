---
layout: post
title: Swift - Input
date: 2019-01-16
excerpt: "Swift Input받기"
tag:
- ios
- swift
comments: true
---

## Swift에서 Input을 받는 방법

Swift를 iOS개발로만 배우다보니 언어를 배울때 기본중의 기본은 입출력 조차 잘 모르고 있었다.. input..? textfield...?? 어떻게 하는거지..?!

**Swift에서는 `readLine()`을 통해서 입력을 받을 수 있다.**

~~~ swift
print("Please your favorite language.")
let language = readLine()
print("My favorite Language is \(language)")
~~~

다음과 같이 사용할 수 있다. 
`readLine()`은 ==Optional String==을 리턴한다.


### 공백이 있는 문자열 입력 받기.
흔한 입력중에 공백을 갖고있는 문자열을 입력받을 때가 있다.
2가지 방법에 대해 알아보겠다. 

1.  **Foundation** framework에서 제공하는 ==components(separatedBy: " ")== 메소드를 사용하는 것이다.  
~~~ swift
import Foundation

if let input = readLine() {
	let a = input.components(separatedBy: " ")
}
~~~

2.  String 자체의 ==split(separator: " ")== 을 사용하는 것이다. 

~~~ swift
if let input = readLine() {
	let a = input.split(separator: " ")
}
~~~

둘에는 약간의 차이점이 있다. 
우선 보시다시피 **1번의 경우 반드시 Foundation을 import 시켜줘야 한다.** PS를 할 경우 속도에 꽤나 영향을 미친다.
 
또 1번의 경우 [String], 2번은 [String.SubSequence]를 리턴한다. 하지만 이를 사용하는 방법은 별 차이가 없다. 똑같이 a[0], a[1]과 같이 일반 배열을 사용하듯이 사용할 수 있고, 하위 메서드들 또한 같이 갖고 있다. 

_String.SubSequence 란 A slice of a string 으로 String의 조각들이라고 보면된다._

공식 문서에서는 다음과 같이 나와 있는데, SubSequence는 문자열 전체의 참조까지 갖고 있어, 저장할 경우에 메모리 누수가 발생할 수 있다고 한다. 특정 작업을 수행할 경우에만 쓰라는 말인 것 같다. 사실 이 부분은 겪어보지 못해 이해가 잘 가지 않아 추후 공부 더 공부를 해야할 것 같다.  
![String.SubSequence](https://lh3.googleusercontent.com/agiUjtbRRrsOtxkjAFMKDvA3lB9DATz2GivZfL4Udmnoz74aCRs1HgHIivIfFdiP91yS9roPJXj4yqNvBhwqdfGbsKcUoQ1BXgIXqozFjE1XFK0ZtD9hbptBfZUJBGpho3lOeQhDObvGeGJDV68CBzKml6dLf3UTzSkAMK1XmvH_yc_afhO9K3glBHTkOKoVQGEWjkcYmVX0LHPbzxxd-2puuV2ez05Z3_7s3i1cZ032sEa3Vz0ybbv-JqiheMcnzmfMxOlMLW-A-Ic6RcABeHS4S_2Bu2DCCz08m5Jsosf_DM4ghk2AUadEY1IK0xgGXQPAOONZbNypeDh2EKspfQ6ZzPZhiV_oqkH-Hk6Qb_YGnwOt-RFeoLn6iwcqrgR8rq4b8bKwSf13zr8nGrLz4l6_j9PNNfG5SUxJkH0ock__cLsaZBxluysKuRAvhj5BBzZIia9n9kis50Gqo5IlqHU77GiiY634aWHdyUmuoUgRooKKE2yE-KZPSJHhRwF7f0cs8qHx9x47dMlHkTeDuv2PxiT0BnOghGdPUS-Ssl4IfzhJct1VnD_JMR0pKIQeTzI6Rb_c1B4KIV98KXl8NvIVTAIbsCre5Eu8Beo2dT9IZRQ34ocHDRlWoI8gIpFLuKxZ6HLC109cuo6YgedIMMtc=w1508-h336-no)

### 공백이 있는 문자열 Int 타입으로 입력 받기.

위에서 공백이 있는 문자열을 입력받는 방법에 대해 알아보았다. 하지만 readLine()을 통해 입력받은 문자열은 [String] 타입으로만 저장된다. 이를 다른 타입으로 저장하려면 어떻게 해야할까?

기본 형변환처럼 ~~Int(readLine()!)~~ ?? 여러 방법을 해보면 알겠지만.. 저런식으로는 [String]타입을 형변환 시킬 수가 없다. 그렇다면 for문을 돌려 일일이 변환시켜야 할까..? 물론 그렇게도 할 수 있겠지만.. 그게 최선인가...

**split 함수에 map을 사용해서 해결할 수 있다.**

~~~ swift
if let input = readLine() {
	let a = input.split(separator: " ").map{Int($0)}
}
~~~

`$0` 은 split을 통해 나뉘어진 배열의 각 요소 요소를 뜻한다. **이를 응용하면 단순히 타입 변환뿐만 아니라 여러 계산도 가능하다.**



> 공부하며 배운 내용을 정리하고 있습니다. 잘못된 부분이 있을 수 있으니 문제가 있는 부분은 댓글을 통해 지적해주시면 감사하겠습니다. 