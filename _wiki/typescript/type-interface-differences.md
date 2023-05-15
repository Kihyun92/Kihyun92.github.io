---
layout  : wiki
title   : type과 interface 정리
date    : 2023-05-15 14:00:00 +0900
updated : 2023-05-15 14:00:00 +0900
tag     : typescript, type, interface
toc     : true
public  : true
parent  : [[typescript]]
latex   : true
---

* TOC
{:toc}

타입스크립트에서는 `type`과 `interface`로 타입을 명시해 줄 수 있다. 각각의 특징과 언제 사용할지 정리해보자.

## type

`type`은 `interface`와 달리 `union`과 같은 타입을 정의할 수 있다.
다양한 [유틸리티 타입](https://www.typescriptlang.org/docs/handbook/utility-types.html)들을 사용하여 타입을 정의할 수 있다.

```typescript
type Name = string;

type Peron = {
  
}
```

## interface

`interface`는 객체의 타입을 정의할 때 사용한다. `type`과 달리 `extends`를 사용하여 상속을 받을 수 있다.

```typescript
interface MyInterface {
  name: string;
  age: number;
}
```
