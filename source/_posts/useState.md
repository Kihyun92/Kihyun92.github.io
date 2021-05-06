---
title: useState
---

# React useState

## [지연 초기화](https://ui.toast.com/weekly-pick/ko_20201022/)

- 직접적인 값 대신 함수를 `useState`의 인자로 넘김
- 초기 값을 구하기 위한 계산 비용이 클 때 `useState`의 지연 초기화를 사용
- 지연 초기화는 상태가 최초로 생성될 때만 실행, 이후 발생하는 리렌더링에서는 실행되지 않음

``` javascript
const [count, setCount] = useState(() =>
  Number.parseInt(window.localStorage.getItem(cacheKey)),
)
```

## 렌더링에 영향을 미칠만한 상태가 아닐땐 ref를 사용하는게 좋다

> 예시 상황
> - 모달이 중첩된 경우, 모달을 닫을때 body의 overflow를 풀어버려서 뒤쪽 스크롤 되는 현상
> - 열린 모달 수를 관리하는 컨텍스트 생성하여 개수에 따라 overflow hidden 처리함

```typescript
import React, { createContext, useContext, useRef } from 'react';

interface BodyScrollLockContext {
  lockScroll: () => void;
  unlockScroll: () => void;
}

const BodyScrollLockContext = createContext<BodyScrollLockContext>({} as BodyScrollLockContext);

const BodyScrollLockProvider: React.FC = props => {
  const modalCountRef = useRef<number>(0);  // useState를 사용할 수 있지만, 렌더링에 영향을 미칠만한 상태가 아니기 때문에 ref를 사용했다

  const lockScroll = () => {
    modalCountRef.current++;
    if (modalCountRef.current > 0) {
      document.body.style.overflow = 'hidden';
    }
  };

  const unlockScroll = () => {
    modalCountRef.current--;
    if (modalCountRef.current === 0) {
      document.body.style.overflow = '';
    }
  };

  const bodyScrollLockContext: BodyScrollLockContext = {
    lockScroll,
    unlockScroll
  };

  return <BodyScrollLockContext.Provider value={bodyScrollLockContext} {...props} />;
};

const useBodyScrollLockContext = () => useContext(BodyScrollLockContext);

export { BodyScrollLockProvider, useBodyScrollLockContext };

```
