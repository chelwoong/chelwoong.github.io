---
layout: post
title: JavaScript - Full Calendar
date: 2019-01-16
excerpt: "Full Calendar 정복하기"
tag:
- Web
- Javascript
- 
comments: true
---

# Full Calendar 를 정복하자
캘린더가 필요해서 직접 만들까 가져다쓸까 여러가지 시행착오 끝에 역시 가장 유명하고 멋드러진(?) Full Calendar를 사용하기로 마음먹었다. 

영어도 부족하고 경험도 부족한 탓에.. 항상 새로운 API를 더디고 어렵다.. 
부족하지만 하나하나 배운 것을 기록해보도록 하자

## Install 

공식 [DOC](https://fullcalendar.io/docs/installation) 에 보면 설치하는 방법이 잘 나와있다.
방법은 Script Tag 와 Module 사용, 두 가지가 나와있다. 모듈사용은 웹팩 등을 사용해야 하는 것 같은데 필자는 간단하게 Script tag를 사용하기로 했다. 
홈페이지의 [downloads page](https://fullcalendar.io/download) 에서 캘린더 Zip을 다운받고, 
jquery 와 Moment.js를 설치한다. 

**jquery 설치**
~~~ javascript
npm install jquery
or
yan add jquery
~~~
**Moment 설치**
~~~ javascript
	npm install moment --save   # npm
	yarn add moment             # Yarn
	Install-Package Moment.js   # NuGet
	spm install moment --save   # spm
	meteor add momentjs:moment  # meteor
	bower install moment --save # bower (deprecated)
~~~
## Loading the Code
설치가 다 끝났으면 다운받은 Zip파일의 lib폴더와 fullcalendar.js 파일, fullcalendar.css 파일을 내 프로젝트로 가져온다.
필자는 js파일은 /js, css파일은 /css 폴더에 저장했다.

이제 코드를 만져보자. 
html의 header 에  다음의 코드를 넣는다.
~~~ javascript
<link  rel='stylesheet'  href='fullcalendar/fullcalendar.css'  />  
<script src='lib/jquery.min.js'></script>  <script src='lib/moment.min.js'></script>  
<script src='fullcalendar/fullcalendar.js'></script>
~~~

그리고 sciprt에 다음의 함수를 하나 추가해준다.
~~~ javascript
<script>
$(function () {
// page is now ready, initialize the calendar...
	$('#calendar').fullCalendar({
		// put your options and callbacks here
	})
});

</script>
~~~

그리고 body에 id "calendar"를 가진 div를 하나 만들어준다.
~~~ javascript
<div  id="calendar"> </div>
~~~
여기까지 했으면 기본 캘린더가 하나 탄생한다!

![
](https://lh3.googleusercontent.com/INEgaoPBIBvag-QEHvAj5s-2i_UueehQGHj6cABGVYVuvxvHmgX-xu9qnMEdLQtsR19tDSCve3A "기본캘린더")

html 파일은 다음과 같이 되겠다.

**index.html**
~~~ javascript
<!DOCTYPE  html>
<html>
<head>
	<link  rel='stylesheet'  href='css/fullcalendar.css'  />
	<script  src='lib/jquery.min.js'></script>
	<script  src='lib/moment.min.js'></script>
	<script  src='js/fullcalendar.js'></script>
	<script>
		$(function () {
			// page is now ready, initialize the calendar...
			$('#calendar').fullCalendar({
				// put your options and callbacks here
			})
		});
	</script>
</head>

<body>
	<div  id="calendar">
	</div>
</body>
</html>
~~~

## Handlers
이제 만들어진 달력을 내 마음대로 가지고 놀아보자 
Docs의 Handlers는 달력의 여러가지 옵션들의 모음이라고 한다. 
	

### Option Tips

**get Calendar**
우선 달력에 여러 작업을 하기 위해서 달력을 가져올 줄 알아야 한다.
아래의 모든 예제들은 이 쿼리안에 넣어서 실행한다.
~~~ javascript
$('#calendar').fuulCalendar({
	// 여기다 옵션들을 넣는다.
})
~~~

**이벤트 넣기**
이제 달력을 가져왔으면 그 안에 옵션들을 채워넣자.  
- 이벤트를 기록하기 위해서는 eventSources: [ ]
- 클릭시 이벤트를 효과를 주려면 eventClick: function()


~~~ javascript
$('#calendar').fuulCalendar({
	eventSources:[
		events:[
			{
				title: Hello Calendar,
				start: 2018-09-96,
				end: ~~
				// start만 입력하면 그날만 기록된다.
			},
			color: 'yellow', // 기타 옵션들
			textColor: 'black',
		]
	],

	eventClick: (event, element) => {
		// click시 title을 CLICKED!로 바꿈
		event.title = "CLICKED!";
		$('#calendar').fullCalendar('updateEvent',event);	// 이 구문을 꼭 넣어야 실행됨		
})
~~~

**클릭시 이벤트**

alert box, 해당 날짜 클릭시 alert
~~~ javascript
dayClick:  function () {
	alert('a day has been clicked!');
}
~~~
클릭시 event1이라는 이벤트 주기
~~~ javascript
var  calendar  =  $('#calendar').fullCalendar('getCalendar');
calendar.on('dayClick', function (date, jsEvent, view) {
	$('#calendar').fullCalendar('addEventSource',
		[
			{
				title:  'event1',
				start:  date.format()
			}
		],
	)
})
~~~



**디자인**
View 모습 변환 header 생성 : 월, 주간, 일 별 전환
~~~ javascript
header: { center:  'month,agendaWeek' }, // buttons for switching between 
views: {
	month: { // name of view
		titleFormat:  'YYYY, MM, DD'
		// other view-specific options here
	}
}
~~~
반응형 디자인, 
windowsize가 일정 크기 이하면 일별달력으로 전환
~~~ javascript
windowResize:  function (view) {
	if ($(window).width() <  514) {
		$('#calendar').fullCalendar('changeView', 'basicDay');
	} else {
		$('#calendar').fullCalendar('changeView', 'month');
	}
},
~~~
