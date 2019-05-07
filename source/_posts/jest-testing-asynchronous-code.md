---
title: Jest - Testing Asynchronous Code
date: 2019-05-03 14:34:02
categories:
    - Jest
    - Unit test
tags:
    - Jest
    - Unit Test
    - Jest 번역
    - 비동기 테스트
    - Test Asynchronous Code
---

해당 포스트의 내용은 Jest 공식 문서의 [Testing Asynchronous Code](https://jestjs.io/docs/en/asynchronous)를 개인 공부를 위해 번역한 것 입니다. 오역이 있을 수 있으니, 정정해야할 내용은 댓글로 알려 주시면 감사하겠습니다.

---

# 비동기 코드 테스트 하기

JavaScript에서 비동기 적으로 실행되는 코드는 일반적입니다. 비동기로 실행되는 코드가있는 경우, Jest는 테스트 중인 코드가 완료된 시점을 알아야 다른 테스트로 넘어갈 수 있습니다. Jest는 이를 처리할 몇가지 방법이 있습니다.

## Callbacks

가장 일반적인 비동기 패턴은 콜백입니다.

예를 들어 일부 데이터를 가져와 `callback(data)`이 완료되면 호출하는 `fetchData(callback)` 함수가 있다고 가정해보겠습니다. 이때 반환 된 데이터가 `'peanut butter'` 문자열 인지 테스트 하려고 합니다.

기본적으로 Jest 테스트는 실행이 끝나면 완료됩니다. 즉, 이 테스트는 의도 한대로 동작하지 않습니다.

```javascript
// Don't do this!
test('the data is peanut butter', () => {
    function callback(data) {
        expect(data).toBe('peanut butter');
    }

    fetchData(callback);
});
```

문제는 `fetchData`가 완료되면, 즉시 콜백을 호출하기 전에 테스트가 완료된다는 것입니다.

이 문제를 해결하는 다른 형태의 `테스트`가 있습니다. 빈 인자가 있는 함수에 테스트를 두는 대신에, `done`이라는 단일 인자를 사용하십시오. Jest는 테스트가 끝나기 전에 done 콜백이 호출 될 때까지 기다릴 것 입니다.

```javascript
test('the data is peanut butter', done => {
    function callback(data) {
        expect(data).toBe('peanut butter');
        done();
    }

    fetchData(callback);
});
```

우리가 원하는대로, `done()`이 호출되지 않으면 테스트가 실패할 것 입니다.

## Promises

코드가 `Promise`를 사용할 때, 비동기 테스트를 처리하는 간단한 방법이 있습니다. 테스트에서 `Promise`를 리턴하면, Jest는 그 `Promise`가 `resolve` 될 때까지 기다릴 것입니다. `Promise`가 `reject`되면 테스트는 자동으로 실패합니다.

예를 들어, 콜백을 사용하는 대신 `fetchData`가 `'peanut butter'` 문자열로 `resolve` 되어야하는 `promise`를 반환한다고 가정 해 봅시다. 우리는 다음과 같이 테스트 할 수 있습니다.

```javascript
test('the data is peanut butter', () => {
    return fetchData().then(data => {
        expect(data).toBe('peanut butter');
    });
});
```
