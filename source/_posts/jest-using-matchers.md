---
title: Jest - Using Matchers
date: 2018-11-10 14:07:41
categories:
    - Jest
    - 공식 문서
tags:
    - Jest
    - Using Matchers
    - Jest 번역
---

해당 포스트의 내용은 Jest 공식 문서의 [Using Matchers](https://jestjs.io/docs/en/using-matchers)를 개인 공부를 위해 번역한 것 입니다. 오역이 있을 수 있으니, 정정해야할 내용은 댓글로 알려 주시면 감사하겠습니다.

---

# Matcher들 사용하

Jest에서 `matcher`를 사용하여 다양한 방법으로 값을 테스트 할 수 있습니다. 이 문서에서는 일반적으로 사용되는 matcher들을 소개합니다. 전체 목록은 [`expect` API doc](https://jestjs.io/docs/en/expect)을 참조하세요.

## 일반적인 Matcher

값을 테스트하는 가장 심플한 방법은 완전히 같은지 확인하는 겁니다.

```javascript
test('two plus two is four', () => {
    expect(2 + 2).toBe(4);
});
```

위의 코드에서 `expect(2 + 2)`는 "예상되는" 객체를 리턴합니다. 일반적으로 호출 대상을 제외하고는 이런 예상 객체(expectation objects)를 잘 사용하지 않습니다. 이 코드에선 `.toBe(4)`가 matcher 입니다. Jest가 실행되면, 모든 실패하는 matchers들을 거치게 되고, 아주 좋은 에러 메세지를 출력할 겁니다.

`toBe`는 `Object.is`를 사용하여 완전히 같은지 테스트합니다. 만약 객체의 값을 체크하고 싶다면 `toEqual`을 사용하면 됩니다.

```javascript
test('object assignment', () => {
    const data = {one: 1};
    data['two'] = 2;
    expect(data).toEqual({one: 1, two: 2});
});
```

`toEqual`은 객체나 배열의 모든 필드를 재귀적으로 체크합니다.

또한 matcher의 반대값도 테스트할 수 있습니다.

```javascript
test('adding positive numbers is not zero', () => {
    for (let a = 1; a < 10; a++) {
        for (let b = 1; b < 10; b++) {
            expect(a + b).not.toBe(0);
        }
    }
});
```

## Truthiness (진실성 부여? 해석이 어렵네요...)

테스트에서 때때로 `undefined`, `null`, `false`를 구분해야할 필요가 있지만, 때때로 이것들을 다르게 처리하고 싶지 않을 때가 있을 것입니다. Jest에는 당신이 원하는 것을 명시할 수 있게 해주는 헬퍼가 포함되어있습니다.

-   `toBeNull`은 오직 `null`에만 매치됩니다.
-   `toBeUndefined`는 오직 `undefined`에만 매치됩니다.
-   `toBeDefined`는 `toBeUndefined`의 반대가 됩니다.
-   `toBeTruthy`는 `if`문이 true로 처리하는 모든 것과 일치합니다.
-   `toBeFalsy`는 `if`문이 false로 처리하는 모든 것과 일치합니다.

예제:

```javascript
test('null', () => {
    const n = null;
    expect(n).toBeNull();
    expect(n).toBeDefined();
    expect(n).not.toBeUndefined();
    expect(n).not.toBeTruthy();
    expect(n).toBeFalsy();
});

test('zero', () => {
    const z = 0;
    expect(z).not.toBeNull();
    expect(z).toBeDefined();
    expect(z).not.toBeUndefined();
    expect(z).not.toBeTruthy();
    expect(z).toBeFalsy();
});
```

당신의 코드에서 수행하고자 하는 작업과 가장 일치하는 matcher를 사용해야 합니다.

## Numbers

숫자를 비교하는 대부분의 방법에는 마찬가지로 matcher를 쓸 수 있다.

```javascript
test('two plus two', () => {
    const value = 2 + 2;
    expect(value).toBeGreaterThan(3);
    expect(value).toBeGreaterThanOrEqual(3.5);
    expect(value).toBeLessThan(5);
    expect(value).toBeLessThanOrEqual(4.5);

    // toBe and toEqual are equivalent for numbers
    expect(value).toBe(4);
    expect(value).toEqual(4);
});
```

매우 작은 반올림 에러가 발생하는걸 원하지 않는다면, 부동 소수점의 동일성을 체크할 경우에는 `toEqual`대신 `toBeClose`를 사용하세요.

```javascript
test('adding floating point numbers', () => {
    const value = 0.1 + 0.2;
    //expect(value).toBe(0.3);           This won't work because of rounding error
    expect(value).toBeCloseTo(0.3); // This works.
});
```

## String

`toMatch`를 사용하여 정규표현식에 대해서 문자열 검사를 할 수 있습니다.

```javascript
test('there is no I in team', () => {
    expect('team').not.toMatch(/I/);
});

test('but there is a "stop" in Christoph', () => {
    expect('Christoph').toMatch(/stop/);
});
```

## 배열과 반복문

`toContain`을 사용하여 배열이나 반복문에 특정 항목이 포함되어 있는지 확인할 수 있습니다.

```javascript
const shoppingList = ['diapers', 'kleenex', 'trash bags', 'paper towels', 'beer'];

test('the shopping list has beer on it', () => {
    expect(shoppingList).toContain('beer');
    expect(new Set(shoppingList)).toContain('beer');
});
```

## Exceptions

`toThrow`를 사용하여 특정 함수가 호출 되었을 때 에러를 던지도록 테스트 할 수 있습니다.

```javascript
function compileAndroidCode() {
    throw new ConfigError('you are using the wrong JDK');
}

test('compiling android goes as expected', () => {
    expect(compileAndroidCode).toThrow();
    expect(compileAndroidCode).toThrow(ConfigError);

    // You can also use the exact error message or a regexp
    expect(compileAndroidCode).toThrow('you are using the wrong JDK');
    expect(compileAndroidCode).toThrow(/JDK/);
});
```

## 그리고...

이것은 그저 맛보기 정도입니다. 완전한 matcher들의 리스트를 확인하려면 [레퍼런스 문서](https://jestjs.io/docs/en/expect)를 확인하세요.

사용 가능한 matcher들에 대해 알게 되었으니, 그 다음으로 [Jest로 비동기 코드 테스트](https://jestjs.io/docs/en/asynchronous)를 하는 방법을 보는게 좋습니다!
