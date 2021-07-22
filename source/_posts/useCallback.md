---
title: useCallback
---

# useCallback

## Guide

이 [문서](https://dmitripavlutin.com/dont-overuse-react-usecallback/) 를 요약해본다.

> Over use 하지 말고, 상황에 맞게 써야한다. 컴포넌트를 느려지게 할수도 있고, 성능에 해를 끼칠 수 있음

`useCallback`을 사용하지 않고 함수를 컴포넌트 내에 선언할 경우, 매 `rendering`마다 `re-create`된다
`inline function`은 저렴하기 때문에 각 렌더링에서 함수를 다시 만드는건 문제되지 않는다.
하지만 아래와 같은 경우엔 `useCallback`을 쓰는게 좋다

1. `React.memo()` 내부에 래핑된 컴포넌트는 `callback prop`을 받는다
2. 함수가 다른 `hook`에 종속적으로 사용되는 경우 (ex. `useEffect(..., [callback]`)

## 사용하는 경우

1. memoization이 필요할 정도로 많은 연산을 하는가?
2. props 형태로 넘겨서 렌더링 할 때 마다 레퍼런스가 같아야 하는가?

## Dependency

의존성에 넘겨준 값이 변할때만 메모이제이션이 변경된다
