---
layout: post
title: Algorithm-BurteForce
date: 2019-02-28
excerpt: "완전탐색 Brute Force"
tag:
- swift
- Algorithm
- BOJ
- 문자열 처리
comments: true
---

# 완전탐색(Brute-force Search)

완전 탐색, 말 그대로 가능한 경우를 일일이 다 탐색해보는 방법이다. 절대 틀릴 일은 없지만 시간은 최대로 들어가는 방법이다. 이런 문제들은 문제를 그대로 코드로 옮겨서 해결하는 연습이 필요하다. 따로 개념보다는 여러 문제를 풀어봐야 할 것 같다. 

바로 문제를 풀어보자!  
[BOJ_2309: 일곱난쟁이](https://www.acmicpc.net/problem/2309)

![BOJ_2309_일곱난쟁이](https://lh3.googleusercontent.com/bevWPMFNpciwn6aIhQ2_g37td0esaZM1ySxItnUhud-sMBdIXgCQC5U7vazMME_JhugjlMfa3QA-JzVGTJExsGSQ6uOcQpT47jKAtcGjc44e3EVHQR_SO-5Nh4jDeJuIk0U34WddJHrK_4GiIB9mY1DdZDH27IwUk8JCMilGQW4EmGheZdHCYvrtLsTmchE98KN2ctvLyOP6DKYZW-N1bqU9U2R9th9_0Mz0fibDMYTScMFH3z36uJxMCJbzKMpRIcWc-sB_i9_3mJ7SBwQZ7QafWZQfx5qwzuUjcehlcTES_w4l5itComDW2Q8GFBLuda4UevZZYEwkM8j0CLW4Cqh9GGFfVYUNSEsNFUYPGplMpvcqVqN9YzvVnGJaVyiIsigLKbh0_MpQK59E-tWW21xnN9dms0OyYNa8-5rgASDvP-HSKc2ACSSDhx18YsrzjhyF_L-KLa78knS3FES74-iEd48gKwGEJTmd63iVj2_ZkR-B_3_7Bws4hEFTx2HBBxuj-ExnpfUOgm0-EpMY1dtn2JgH4xr01xNEUnIn4eeFi2sVbUFTf21XB-5tQ0Z4YIvgJ-fQ69pS9vbxqojP0RO6iHGTCionL9lw0vqTqctRSU8vSBVanTXLwXEjY-PWdB6w--ZBY4Ijc1APexNvF1iTYbciRoM=w838-h657-no)

9명의 난쟁이 중에서 진짜가 아닌 2명만 찾아내면 되는 문제이므로 9c2 = 36가지의 경우밖에 되지 않는다. 따라서 이런 경우에 완전 탐색으로 풀면된다.

 <details><summary>CLICK ME</summary>
 <p>
 
```c++	
#include <iostream>
#include <algorithm>
using namespace std;

int main(int argc, const char * argv[]) {

int testCase = 9;
int talls[9];
int total = 0;
int noDwarf1 = 0;
int noDwarf2 = 0;

for(int i=0; i<testCase; i++){
	scanf("%d", talls + i);
	total += talls[i];
}

sort(talls, talls + 9);

for(int i=0; i < testCase-1; i++) {
	for(int j = i+1; j < testCase; j++) {
		if ((talls[i] + talls[j]) == (total - 100)){
			noDwarf1 = i;
			noDwarf2 = j;
		}
	}
}

for(int i=0; i< testCase; i++) {
	if ((i != noDwarf1) && (i != noDwarf2))
		printf("%d\n", talls[i]);
}

return  0;
}
```

</p>
</details>

> 생각은 쉽지만 구현하는 것이 생각보다 쉽지는 않았다.. 아직은 많이많이 부족하다..
> 아닌 경우를 구할 때, 변수를 하나 더 만들고 이상하게 시도해보았었는데, (talls[i] + talls[j]) == (total - 100) 이런 조건문은 기억해둬야겠다.
> (total - talls[i] - talls[j]) == 100 이런 표현도 가능하다. 

여러 문제를 풀며 연습해보자!

[BOJ_2231: 분해합](https://www.acmicpc.net/problem/2309)




참고  
https://kks227.blog.me/220769870195