---
layout: post
title: Swift - LifeCycle
date: 2019-01-14
excerpt: "LifeCycle on swift"
tag:
- ios
- swift
comments: true
---

# [Swift] LifeCycle

**viewDidLoad**
일반적으로 초기화 하기에 가장 좋은 메서드. 모든 것이 준비되어있고 outlet도 연결돼서 바로 시작이 가능하다.
**_단 한번만 호출된다._**

**하지만 아직 경계(bounds)가 설정되지 않았기 때문에 기하와 관련된 설정은 하지 말아야 한다.** 
--> viewWillLayoutSubViews(), viewDIdLayoutSubViews() 에서 관리
{% highlight html %}
override func viewDidLoad() {
	super.viewDidLoad()
}
{% endhighlight %}


**viewWillAppear**
곧 뷰 컨트롤러의 뷰가 화면에 나타날 것. 화면에 보이지 않던 시간동안 발생한 일을 관리. 주로 최신작업을 해준다.
**_여러번 호출 가능_**

{% highlight html %}
override func viewWillAppear() {
	super.viewWillAppear()
}
{% endhighlight %}


**viewDidAppear**
뷰가 화면에 나타난 이후에 호출된다. 애니메이션 같은 작업을 하기에 좋다.
네트워크 작업과 같이 비용이 큰 작업을 하기에 적합하다. 이러한 네트워크 작업은 보통 백그라운드에서 실행한다. 
**절대 사용자 작업을 방해해서는 안된다.**
{% highlight html %}
override func viewDidAppear() {
	super.viewDidAppear()
}
{% endhighlight %}

**viewWillDisappear**
viewWillAppear에서 했던 작업을 그대로 되돌리기 적합하다. 
타이머를 시작했거나, 애니메이션을 시작했거나, GPS관찰을 시작했을 때 되돌리기 좋다.

{% highlight html %}
override func viewWillDisappear() {
	super.viewWillDisappear()
}
{% endhighlight %}

**viewDidDisappear**
MVC를 정리하기 좋다. 자주 쓰이지는 않는다.

{% highlight html %}
override func viewDidDisappear() {
	super.viewDidDisappear()
}
{% endhighlight %}

**viewWillLayoutSubViews(), viewDIdLayoutSubViews()** 

bounds를 설정하기 위한 메서드들, 하지만 autolayout덕에 보통의 경우엔 호출할 필요가 없다. 컨트롤러에서 관리가 필요할 경우에 사용.

생각보다 여러 경우에 호출될 수 있다. 경계의 변화에 대응하도록 구현할 때 적절히 사용해야 한다.