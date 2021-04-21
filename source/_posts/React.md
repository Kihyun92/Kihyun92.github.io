---
title: React
---

# React

## [React의 탄생 배경과 핵심 개념](https://soldonii.tistory.com/100)

업무를 진행하면서 항상 고민할것

- 컴포넌트를 얼마나 작은 단위로 쪼갤 것인지, 어떻게 재사용 가능한 컴포넌트를 만들 것인지
- state는 가상 DOM 내에 여러 곳에 존재할 수 있는데, 이를 어디에 위치시킬지
- state가 변경되었을 때, 어떤 부분이 re-rendering 되어야 하는지

## React 가 렌더링을 수행하는 시점

1. Props가 변경된 경우 → 원시값이 아닌 객체나 배열, `함수`의 경우, `얕은 비교`를 진행하기 때문에 매 랜더시 쓸데없는 얕은 평가를 진행함 → 불필요한 렌더링이 이루어질 수 있음
    - children 또한 props이므로 ReactElement의 경우에도 비교 대상이다.
2. State가 변경된 경우
3. [forceUpdate()](https://reactjs.org/docs/react-component.html#forceupdate)를 싱행한 경우
4. `부모 컴포넌트가 렌더링 된 경우`

## hooks 정리

- [useState](/useState)
- [useEffect](/useEffect)
- [useCallback](/useCallback)
- [useRef](/useRef)
- [useMemo](/useMemo)

## 왜 함수형 컴포넌트인가?

[참고](https://boxfoxs.tistory.com/395)

## 클래스형 컴포넌트와 함수형 컴포넌트의 차이

기존엔 라이프사이클 컨트롤 유무였지만, 함수형 컴포넌트에서도 hook(16.8 버전 이후)을 이용하면 된다.

또한 클래스형 컴포넌트에는 props를 재사용 하기 때문에 의도와 다르게 동작하는 문제점이 있다.

그외에도 가독성이 좋으며 테스트가 편하다.

## React.FC를 왜 써야하는가에 대한 정리

벨로퍼트님이 잘 정리해주셨다. [참고](https://velog.io/@velopert/create-typescript-react-component)

그외에 함수형 컴포넌트 사용시 화살표 함수로 선언할지 아니면 function 키워드를 사용할지에 대해서도 정리되어있다.

- React.FC를 사용하면 defaultProps를 사용해도 에러가 발생함.

## Event handler convention

https://medium.com/javascript-in-plain-english/handy-naming-conventions-for-event-handler-functions-props-in-react-fc1cbb791364

## useLayoutEffect

DOM 관련된 effect를 컨트롤 할때는 사용하는걸 권장. DOM이 완전히 그려진 다음에 실행하는 effect.
[참고](https://ko.reactjs.org/docs/hooks-reference.html#uselayouteffect)

``` typescript
useLayoutEffect(() => {
    if (postBodyRef.current && (postBodyRef.current.scrollHeight - 1 > postBodyRef.current.offsetHeight)) { // IE fix
      setIsFolded(true);
    }
  }, [body]);
```

## Modal 구현할때

[Portal](https://ko.reactjs.org/docs/portals.html) 이용하면 좋다!

- https://velog.io/@velopert/react-portals
