---
layout: post
title: [Swift] guard vs if
date: 2019-01-14
excerpt: "when use to guard or if on swift"
tag:
- ios
- swift
comments: true
---

# When use to guard vs if

swift 개발에서 명심해야 할 사항이 하나 있다!
그건 바로 ! 강제 캐스팅 `!` 은 치명적인 오류를 낳을 수 있다는 것이다. **가급적 아니, 아예 강제 캐스팅은 사용하지 말자.**

그렇다면 숙명적으로 if 혹은 guard 또는 switch 구문을 사용해야 할 때가 온다. switch는 그렇다 치고 스위프트 초보인 나는 별 생각없이 if 혹은 guard를 사용하곤 했다. 아니 사실 처음에는 같은 것인데 후에 guard라는 구문이 추가되었구나 내키는대로 쓰면 되겠지. 라고 생각하기도 했었던 것 같다. 

하지만 공부를 좀 해보면, 여러 예제나 코드들을 보면 알다시피 어느 곳에서는 guard가, 어디서는 if가 사용된다.  

무슨 차이일까? 우선 그 차이부터 알아야 어디서 어떻게 써야할 지가 그려질 것이다.

내가 이해한 바로는
**if**는 단순히 특정 조건을 확인하는 방법으로, 없어도 상관 없을 때 사용하면 좋다.

**guard**는 특정 값이 반드시 있어야 할 경우에 사용해야 한다. 따라서 값이 없다면 어떻게 해야 할 지 정해줘야 한다. 

공식 문서에서 [Control transfer statements](https://docs.swift.org/swift-book/ReferenceManual/Statements.html) 로 불리우는 

- return
- brerak
- continue
- throw

등을 사용해서 말이다.  

이렇게 사용하는 것이 
> if는 ~ 상황 '이면' ... 해라
 guard는 ~ 상황이 '아니면' ... 해라

로 읽히기 때문에 가독성 측면에서도 좋다.

~~예를 들어보자,~~