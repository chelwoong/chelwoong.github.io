---
layout: post
title: Swift - TimeStamp를 이용해 시간 변환하기
date: 2019-01-15
excerpt: "TimeStamp를 이용해 시간 변환하기"
tag:
- ios
- swift
comments: true
---


### Timestamp를 사용해 시간 포멧을 변경해보자.

간단하다. 바로 코드부터 보자.

~~~ swift
func timeFormatter(timestamp: TimeInterval) -> String? {

	let dateFormatter = DateFormatter()

	dateFormatter.locale = Locale(identifier: "ko_KR")

	dateFormatter.dateFormat = "yyyy.MM.dd HH:mm"

	let date = Date(timeIntervalSince1970: timestamp)

	return dateFormatter.string(from: date)

}
~~~

timestamp는 1970년도를 기준으로 한 경과시간을 나타낸다. 
이를 변환해주는 ==DateFormatter()==를 생성하고
DateFormatter에 원하는 형식을 입력해주면 된다.
우선 지역을 입력한다. (한국 기준 "ko_KR") 
그리고 원하는 날짜 포멧 형태를 입력한다. (예제는 연도,월,일 시:분:초)
그리고 timestamp를 Date형식으로 변환시켜주면 된다.