---
title: RxJS Quick Start, 책 정리 (71~109p)
date: 2019-03-08 01:52:47
categories:
    - RxJS
tags:
    - RxJS
---

## Chap3. RxJS가 해결하려고 했던 문제 3 : ***로직 오류***

### 1.1 웹 애플리케이션의 로직

- 웹 애플리케이션은 전달 받은 입력값을 로직을 통해 새로운 결과를 반환하거나 표현함
- 사용자 정보를 표현하는 UI를 작성하는 예제
  - 데이터를 추출하고 변환 하는 작업
    - 반복문
    - 분기문
    - 변수

### 1.2 로직의 복잡성 그리고 오류

- 반복문과 분기문, 변수는 코드의 복잡도를 높이고 가독성을 떨어트려 오류 발생 빈도를 높임

### 1.2.1 반복문과 분기문

- 로직의 복잡성 줄이는 방법
  - 기능별로 쪼개기
    - 기능을 추상화할 수 있음
      - 로직의 복잡성이 감소!

### 1.2.2 변수는 오류의 시작

- 브라우저 환경의 자바스크립트는 싱글 스레드 구조이기 때문에 멀티 스레드 사용으로 인한 동시성 문제는 발생하지 않음
- 하지만 DOM에 등록된 이벤트 핸들러에 의해 변수의 값이 변경될 수 있음
- 또는 비동기로 인해 변수의 값이 변경가능함

### 1.3 자바스크립트의 솔루션

- 함수형 프로그래밍!
  - 함수는 일급 객체임을 이용

### 1.3.1 로직의 분리

- 이전 예제에서 logic, makeHtml 함수 생성
  - 핵심 로직(process 함수)과 함수를 분리

### 1.3.2 반복문, 분기문, 그리고 변수와의 이별

- **고차함수 (higher-order function)**

  - 다른 함수를 인자로 받거나 그 결과로 함수를 반환하는 함수

  - 고차 함수는 변경되는 주요 부분을 함수로 제공

    - 이로인해 동일한 패턴 내에 존재하는 문제를 해결

  - 함수의 합성, 변형과 같은 작업을 쉽게 할수 있게 해줌

    - 커링(currying), 메모이제이션(memoization) 기법

  - ``` javascript
    const twice = (f, v) => f(f(v));
    const fn - v => v + 3;
    console.log(twice(fn, 7));  // 13
    ```

- 고차 함수를 이용한 process 함수 개선

  - if문 -> filter로 변환
  - map을 이용하여 값을 변환
  - reduce를 이용하여 축적된 데이터를 반환

- 순수함수

  - 같은 입력이 주어지면 항상 같은 출력을 반환하는 함수

-----

### 1.4 RxJS는 어떻게 개선하였나?

### 1.4.1 RxJS가 제공하는 오퍼레이터

