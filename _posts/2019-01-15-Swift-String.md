---
layout: post
title: Swift - String
date: 2019-01-15
excerpt: "What is String on swift?"
tag:
- ios
- swift
comments: true
---

# String

>공부하면서 익힌 내용을 정리하고 있습니다. 아직 부족한 부분이나 잘못된 부분이 있을 수 있으니, 있다면 댓글로 피드백 부탁드립니다.
스탠포드의 [CS193p](https://www.edwith.org/swiftapp/joinLectures/13694) 강의를 참고해 작성하였습니다.

string은 unicode로 구성되어 있다. 유니코드는 전세계 모든 언어를 나타낼 수 있는데, 바이트 단위로 데이터를 나타낸다.

'cafe'라는 글자가 있을 때, 강세가 있냐 없냐에 따라서
4개의 유니코드 (c-a-f-e) or 5개의 유니코드 (c-a-f-e-')로 나타내질 수 있다. 따라서 이러한 차이로 인해 string은 Int 로 색인되지 않는다. 
유니코드는 대신 string.index를 사용한다. 

예를 들어보자,

~~~ swift
let pizzaJoint = "cafe(`) pesto"
let firstCharacterIndex = pizzaJoint.startIndex // String.index 타입이다.
let fourCharacterIndex = pizzaJoint.index(firstCharacterIndex, offsetBy: 3)
let forCharacter = pizzaJoint[fourCharacterIndex] // e(')

// "pesto" 를 얻어보자.
if let firstSpace = pizzaJoint.index(of: " ") {	// space가 없을 수도 있어서 if let을 사용
	let secondWordIndex = pizzaJoint.index(firstSpace, offsetBy: 1) 	// 두 번째 문장은 공백 바로 뒤 첫번째에서 시작!
	let secondWord = pizzaJoint[secondWordIndex..<pizzaJoint.endIndex] // 두 번째문장 처음부터 문장 끝까지! 
}

// "pesto"를 얻는 다른방법
// 단, 여기선 문장에서 공백이 하나일 때를 가정, 
// separatedBy에 지정한 문자를 기준으로 분리된 요소의 배열을 만들어준다.
// 다음은 공백을 기준으로 분리된 모든 단어들을 갖는다.
pizzaJoint.components(separatedBy: " ")[1]
~~~

**다른 String Method**
func hasPrefix(String) -> Bool

func hasSuffix(String) -> Bool

var localizedCapitalized/Lowercase/Uppercase: String

func replaceSubrange(Range<String.index>, with: collection with character)

~~~ swift
e.g. s.replaceSubrange(..<s.endIndex, with: "new contens")
~~~

다음 예처럼 범위의 한쪽을 생략하면 자동으로 처음 또는 끝의 인덱스를 넣어준다. 하지만 그 타입을 추측가능할 때만 사용할 수 있다.




