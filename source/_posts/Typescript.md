---
title: Typescript
---

# Typescript Wiki

## Union type array map

Union 타입 배열을 맵핑할때 발생한 문제가 있다. Union type의 경우 함수인 멤버(map)도 union 타입으로 지정된다는 것!
`Array<Test1|Test2> and (Test1 | Test2)[]` 와 같이 타입을 지정해주면 됨.
[참고](https://stackoverflow.com/questions/49510832/typescript-how-to-map-over-union-array-type)

그런데 또 다른 문제는 map 내에 인자값의 타입이 any로 지정되버림..

## Record<Keys, Type>

`Type`이란 type을 가지는 `Keys` 속성의 집합으로 타입을 구성한다. type의 property를 다른 type에 매핑하는데 사용한다.

## Partial<Type>

`Type`의 모든 property를 optional type으로 가진다. 주어진 type의 모든 하위 type을 나타내는 type을 반환합니다.

## infer

https://typescript-kr.github.io/pages/advanced-types.html

`조건부 타입의 타입 추론 (Type inference in conditional types)`

상속 관계일때 제네릭 타입을 추정해서 가져올 수 있음

``` typescript
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;
```

```typescript
type GetPromiseType<T extends Promise<unknown>> = T extends Promise<infer V> ? V : never;

type A = GetPromiseType<Promise<string>>; // string;
type B = GetPromiseType<Promise<number>>; // number;
type C = GetPromiseType<Error>; // error
```

---

## issues

### A computed property name must be of type 'string', 'number', 'symbol', or 'any'

```typescript
export enum MyEnum {
  one = 'stringOne',
  two = 'stringTwo',
}

export const someMap = {
  [ MyEnum.one ]: 'valueOne',
  [ MyEnum.two ]: 'valueTwo',
};
```

위와 같은 상황에서 타입 에러 발생
찾아보니 몇가지 방법이 있지만, `as string`을 추가하는 방식으로 해결

```typescript
export const someMap: ForceStringType = {
  [ MyEnum.one as string ]: 'valueOne',
  [ MyEnum.two as string ]: 'valueTwo',
};
```

- https://stackoverflow.com/questions/44110641/typescript-a-computed-property-name-in-a-type-literal-must-directly-refer-to-a-b