- RxJS에서도 ES5의 고차함수와 같은 operator를 제공함 ([RxJS 공홈 참고](http://reactivex.io/rxjs/manual/overview.html#categories-of-operators))
- 오퍼레이터를 이용하면 Observable을 생성할 수도 있고, 전달된 데이터를 변환하거나 추출할 수 있음
  - Observable의 합성과 분리도 가능
  - 오퍼레이터를 많이 알면 좋지만, 이게 장벽이 될수도..
    - 오퍼레이터들은 함수형 프로그래밍에 근간

### 1.4.2 불변 객체 Observable

- RxJS의 오퍼레이터는 항상 새로운 Observable을 반환함
  - 이 Observable은 불변 객체임(immutable object)
    - 불변 객체 : 생성 후 상태를 바꿀 수 없는 객체
    - 불변 객체를 사용하면 프로그램의 복잡도가 줄어듬
- Array와 다른점
  - Array는 새로운 Array 객체 생성 작업만 함
  - Observable은 새로운 Observable을 만들고, 그 Observable이 오퍼레이터를 호출한 원래의 Observable을 내부적으로 subscribe 함
    - 즉, 링크드 리스트 형태로 기존 Observable 객체와 새롭게 만든 Observable 객체를 오퍼레이터로 연결함
    - 따라서 source 부터 전달된 데이터, 에러, 종료 여부가 Observable의 오퍼레이터들을 통해 전달되거나 변형되어 구독한 Observer에게 전달할 수 있음

## 부록2 : 함수형 프로그래밍(functional programming)

### 1.1 함수형 프로그래밍이란?

> 함수형 프로그래밍은 자료처리를 ***수학적 함수의 계산***으로 취급하고 ***상태 변경과 가변 데이터를 피하려는*** 프로그래밍 패러다임이다

### 1.2 수학적 함수의 계산

- 함수형 프로그래밍은 수학적인 계산을 이용하여 반복문이나 조건문과 같은 로직의 복잡성을 쉽게 풀고자 하는게 목적임

### 1.3 상태변경과 가변 데이터를 피하려는

- 함수형 프로그래밍의 또다른 목적은 상태 변경을 피하려는 것
- 변수를 모든 오류의 근본 원인으로 치부함

### 1.4 순수함수, 상태가 없다

- 순수함수?
  - 같은 입력이 주어지면, 항상 같은 출력을 반환
  - side effect를 발생시키지 않음
  - 외부의 가변(mutable) 데이터에 의존하지 않음

### 1.5 RxJS에 녹아있는 함수형 프로그래밍

- 상태를 어떻게 전파할건지에 대한 해결 -> 리엑티브 프로그래밍 패러다임
- 복잡한 문제를 외부 상태 변경 없이 효과적으로 해결 -> 함수형 프로그래밍 패러다임
  - RxJS의 Observable은 오퍼레이터를 제공
  - 이로 인해 생성된 Observable은 불변 객체(immutable object)를 반환
  - 오퍼레이터의 인자로 순수 함수를 받음으로써 부원인과 부작용 제거
  - 이로인해 코드는 동시성 문제에서 자유롭고, 테스트 또한 용이해지고, 로직 또한 단순해짐

-----

# 2부

## Chap 1. RxJS란 무엇인가?

### 1.1 RxJS란?

> Observable을 사용하여 비동기및 이벤트 기반 프로그램을 작성하기 위한 라이브러리

### 1.2 RxJS 시작하기

### 1.2.1 RxJS 첫번째 예제

- 페이지를 클릭시, event.currentTarget 정보를 콘솔로 출력해보자

  - 이벤트 핸들러를 만들고, 그 핸들러를 addEventListener에 등록

  - ``` javascript
    const eventHandler = event => {
        console.log(event.currentTarget);
    };
    document.addEventListener("click", eventHandler);
    ```

- 동일한 기능을 RxJS로 구현

  - 이벤트를 Observable로 변환하는 fromEvent 함수를 제공함

  - ``` javascript
    const { fromEvent } = rxjs;
    cosnt click$ = fromEvent(document, "click"); // observable
    const observer = event => {
        console.log(event.currentTarget);
    };
    click$.subscribe(observer);
    ```

  - 이벤트 핸들러 만드는 것과 같이 observer를 만듬

  - addEventListener를 통해 이벤트 핸들러를 등록하는것과 같이, observer를 Observable에 구독(subscribe)함

### 1.2.2 RxJS 첫번째 예제 개선하기

- 앞 예제에서 실제 필요한 정보는 click 때의 currentTarget 정보임

  > **pluck(properties: ...string): Observable**
  >
  > pluck은 '~을 뽑다'는 의미. 추출할 속성들을 '문자열'로 지정할 수 있음

- RxJS에서 오퍼레이터를 적용하기 위해 반드시 `pipe` 오퍼레이터를 통해 적용해야함

- pipe 오퍼레이터는 파라미터로 전달된 오퍼레이터들이 적용된 새로운 Observable 인스턴스를 반환함

- pipe 오퍼레이터는 Observable 인스턴스의 메소드로 존재함

  > **pipe(operations: …): Observable**
  >
  > 처리되어야 할 작업(operator)들을 순차적으로 받아서 처리함



- 도트체이닝 방식과 pipe 오퍼레이터 방식

  - 도트 체이닝(dot chaining)
    - 메소드 호출방식처럼 .을 찍어서 동작
    - 문제점
      - 도트 체이닝을 구성하기 위해선 Observable 객체가 모든 오퍼레이터를 가지고 있어야함
      - 불필요한 오퍼레이터를 모두 가지고 있어야 하기 때문에, 파일 사이즈가 증가됨
  - pipe 오퍼레이터 방식
    - 웹팩이나 rollup을 통해 트리셰이킹(사용하지 않는 모듈을 번들링할 때 제거하는 기능)이 가능
    - 함수형태로만 오퍼레이터가 만들어지므로 Observable과의 결합도를 떨어트려 쉽게 사용자 오퍼레이터를 작성 가능

- pluck 오퍼레이터를 이용하여 코드 리펙토링

  - ``` javascript
    const { fromEvent } = rxjs;
    const { pluck } = rxjs.operators;
    const currentTarget$ = fromEvent(document, "click")
    	.pipe(
        	pluck("currenttarget")
        );	// Observable
    const observer = currentTarget => {
        constsole.log(currentTarget);
    };
    currentTarget$.subscribe(observer);
    ```

  - click이 발생하면 currentTarget$은 event 객체의 currentTarget을 전달

  - observer는 currentTarget을 구독함으로써 해당 데이터를 전달 받을 수 있음

### 1.2.3 RxJS 두번째 예제

- 예제: 사용자 정보를 가지는 배열에서 '촉'나라 사람만 추출

  - ``` javascript
    const user = [{
        name: "유비",
        birthYear: 161,
        nationality: "촉"
    },{
        name: "손권",
        birthYear: 182,
        nationality: "오"
    },{
        name: "관우",
        birthYear: 160,
        nationality: "촉"
    },{
        name: "장비",
        birthYear: 168,
        nationality: "촉"
    },{
        name: "조조",
        birthYear: 155,
        nationality: "위"
    },{
        name: "손권",
        birthYear: 182,
        nationality: "오"
    }].filter(user => user.nationality === "촉");
    const log = user => console.log(user);
    users.forEach(log);
    ```

- 위 코드와 동일한 기능을 RxJS로 작성

  - from 메소드

    - Array를 Observable로 변환

  - ``` javascript
    const { from } = rxjs;
    const { filter } = rxjs.operators;

    const users$ = from([{
        name: "유비",
        birthYear: 161,
        nationality: "촉"
    },{
        name: "손권",
        birthYear: 182,
        nationality: "오"
    },{
        name: "관우",
        birthYear: 160,
        nationality: "촉"
    },{
        name: "장비",
        birthYear: 168,
        nationality: "촉"
    },{
        name: "조조",
        birthYear: 155,
        nationality: "위"
    },{
        name: "손권",
        birthYear: 182,
        nationality: "오"
    }]).pipe(
    	filter(user => user.nationality === "촉")
    )
    const observer = user => console.log(user);
    user$.subscribe(observer);
    ```

  - observer에서 로그 출력

  - forEach를 통해 log 함수를 호출하는 것같이, observer를 Observable에 subscribe함

  - Array 객체를 observable로 변화하고, pipe를 통해 filter 오퍼레이터 적용

    > 두 예제를 통한 결과: 비동기 방식, 동기 방식 모두 동일한 형태로 개발 가능하다!

### 1.3 RxJS 4대 천왕

- RxJS에서의 중요한 개념들
  - Observable
  - Operator
  - Observer
  - Subscription
  - Subject
  - Scheduler

### 1.3.1 Observable

> 시간을 축으로 연속적인 데이터를 저장하는 컬렉션을 표현한 객체

### 1.3.2 Operator

> Observable을 생성하고 조작하는 함수
>
> 오퍼레이터는 현재의 Observable 인스턴스를 기반으로 항상 새로운 Observable 인스턴스를 반환함

### 1.3.3 Observer

>  Observable에 의해 전달된 데이터를 소비하는 주체
>
> next, error, complete 함수를 가진 객체를 가리킴

### 1.3.4 Subscription

> Observable.prototype.subscribe의 반환값
>
> 자원의 해제를 담당 -> unsubscribe메소드를 통해

### 1.4 RxJS 개발 방법

1. 데이터 소스를 Observable로 변경
2. 오퍼레이터를 통해 데이터를 변경하거나 추출. 또는 여러 Observable을 하나의 Observable로 합치거나, 하나의 Observable을 여러개의 Observable로 만든다
3. 원하는 데이터를 받아 처리하는 observer 만들기
4. Observable의 subscribe를 통해 Observer를 등록
5. Observable 구독을 정지하고 자원을 해지

