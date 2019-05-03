---
title: jest-using-matchers
date: 2018-11-10 14:07:41
categories:
    - Jest
    - Unit Test
tags:
    - Jest
    - Using Matchers
    - Jest 번역
---

# Matcher들 사용하기

이 문서는 [Jest Docs - Using Matchers](https://jestjs.io/docs/en/using-matchers)를 번역한 내용입니다.

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
