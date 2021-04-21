---
title: React
---

# React

## 왜 함수형 컴포넌트인가?

[참고](https://boxfoxs.tistory.com/395)

### 클래스형 컴포넌트와 함수형 컴포넌트의 차이

기존엔 라이프사이클 컨트롤 유무였지만, 함수형 컴포넌트에서도 hook(16.8 버전 이후)을 이용하면 된다.

또한 클래스형 컴포넌트에는 props를 재사용 하기 때문에 의도와 다르게 동작하는 문제점이 있다.

그외에도 가독성이 좋으며 테스트가 편하다.

### hooks

- [useState](/useState)
- [useEffect](/useEffect)
- [useCallback](/useCallback)

---

## React.FC를 왜 써야하는가에 대한 정리

벨로퍼트님이 잘 정리해주셨다. [참고](https://velog.io/@velopert/create-typescript-react-component)

그외에 함수형 컴포넌트 사용시 화살표 함수로 선언할지 아니면 function 키워드를 사용할지에 대해서도 정리되어있다.

- React.FC를 사용하면 defaultProps를 사용해도 에러가 발생함.

---

## useRef

`useRef`는 `.current` 프로퍼티로 전달된 인자(initialValue)로 초기화된 변경 가능한 `ref 객체`를 반환합니다. 반환된 객체는 컴포넌트의 전 생애주기를 통해 유지될 것입니다.

> 주로 태그를 직접 다룰 경우 사용, 간단하지 않은 구조의경우(반복 등) id대신 사용

---

## useMemo

- 상태나 디펜더시에 따라 변하는 인스턴스
- 과한 연산으로 인한 메모이제이션을 기대하는 결과
- memo에 영향이 있을 수 있는 mutable한 값(객체, 배열, 함수, 컴포넌트)라던지, expensive한 계산에만 쓰는게 좋음

---

## Event handler convention

https://medium.com/javascript-in-plain-english/handy-naming-conventions-for-event-handler-functions-props-in-react-fc1cbb791364

---

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
