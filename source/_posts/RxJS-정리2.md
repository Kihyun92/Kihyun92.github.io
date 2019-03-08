---
title: RxJS Quick Start, 책 정리 (35~69p)
date: 2019-03-08 01:52:47
categories:
    - RxJS
tags:
    - RxJS
---

## Chap1. RxJS가 해결하려 했던 문제 1 : 입력 데이터의 오류

### 1.1 웹 애플리케이션의 입력 데이터

- 데이터 흐름의 관점
  - 서버 / 브라우저 / 브라우저 UI 객체 간에 데이터 이동
- State machine 관점
  - 동기 / 비동기 처리

### 1.2 입력 데이터의 전달 시점이 다양하다

### 1.2.1 동기

- 장점: 순차적으로 진행되므로 개발이 쉽다
- 단점: 웹브라우저와 같이 단일 UI 스레드를 사용할 경우, 해당 작업이 끝날때까지 브라우저는 대기해야함

### 1.2.2 비동기

- 호출하는 함수가 호출되는 함수의 작업 완료를 기다리지 않고 그 다음을 진행함
  - 호출되는 함수의 작업이 완료되면 별도의 **이벤트나 콜백 함수**를 통해 결과를 전달함
- 장점: 효율적인 작업 진행이 가능
- 단점: 개발은 더욱 복잡해지고, 오류 확률이 높아짐

### 1.3 동기와 비동기를 함께 사용할 수 밖에 없나?

- 단일 스레드 기반의 브라우저 환경에서는 비동기 방식을 사용하지 않으면 특정 작업이 프로세스를 독점하기 때문에 성능상 문제가 발생함
- 어쩔수없음

### 1.4 RxJS는 어떻게 개선했나?

- 입력 데이터에 대한 구조적인 문제를 개선하고자 했음
  - 구조의 일원화 -> 개발을 단순화
- RxJS는 동기와 비동기의 차이점을 **시간**이라는 개념을 도입함으로써 해결하려함
  - 동기와 비동기는 시간의 축으로 봤을때, 같은 형태이다! => **스트림** 이라 표현함
- RxJS에서는 이런 스트림을 표현하는 Obsevable 클래스를 제공함

### 1.4.1 Observable

>  시간을 인덱스로 둔 컬렉션을 추상화한 클래스

- 동기나 비동기의 동작 방식으로 전달된 데이터를 하나의 컬렉션으로 바라볼 수 있게 해줌
  - 개발자는 데이터가 어떤 형태로 전달되는지에 대해 고민할 필요 없음
  - 단지 Observable을 통해 데이터를 전달 받으면 됨

### 1.4.2 모든 데이터는 Observable 인스턴스로 만들 수 있다.

* Observable은 모든 데이터를 다룬다

  * 동기든 비동기든 모든 데이터 타입을 동일한 형태로 사용

* `event`를 Observable로 만들 때는 `fromEvent` 를 이용

  * ``` javascript
    fromEvent(HTMLElement, "이벤트 타입");
    ```

  * Example

    ``` javascript
    const { fromEvent } = rxjs;
    const key$ = fromEvent(document, "keydown");
    const click$ = fromEvent(document, "click");
    ```

* 배열 같은 `iterable`이나 `array-like`,` Promise 데이터` 를 Observable로 만들 때는 `from`을 이용

  * ``` javascrip
    from(Iterable | Array-like | Promise);
    ```

  * Example

  * ``` javascript
    const { from } = rxjs;
    const arrayFrom$ = from([10, 20, 30]);
    const iterableFrom$ = from(new Map([1, 2], [2, 4], [4, 8]));
    const ajaxPromiseFrom$ = from(fetch("./api/some.json"));
    ```

* 단일 데이터를 연속으로 전달할 경우엔 `of` 를 이용

  * ``` javascript
    of(...items);
    ```

  * Example

  * ``` javascript
    const { of } = rxjs;
    const numberOf$ = of(10, 20, 30);
    const stringOf$ = of("a", "b", "c");
    ```

> Observable 객체의 변수명은 관용적으로 접미사로 $(Stream의 S와 유사해서라고함) 를 붙인다.

----

## Chap2. RxJS가 해결하려고 했던 문제 2 : 상태 전파(State Propagation) 문제

### 1.1 웹 애플리케이션의 상태

- 웹 애플리케이션은 하나의 큰 상태머신
  - 이를 구성하고 있는 크고 작은 단위들 또한 하나의 상태머신임
    - 각각의 상태머신들은 각자의 상태를 가지고있음
    - 상태 머신들은 각자의 역할에 따라 서로 유기적으로 연결됨
    - 각 모듈간에 의존성이 있음

### 1.2 웹 애플리케이션의 상태 변화로 인한 문제점

- System과 User의 관계에 따른 상태 변화 예제

### 1.2.1 첫째, User의 인터페이스가 변겨오디면 System도 함께 변경되어야함

### 1.2.2 둘쨰, User의 상태를 확인하기 위한 인터페이스에 대한 의사소통 비용이 발생함

- User의 인터페이스가 늘어난다면, 다른 User와의 의존 관계에 있는 클래스 간에 의사소통 비용이 발생

