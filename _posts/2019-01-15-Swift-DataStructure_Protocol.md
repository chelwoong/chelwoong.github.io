---
layout: post
title: Swift - DataStructure_Protocol
date: 2019-01-15
excerpt: "Swift 자료구조: Protocol"
tag:
- ios
- swift
comments: true
---


# Protocol

>공부하면서 익힌 내용을 정리하고 있습니다. 아직 부족한 부분이나 잘못된 부분이 있을 수 있으니, 있다면 댓글로 피드백 부탁드립니다.
스탠포드의 [CS193p](https://www.edwith.org/swiftapp/joinLectures/13694) 강의를 참고해 작성하였습니다.

Swift 자료구조의 4가지 기둥 중 하나인 Protocol을 알아보자.  swift 실행 시 굉장히 많이 사용되기 때문에 중요하다.

**Protocol이란 API에서 원하는 것을 불러오는 방식이다.** 
어떤 구조체든 열거형이든 클래스든 원하는 모든 것을 불러오고 어떤 것이든 전달할 수 있다. 그걸 받는 메소드는 원하는 것이 무엇인지 나타낼 수 있다. 즉, 호출자와 피호출자 양쪽 모두를 만족시키는 것이다. 

이는 프로토콜이 변수와 함수의 리스트이기 때문이다. 프로토콜은 어떤 구현이 아니라 단순한 리스트다. 

**프로토콜은 왜 좋을까?**

프로토콜은 API를 매우 유연하고 더 잘 이해할 수 있도록 만든다. MVC와 같은 블라인드 커뮤니케이션 구조에 매우 효과적이다. 



