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
