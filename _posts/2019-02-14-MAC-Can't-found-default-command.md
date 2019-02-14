---
layout: post
title: MAC-Can't-found-default-command
date: 2019-01-29
excerpt: "ls, vi등 기본 명령어를 찾을 수 없을 때"
tag:
- MAC
comments: true
---

# ls, vi등 기본 명령어 찾을 수 없을 때


MAC 터미널을 사용하던 중 ls, vi, sudo등 기본 명령어를 실행시키지 못할 때가 있다. 필자의 경우 터미널에서 작업실행 중 중단 방법을 몰라 강제로 터미널을 종료하고 이 증상이 발생했다.

강제종료해서 생긴 문제인줄 알았으나 찾아보니 그런게 아니라 필자가 cuda를 설치하면서 경로를 설정했는데 그 경로로 인해 원래 내 계정의 경로를 제대로 읽지 못해서 발생하는 문제였다...

해결방법은
>sudo vi .bash_profile

로 배쉬 프로파일에 들어간뒤,

>export PATH=%PATH:/bin:/usr/local/bin:/usr/bin

를 추가해줘야 이후에도 위의 명령어를 입력하지 않고 제대로 사용할 수 있다.

단, 주의할 것은 필자의 경우 cuda를 설치하기 위해 새로운 경로를 export를 했는데 이 export 밑에 위의 경로를 지정해줘야 한다. 

디폴트 경로를 설정해두고 따로 뭔가 추가하는 방법이 있을 듯 한데.. 좀 더 공부한 뒤에 추후에 다시 포스팅 해야할 듯하다.




출처: [http://arcanelux.tistory.com/entry/vi-ls-ssh등-터미널에서-명령어를-찾을-수-없을-때](http://arcanelux.tistory.com/entry/vi-ls-ssh%EB%93%B1-%ED%84%B0%EB%AF%B8%EB%84%90%EC%97%90%EC%84%9C-%EB%AA%85%EB%A0%B9%EC%96%B4%EB%A5%BC-%EC%B0%BE%EC%9D%84-%EC%88%98-%EC%97%86%EC%9D%84-%EB%95%8C)