### 1.2.3 셋째, 다수의 클래스가 User에 의존관계가 있는 경우라면 User의 변경 여부를 반영하기 위해 다수의 클래스들이 직접 User의 상태를 모두 반영해야함

-----

### 1.3 우리가 이미 알고 있는 솔루션 - 옵저버 패턴

### 1.3.1 Loosely Coupling

- 옵저버 패턴에서는 상태가 변경될 대상을 `Subject` 라고 함
- 그 상태 변화를 관찰하는 대상을 `Observer` 라고 함
- 옵저버 패턴에서는 Subject와 Observer가 서로 느슨하게 연결(Loosely coupling)되어있음
  - 서로 상호작용을 하지만, 서로 잘 모른다는 뜻

### 1.3.2 자동 상태 전파

* Subject로 부터 데이터를 제공 받음 -> push 방식
  * Subject와 Observer가 1:n의 상황에서 더욱 효과적
  * 데이터 변경 시점을 매번 확인할 필요 없이, 변경되었다는 신호가오면 처리

### 1.3.3 인터페이스의 단일화

- 인터페이스가있다는 것은 많은 비용을 수반함
  - 인터페이스가 있어도 없게 만들면 됨
    - 인터페이스를 특정 몇개로 통일
- Observer pattern은 `Observer.update` 만 존재하기 때문에, Subject에서는 Observer인터페이스에 대한 별도의 비용이 존재하지 않음

-----

### 1.4 옵저버 패턴의 흔한 예

- 뉴스를 발행하는 신문사(subject)와 이를 구독하는 고객(observer)의 경우

  - 신문사는 고객을 등록하고, 신문이 발행될 때 각각의 고객에게 신문이 발행되었다고 알려줌(notify)
  - 신문이 발행되면 어떤 고객은 뉴스를 읽거나 스크랩함

  - subject => add, remove, notify
  - observer => update

-----

### 1.5 옵저버 패턴적용하기

- 기존 예제에 적용, user와 system의 의존성을 느슨하게함

-----

### 1.6 RxJS는 무엇을 해결하려 했나?

- 상태 변화에 대한 문제를 옵저버 패턴을 기반으로 해결하려함

### 1.6.1 상태 변화는 언제 종료되는가?

- observer와 subject간에 별도의 규칙을 정해서 observer측에서 별도의 예외처리를 해줘야함
  - 아쉬운 부분

### 1.6.2 상태변화에서 에러가 발생하면?

- subject 자체적으로 에러 처리
  - try-catch문을 통해
- observer 쪽에서 에러 발생 여부를 인지하고, 이에대한 별도의 처리
- 옵저버 패턴은 에러 발생 여부를 Observer들에게 전달할 방법이 딱히 없음

### 1.6.3 Observer에 의해 Subject의 상태가 변경되는 경우

- 예) 신문 기자이면서 동시에 구독자인 사람이 있는 경우
  - 구독받은 기사의 내용을 조금 변경하여 가짜 뉴스를 만들어냄
- 데이터를 양방향으로 흐르게하면 편할수 있으나, 코드의 복잡도를 증가시킴

-----

### 1.7 RxJS는 어떻게 개선했나?

- RxJS에서 전달되는 데이터는 모두 Observable 형태로 반환됨.

  - Observable은 구독(subscribe) 과정 후부터 데이터를 전달받음

  - ``` javascript
    const {fromEvent } = rxjs;
    const click$ = fromEvent(document, "click");
    click$.subscribe(function(v) {
        console.log(v);
    });

    // 또는
    click$.subscribe({
        next: function(v) {
            console.log(v);
        }
    });
    ```

- 반면 옵저버 패턴은 add 과정 후부터 데이터를 전달받음

> RxJS의 Observer는 함수와 객체 둘 다 가능하며  subscribe라는 메소드를 통해 Subject에게 전달됨
>
> RxJS의 Observable은 단지 하나의 Observer에게 독립적인 데이터를 전달함

### 1.7.1 인터페이스의 확장

- RxJS는 시간의 축으로 데이터를 보기 때문에 데이터의 연속적인 변화를 Observer에서 표현할 수 있도록 기존 update 메소드를 next로 바꿈
- 또한 종료를 나타내는 complete, 에러 시점을 나타내는 error 메소드가 추가됨
  - 옵저버 패턴에서의 Observer는 update하나의 메소드를 가짐
  - 반면 Rxjs의 Observer는 next, complete, error 세개의 메소드
- **객체는 상태를 가질 수 있기때문에, RxJS의 subscribe는 가급적 상태가 존재하지 않는 함수 형태를 사용함**

### 1.7.2 Observable은 Read-only

- 단방향 데이터 흐름을 위함
  - Observer에게 데이터를 전달만함, 받지 않음

-----

### 1.8 Observable은 리액티브함

- 데이터가 발생하면 Observer에게 자동으로 그리고 빠르게 변경된 데이터를 전달하기 떄문에 리액티브하다고 함
  - [리액티브 프로그래밍](https://en.wikipedia.org/wiki/Reactive_programming)





