---
title: Jest - Setup and Teardown
date: 2019-05-07 14:36:14
categories:
    - Jest
    - 공식 문서
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

## 일회성 설정

경우에 따라 파일 시작 부분에서 한 번만 설정하면 됩니다. 설정이 비동기 일 때 특히 불편할 수 있으므로 인라인으로 설정할 수 없습니다. Jest는 이러한 상황을 처리하기 위해 `beforeAll`과 `afterAll`을 제공합니다.

예를 들어, `initializeCityDatabase` 및 `clearCityDatabase`가 프로미스를 반환하고 도시 데이터베이스를 테스트 간에 다시 사용할 수있는 경우, 테스트 코드를 다음과 같이 변경할 수 있습니다.

```javascript
beforeAll(() => {
    return initializeCityDatabase();
});

afterAll(() => {
    return clearCityDatabase();
});

test('city database has Vienna', () => {
    expect(isCity('Vienna')).toBeTruthy();
});

test('city database has San Juan', () => {
    expect(isCity('San Juan')).toBeTruthy();
});
```

## Scoping

기본적으로 `before` 및 `after` 블록은 파일의 모든 테스트에 적용됩니다. 또한 `describe` 블록을 사용하여 테스트를 그룹화 할 수도 있습니다. 그들이 `describe` 블록 안에 있을 때, `before` 및 `after` 블록은 해당 `describe` 블록 내의 테스트에만 적용됩니다.

예를 들어, 우리가 도시 데이터베이스 뿐만 아니라 음식 데이터베이스를 가지고 있다고 가정 해 봅시다. 다른 테스트를 위해 다른 설정을 할 수 있습니다.

```javascript
// Applies to all tests in this file
beforeEach(() => {
    return initializeCityDatabase();
});

test('city database has Vienna', () => {
    expect(isCity('Vienna')).toBeTruthy();
});

test('city database has San Juan', () => {
    expect(isCity('San Juan')).toBeTruthy();
});

describe('matching cities to foods', () => {
    // Applies only to tests in this describe block
    beforeEach(() => {
        return initializeFoodDatabase();
    });

    test('Vienna <3 sausage', () => {
        expect(isValidCityFoodPair('Vienna', 'Wiener Schnitzel')).toBe(true);
    });

    test('San Juan <3 plantains', () => {
        expect(isValidCityFoodPair('San Juan', 'Mofongo')).toBe(true);
    });
});
```

`beforeEach` 최상위 레벨은 `describe` 블록 내에서 `beforeEach` 앞에 실행됩니다. 모든 훅의 실행 순서를 설명하는데 도움이 될 수 있습니다.

```javascript
beforeAll(() => console.log('1 - beforeAll'));
afterAll(() => console.log('1 - afterAll'));
beforeEach(() => console.log('1 - beforeEach'));
afterEach(() => console.log('1 - afterEach'));
test('', () => console.log('1 - test'));
describe('Scoped / Nested block', () => {
    beforeAll(() => console.log('2 - beforeAll'));
    afterAll(() => console.log('2 - afterAll'));
    beforeEach(() => console.log('2 - beforeEach'));
    afterEach(() => console.log('2 - afterEach'));
    test('', () => console.log('2 - test'));
});

// 1 - beforeAll
// 1 - beforeEach
// 1 - test
// 1 - afterEach
// 2 - beforeAll
// 1 - beforeEach
// 2 - beforeEach
// 2 - test
// 2 - afterEach
// 1 - afterEach
// 2 - afterAll
// 1 - afterAll
```

## describe 및 test 블록 실행 순서

Jest는 실제 테스트를 실행하기 전에 모든 테스트 핸들러를 테스트 파일에 실행합니다. 이것은 describe 블록 내부가 아닌 `before*` 및 `after*` 핸들러 내부에서 설정 및 해제를 수행해야하는 또 다른 이유입니다. describe 블록이 완료되면, 기본적으로 Jest는 수집 단계에서 모든 테스트를 순차적으로 실행하고, 각 테스트가 완료 될 때까지 기다렸다가 계속 진행하기 전에 정리합니다.

다음과 같은 예시 테스트 파일 및 출력을 고려하세요:

```javascript
describe('outer', () => {
    console.log('describe outer-a');

    describe('describe inner 1', () => {
        console.log('describe inner 1');
        test('test 1', () => {
            console.log('test for describe inner 1');
            expect(true).toEqual(true);
        });
    });

    console.log('describe outer-b');

    test('test 1', () => {
        console.log('test for describe outer');
        expect(true).toEqual(true);
    });

    describe('describe inner 2', () => {
        console.log('describe inner 2');
        test('test for describe inner 2', () => {
            console.log('test for describe inner 2');
            expect(false).toEqual(false);
        });
    });

    console.log('describe outer-c');
});

// describe outer-a
// describe inner 1
// describe outer-b
// describe inner 2
// describe outer-c
// test for describe inner 1
// test for describe outer
// test for describe inner 2
```

## 일반적인 조언

테스트가 실패하면 가장 먼저 점검해야 할 사항 중 하나는 실행되는 유일한 테스트 일 때 테스트가 실패하는지 여부입니다. Jest에서는 단 하나의 테스트만 실행하는게 간단합니다. 단지 테스트 명령을 `test.only`로 변경해주면 됩니디.

```javascript
test.only('this will be the only test that runs', () => {
    expect(true).toBe(false);
});

test('this test will not run', () => {
    expect('A').toBe('A');
});
```

대규모 패키지의 일부로 실행될 때 종종 실패하지만 혼자 실행할 땐 실패하지 않는 테스트가 있을 때, 다른 테스트의 일부가 이 테스트에 간섭한다고 확신할 수 있습니다. `beforeEach`를 사용하여 공유 상태를 정리해서 이런 문제를 해결할 수 있습니다. 공유 상태가 수정되는지 여부가 확실하지 않은 경우에도 `beforeEach`를 사용하여 데이터를 기록 할 수도 있습니다.
