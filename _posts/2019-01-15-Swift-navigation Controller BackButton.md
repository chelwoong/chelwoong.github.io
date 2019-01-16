---
layout: post
title: Swift - navigation Controller BackButton 수정하기
date: 2019-01-15
excerpt: "navigation Controller BackButton 수정하기"
tag:
- ios
- swift
comments: true
---

## navigation Controller BackButton 수정하기

navigationController에서 navigation bar의 ==`< Title`== 을 수정하고 싶을 때가 있다. 

![backbuttonTitle](https://lh3.googleusercontent.com/1Q5XtayaKOHr5V8pukvQlpdobUjkiMJuwta3trQWkAm-TI2uM27DpW5iMp7FtmzKNfwHKNSZujQJ_2iSTRA7Pq0SFeEKjVJ4F16ODgEX8mgSW7jX6qiXkximexOJJIraKsQFiVmUB3zEQhlQUDHAmOPJi-n6U4utUty4L9ZvJxp-f4fn1RuEpO3ehn80eUFt-0aqO3YSZcXAbSoT3s_kWYKB9InZioXSIP26yplhExfaBzyZTSWLUTYJ1tyV3vbDCH5tLeX1F7Htc5hAazvq42kjDCrhtB2TIcXClVs3_Mn6CaWmR0ptSu1-0NsyPcuFYSIEqpoJtANVuD6G93gQwbEp9N56SOMpBYx3G-RTKR9cDDAeqP0jjOkkSKL5XhHMoMBA_RMWIlrVdqjJkpoKUhGGkgyzbdPnvZXry8IT06kZCD6X2WUwPS8fIdyGUrteDZNPVrpgn-n6J5lXiZ_lLXsSJ5pnyQkqmoN6aKztC4spuUR24RYMfKyzu7-NrLAR8MzEfoFFdPHfTScF2LEgwULN7w5JhXCcg9BjhlUyzuQE_UotSD4bUecx-VIxu9MvcrdDeV_r_omXJtz00qF4BwTB25_UY2A0VzE5tNIh4yg6442Ig-0u2KH_bnEKEaORgTEbXJYIfQpQhZj--wHHlf-h=w444-h146-no)

구글링을 해보면

~~~ swift
let backItem = UIBarButtonItem()
backItem.title =` `"Back"
navigationItem.backBarButtonItem = backItem
~~~

~~~ swift
navigationItem.backButton?.title = ""
~~~

등등 여러 방법들이 나오지만 . . . . 

~~무슨짓을 해도 수정되지 않는다.~~

**왜냐하면 navigation controller에서 backbutton은 현재 컨트롤러가 아니라 이전 컨트롤러기 때문에 segue를 전달하기 전에 수정을 해줘야 한다!!**

따라서 **prepare에서** ==backBarButtonItem==을 수정해주면 된다!!!

~~~ swift
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
	let nxetVC = segue.destination

	let backItem = UIBarButtonItem()
	backItem.title = "nextBackTitle!!!"
	navigationItem.backBarButtonItem = backItem
}
~~~


