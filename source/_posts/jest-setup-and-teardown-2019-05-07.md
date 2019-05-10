---
title: Jest - Setup and Teardown
date: 2019-05-07 14:36:14
categories:
    - jest
    - unit test
tags:
    - Jest
    - Unit Test
    - Jest 번역
    - 설정 및 해제
    - Setup and Teardown
---

해당 포스트의 내용은 Jest 공식 문서의 [Setup and Teardown](https://jestjs.io/docs/en/setup-teardown)을 개인 공부를 위해 번역한 것 입니다. 오역이 있을 수 있으니, 정정해야할 내용은 댓글로 알려 주시면 감사하겠습니다.

---

# 설정 및 해제

테스트를 작성하는 동안 테스트를 실행하기 전에 수행해야하는 설정 작업이 있으며 테스트를 실행 한 후에 해야 할 작업이 있습니다. Jest는 이것을 처리 할 도우미 함수를 제공합니다.

## 많은 테스트를 위한 반복 설정

많은 테스트를 위해 반복적으로 해야하는 작업이 있으면 `beforeEach`와 `afterEach`를 사용할 수 있습니다.

예를 들어 여러 테스트가 도시의 데이터베이스와 상호 작용한다고 가정 해 봅시다. 이러한 각 테스트 전에 호출되어야하는 `initializeCityDatabase()` 메서드와 각 테스트 후에 호출되어야하는 `clearCityDatabase()` 메서드가 있습니다. 다음과 같이 할 수 있습니다 :

```javascript
beforeEach(() => {
    initializeCityDatabase();
});

afterEach(() => {
    clearCityDatabase();
});

test('city database has Vienna', () => {
    expect(isCity('Vienna')).toBeTruthy();
});

test('city database has San Juan', () => {
    expect(isCity('San Juan')).toBeTruthy();
});
```

`beforeEach` 및 `afterEach`는 [테스트가 비동기 코드를 처리하는 것과 동일한 방식](https://jestjs.io/docs/en/asynchronous)으로 비동기 코드를 처리 할 수 ​​있습니다. `done' 매개 변수를 사용하거나 프로미스를 반환 할 수 있습니다. 예를 들어,`initializeCityDatabase()`가 데이터베이스가 초기화 될 때 resolved 된 프로미스를 반환하면, 우리는 그 프로미스를 반환하려 합니다:

```javascript
beforeEach(() => {
    return initializeCityDatabase();
});
```
