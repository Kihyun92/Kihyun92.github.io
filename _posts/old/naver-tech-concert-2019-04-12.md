---
title: 네이버 테크 콘서트
date: 2019-04-12 10:55:37
tags:
    - FE 2019
    - frontend
    - 네이버 테크 콘서트
---

# 플랫폼 UI 개발 전략의 모든 것

[첫번째 세션](https://www.slideshare.net/NaverEngineering/naver-tech-concertfe2019-ui)으로 네이버에서 스마트에디터의 UI를 개발하신 이주용님께서 발표하셨습니다.

## 스마트 에디터 3.0 -> 스마트 에디터 원으로 변경하면서 느꼈던점에 대한 발표

### 1. 기존 설계의 문제점

-   커스텀 및 확장을 고려하지 않아, 서비스의 요구사항을ㄹ 수용하기 어려움
-   플랫폼의 CSS와 서비스의 CSS 간섭이 발생하고 스타일의 우선순위 관리가 어려움
-   에디터 UI의 요소간 관계를 파악하기 어려워 버그 및 사이드 이펙트 발생

### 2. 새로운 설계 방향

-   UI 공통화는 디자인 중심이 아닌, 기능 중심으로!
    -   구조를 먼저 파악해야함
-   조건 및 상태에 따라 다른 스타일 적용
    -   CSS 설계는 동적으로
-   각기 다른 요구사항을 빠르고 쉽게 적용해야함
    -   설정으로 분리하여 하나의 파일에서 모두 변경가능하도록

### 3. 구현과 문제 해결

#### CSS Methodology

-   Block, Element, Modifier (BEM)
-   Scalable and Modular Architecture for CSS
-   Object-Oriented CSS

#### CSS Preprocessor

-   CSS의 기능을 확장하여 선택자 상속, 변수, 조건문, 반복문, 함수 등 사용 가능
-   sass

### 4. 공통 요소의 분리

#### 플랫폼의 스펙 분석 전략

-   디자인 보다는 기능(구조) 중심의 분석
-   동일한 기능을 하는 요소는 동일한 HTML 구조를 가질 수 있을지 검토
-   공통화 요소 중 일부 UI가 다른 경우는 전체 스펙으로 구현 검토

### 정리

1. 모듈화

-   디자인보다 각 요소가 하는 기능에 집중하여 모듈화
-   현재의 요구사항에 맞게 최소한의 기능으로 모듈화 (확장성은 배제)
-   같은 기능의 요소는 동일한 HTML 구조를 사용

2. 설정과 공통 코드

-   간격, 색상, 서체, 폰트 사이즈 등 서비스 별로 변경이 필요한 것들은 설정으로 관리
-   css pre-processor를 활용하여 반복적인 코드 줄이기
-   연관된 UI나 수치는 공통적으로 묶어 관계를 명확히하기

3. 플랫폼은 만능이 아니다

-   모든 요구사항을 플랫폼의 공통 코드로 소화할 수 없음
-   따라서 때론 스펙 협의나 커뮤니케이션이 설계보다 중요할 수 있음
-   플랫폼의 공통코드는 **불변**이 아니며 지속적인 리펙토링이 필수

---

# 주니어 개발자의 성장에 대한 뻔하지만 뻔하지 않은 이야기

[두번째 세션](https://www.slideshare.net/NaverEngineering/naver-tech-concertfe2019-140435675)으로 LINE Financial Plus의 한재엽님 께서 발표하셨습니다.

## 성장의 종류

![](https://user-images.githubusercontent.com/35797540/56034194-9f758200-5d61-11e9-995c-fe440c281d12.jpg)

개발자의 성장 방향에는 크게 이 정도가 있을것 같음.

### 성장을 왜 해야하는지 생각해보기 (Why?)

> 나의 선택과 집중이 어느 방향에 집중되어야 할지

1. 성장해야하는 이유부터 정리
2. 어느쪽으로 성장하고 싶은지 조금 더 구체화하기

### 성장을 어떻게 해야할까? (How?)

해야할 것과 하고 싶은 것은 매우 많지만 우리의 하루는 24시간이다. 너무 짧다..

따라서 하루에 8시간 이상을 보내는 회사에서 성장해보자

## 회사에서 성장하기

### 업무를 **소비**하지 말자

-   이때 업무란?
    -   Production 레벨에서 코드를 작성하는 일
    -   그리고 구현한 코드에 책임을 지는 일
-   삽질에 대해서 다시 생각해보기
    -   버그를 눈 앞에서 치워버려야하는 것 이라고 생각하지 말기
    -   디버깅 (다양한 툴들, ex.크롬 개발자 도구, Charles, Fiddler, ...)
    -   문제 원인 파악 -> 학습 -> 문제 해결 시도 -> 문제 원인 파악 -> (반복...)
        -   최종적으로는 이 모든 경험들이 **노하우**가 된다. 이 노하우들이 쌓이면 전문성이 갖춰진다.
    -   삽질을 통해 배우고, *정리*하자!

### 질문을 '잘' 하자

> 바보같은 질문은 없어도 성의없는 질문은 있다.

-   배울점이 많은 동료들에게 많이 배워보자
-   하지만 동료의 시간을 낭비하면 안된다! -> 질문을 잘! 해야한다.

잘 질문 하려면?

1. 충분한 구글링을 선행
2. 질문을 정리하자
   2-1. 현재 발생한 **상황** 정리
   2-2. 내가 해본 **시도**들을 정리
   2-3. 최종적으로 Yes/No로 답이 오도록 정리
   2-4. 혹은 내 결론에 대한 의견을 답할 수 있도록 정리

### 문서화를 '잘' 하자

트러블 슈팅 목록으로 나눠서 정리 ([오픈소스들의 이슈 템플릿](https://github.com/angular/angular/issues/new/choose)을 참조해보자!)

-   **어쩌다**가 버그가 발생했나?
-   **원인**은 무엇인가?
-   어떤 **시도**들을 해보았나?
-   그래서 최종적으로 어떻게 해결했나?

### 문서 쓸 시간이 없다면?

문서화를 개발 프로세스의 일부분으로 생각하고 개발 기간을 잡자!
그리고 잘 정리한 문서를 **공유** 하자!!

## 팀의 생산성을 높이기

### 개발 환경의 중요성

-   개선하기
-   환경을 알기
-   자동화의 중요성
-   관성에 젖지 않는 비판적인 사고하기

### 변화 무쌍한 스펙 변경에 맞서기

-   초기에 결정된 스펙은 무조건 변경된다고 생각하기
-   어떻게 대응할지 생각하기
-   변경될 수 있는 요소들을 어떻게 제어해야할지

---

# 일 만드는 개발자 VS 일 부풀리는 개발자

[세번째 세션](https://www.slideshare.net/NaverEngineering/naver-tech-concertfe2019-vs)으로 우아한 형제들의 김민태 프로그래머님의 발표입니다.

## '일' 에 대해 정의해보기

사람과 태도, 전문성, 에너지, 등등

## 출발점은 Requirement!

### 요구사항은 어디까지 수용해야하나?

-   먼저 직업인과 직장인에 대해 생각해보자
    > "나는 주니어니까..." 라는 생각은 하지말자.
-   상사와 제품에 대해 생각해보자
    > 제품이 모든것의 중심이 되어야 하지 않을까?
-   습관은 관성이 된다.

요구사항을 분석하고, 계획하고, 실행하고, 측정하고, 보정하고, 다시 분석하고 이런 반복적인 과정에서 예외사항이 발생할때는 바로 사람 때문이 대부분이다.

### 커뮤니케이션이 중요하다.

### 동료를 위한 개발

### 고객을 위한 개발

---

# 빠르게 훑어보는 웹 개발 트렌드

[네번째 강의](https://www.slideshare.net/NaverEngineering/naver-tech-concertfe2019)로 카카오뱅크의 한장현님이 발표하셨습니다.

약간 좀 뻔한 내용,,
[2019 Front-end Developer's Roadmap](https://github.com/kamranahmedse/developer-roadmap)을 기반으로한 발표였다.

### 웹개발 트랜드

서버 중심 -> 클라이언트 중심

---

# 데이터 상태 관리. 그것을 알려주마!

[다섯번째 강의](https://www.slideshare.net/NaverEngineering/naver-tech-concertfe2019-140432157)로 네이버 PWE의 최현철님이 발표하셨습니다.

## FE에서 상태관리란 무엇일까?

## SPA에서 상태관리란 무엇일까?

> 상태라는 눈에 보이지 않는 부분이 실시간 비동기적으로 변하기때문에 제어하기 힘들다.

---

# 오늘부터 나도 FE 성능 분석가

[마지막 강의](https://www.slideshare.net/NaverEngineering/naver-tech-concertfe2019-fe)로 네이버 아폴로 FE의 손찬욱님이 발표하셨습니다.
개인적으로는 이번 컨퍼런스에서 가장 유익한 강의였습니다.

## 성능 분석가의 관심사(Goal)은 무엇일까?

> 유저 입력시에 얼마나 빠르게 반응할 수 있나?

### LAI (Loading and Interation)

## 어떻게 성능을 올릴까? (Plan)

1. 대상을 선정. _숲을 보기!_
    - 어떤게 중요한 포인트인지 파악하기
2. 개선 프로세스
    - 측정
    - 분석
    - 최적화
    - 측정 ...(반복)
3. 언제까지?
    - 목표하는 초기 로딩 시간에 맞게
    - 구글의 경우 [RAIL](https://developers.google.com/web/fundamentals/performance/rail?hl=ko), [FMP](https://developers.google.com/web/tools/lighthouse/audits/first-meaningful-paint)

## 초기 로딩 속도 개선하기

-   Waterfall 차트
    -   높이 줄이기
    -   폭 줄이기
    -   간격 땡기기

### 1. 높이 줄이기

    - Data URI -> HTML에 Default 이미지 같은 이미지를 포함
    - Lazy
    - 이미지 (캐러셀의 경우 보여지는 곳만 먼저 로딩)

### 2. 폭 줄이기

    - Initial connection
        - HTTP 2.0으로 바꾸면 좋다(멀티 커넥션이 가능해짐)
    - TTFB (Time To First Byte)
        - 서버나 비즈니스 로직이 느린걸 체크할 수 있음
    - Content download (네트워크 속도 등 여러 요인이 있지만)
    - [GZIP](https://ko.wikipedia.org/wiki/Gzip), [Minify](https://www.minifier.org/)(이걸 말한건지 정확하진 않음..), [Obfuscation](https://en.wikipedia.org/wiki/Obfuscation_(software))
    - 이미지 줄이기
    - Decode 비용 줄이기 (이미지 화면에 렌더링하는 비용)

### 3. 간격 땡기기 -> 잘하기 위해선 [브라우져 렌더링 과정](https://d2.naver.com/helloworld/59361)을 잘 알아야함

    <img width="649" alt="브라우저 렌더링 과정 (출처:네이버D2)" src="https://user-images.githubusercontent.com/35797540/56470210-a6497680-647e-11e9-9db6-229eddd3083b.png">

1. 서버로부터 HTML 문자열을 Stream으로 받음
2. `<head>` 태그의 자원을 병렬로 받음
3. 2번에서 받은 자원을 모두 실행
4. `<body>` 태그부터 화면을 그리기 시작

-   head 태그엔 css와 필수 JS만 넣기
-   JS는 body 태그 마지막에 넣기
    -   async, defer를 사용해서 원하는 위치에 넣어도 됨(but 지원하지 않는 브라우저가 존재함)
    -   async -> 의존성이 없는 경우(GA)
    -   defer -> DOM 제어와 관련이 있을때
-   preload
    -   css 내에 폰트, 이미지를 미리 css와 함께 부름
-   HTTP2 Server Push
    -   HTML, Javascript, CSS, Img 같이 받음

### 4. 총체적으로 점검하기

-   FP(Fisrt Paint) -> head 태그 종료 후 이루어짐
-   FMP(First Meaningful Paint) -> **_hero element!_** -> 이걸 어떤걸로 정할지가 중요함! (Lazy하게 처리하면 안되는 요소들)
-   TTI([Time To Interactive](https://developers.google.com/web/tools/lighthouse/audits/time-to-interactive))
-   결국, 전체적으로 균형감 있게 줄여주는게 중요하다

## Part 2.

### Case by Case

-   브라우져 메인 스레드를 괴롭히지 않아야함!

### Javascript가 DOM을 만지면 메인 스레드가 Rendering Pipeline 과정을 거친다

-   Rendering Pipeline 과정

1. Javascript가 건들면
2. Style recalculation
3. Layout
4. Paint
5. Composite (cpu가 아닌 gpu의 도움을 받음)
    - 레이어를 겹쳐서 그리는 작업 (따라서 레이어를 어떻게 만드느냐가 중요함. 꼭 필요한 부분만 만들어야한다.)

[csstriggers.com 참조](https://csstriggers.com/)
