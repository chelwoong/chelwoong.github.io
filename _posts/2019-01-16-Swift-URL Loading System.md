---
layout: post
title: Swift - URL Loading System
date: 2019-01-16
excerpt: "Swift URL Loading system"
tag:
- ios
- swift
comments: true
---


## URL Loading System

서버와 통신하려고 할 때 `URLSeession` API를 사용한다. 하지만 공식문서에서는 이를 사용하기 전에 URL Loading System에 대해 먼저 보고 올 것을 권장한다. 

![URL](https://lh3.googleusercontent.com/ITlx0gzMDe8Q8a2VhXXXJA6NTHE9ojXHtOpsd00Hcrg54r9TEfWl0UWWhEzaIgpt7skc-YP0F05xyumGJHUUmewK-63IDGXrHf80Jr6sWriGw9R1Ba-LtVxhB9-Qfd3j-GuHClAU5Kg2kjoCLbDqBzOuHeSjjSa_no2RTb-P9bRlWmIVBJ1dHG28P1qpPo0XUWADkNsxARGH1nnxEDAeJKs1cpFVQ0kfKOtB_V2ZAqhvQTFYNFore0DTQDQHPiLrztN8rlNnIXxEVgONiC8xGJwc1y6YQ_jxCB2CqY1Km-FNiMYVkZ6cTLz04iQy4VmquspjmH1PWZZ0TaZVRnBG7AGo9pSkKfg5HJ1vygwSgOBt5vvzM7WO4VBDbqpobK7mD6Sfc1-LE6a6n0rEtbOSg8PjsV4zDnW1up7rZDgXdl9wphtFY-18Si0vT3Pv9KCV-c7vUYnJyhLVa5qZLNGzzoqAgzbpNEym_V2XTzM0n4zlAHR3ETNy-IOU5S1uariLBb8t_Yg53KeeWi7sOKxOqVNyDBZqZEQ2szpW_zXMoM3ThbC0GqLqBdvFfSRPgqevUtLculXXYOvEKmgDJM2E-wbrs4pxlOVbb-OgBhtDtYMgRP0Tm_pL0fE2akKpQH4UGc678d3NYPP1-WU6pmm_5RSK=w1242-h386-no)

### URL Loading System
URL Loading System은 https나 직접만든 표준 프로토콜을 사용해 URLs로 식별되는 자료에 접근할 수 있도록 해준다. Loading은 비동기적으로 처리되기 때문에 앱이 응답속도를 유지하면서 데이터나 오류를 처리할 수 있다. 

URLSession instance는 하나 또는 다수의 URLSessionTask instance를 가질 수 있는데, URLSessionTask instance는 앱에 대한 데이터, 다운로드 파일 또는 업로드 데이터나 remote의 파일등을 가져오고 리턴할 수 있다. 

Session을 관리하기 위해서 URLSessionConfiguration object를 사용해 캐시나 쿠키등을 컨트롤 할 수 있고 네트워크와 연결을 관리할 수 있다.

하나의 Session을 반복적으로 사용해 task를 만들 수 있다. 예를들어, 하나의 웹브라우저는 여러개의 분리된 세션들을 가질 수 있다. 

![creating tasks from URL sessions](https://lh3.googleusercontent.com/e_YqCdehbJIX5gxgTA8AaZWFUPoTqYcza1Y6Fb6fEEQ6Yg0BaOSUU1iEoD2oxf6Crzlsp0hXwl-bSuFgA7zqlWCFhyqF2yDHRXnw1h-3gsFggRjCasaLPPE9rzjqr2gqoLZtXrenDSiqts323ptcr_-1UcMgiUOMk-_InJ3rYElzretmvrp8rDAS0jsG5tp180YzJC9sYDSTcfqTIpK63MdRNfwMdwtAyzagORD7srlPtJPCMYNItBLxzKM0hOzoSmugk_n9cApZyc6rBg-wam9IjHTfpD5gS3ZtjVNdm6GnnxnHg1WEUciVUowenzKZKPmfsXdysOrJMDJpqMye8yvOl2TMF59JedBrWg6VQ8_PqmV2J3Uy5Hnrh4NN-PgoSLWQntU4gF4CsLA52MWZU1eBqHoa4LHQvRVS6sa2XmB4xc0QnNKh_jfN_AlxA30xxJ100Ly8AXtjOuJn21_Zo1ZG9WOGk-P8rCoExyf0JH9enaFj98yJnmMWaRGPEkTCTwcOTCVV1XS4NnjlbRt5d52zwxjRc5VYS5EY6xLW6UK1hMTKlWf18BJhFAwuJ7GfzMYMU1EzzpPxyDi_EHKUtV9yTQKy_YWcEj6gaZLKS-Eyg1N3-KJcGNP7fO6Pyhq2r5XbViWy2MC0Zb5GTl5PgVAv=w259-h125-no)

#### Session
Session은 크게 3가지가 있다.
- Deafult: 기본적인 디스크 기반의 Default session
- Ephemeral: 어떠한 데이터도 저장하지 않는 Ephemeral Session
- Background: 앱이 종료된 이후에도 통신이 이뤄지는 Background Session