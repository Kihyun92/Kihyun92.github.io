---
layout  : wiki
title   : React가 렌더링을 수행하는 시점
date    : 2023-05-08 17:43:00 +0900
updated : 2023-05-08 17:43:00 +0900
tag     : react
toc     : true
public  : true
parent  : [[react]]
latex   : true
---

* TOC
{:toc}

## React가 렌더링을 수행하는 시점

1. Props가 변경된 경우 → 원시값이 아닌 객체나 배열, `함수`의 경우, `얕은 비교`를 진행하기 때문에 매 랜더시 쓸데없는 얕은 평가를 진행함 → 불필요한 렌더링이 이루어질 수 있음
  - children 또한 props이므로 ReactElement의 경우에도 비교 대상이다.
  - 얕은 비교란, 같은레벨에서의 비교다. 따라서 원시값의 경우엔 값을 비교하지만, 객체의 경우엔 실제 프로퍼티 값들을 비교하지 않고, 그들의 참조 위치를 비교한다. 따라서 값이 변경되지 않아도 참조 정보가 바뀌면 리랜더링이 발생할 수 있다.
2. State가 변경된 경우
3. [forceUpdate()](https://reactjs.org/docs/react-component.html#forceupdate)를 싱행한 경우
4. `부모 컴포넌트가 렌더링 된 경우`
