---
title: Javascript
---

# Javascript

## Object Literal lookups

switch문과 같은 조건문 대신에 사용하면 좋은 패턴이다!
[참조](https://ultimatecourses.com/blog/deprecating-the-switch-statement-for-object-literals)

``` javascript
function getDrink (type) {
  var drinks = {
    'coke': 'Coke',
    'pepsi': 'Pepsi',
    'lemonade': 'Lemonade',
    'default': 'Default item'
  };
  return 'The drink I chose was ' + (drinks[type] || drinks['default']);
}

var drink = getDrink('coke');
```

### default case 없이 사용할 경우

``` javascript
function getDrink (type) {
  return 'The drink I chose was ' + {
    'coke': 'Coke',
    'pepsi': 'Pepsi',
    'lemonade': 'Lemonade'
  }[type];
}
```

### 함수로 사용한 경우

```javascript
var type = 'coke';

var drinks = {
  'coke': function () {
    return 'Coke';
  },
  'pepsi': function () {
    return 'Pepsi';
  },
  'lemonade': function () {
    return 'Lemonade';
  }
};

drinks[type]();
```

### basic solution

```javascript
function getDrink (type) {
  var drink;
  var drinks = {
    'coke': function () {
      drink = 'Coke';
    },
    'pepsi': function () {
      drink = 'Pepsi';
    },
    'lemonade': function () {
      drink = 'Lemonade';
    },
    'default': function () {
      drink = 'Default item';
    }
  };

  // invoke it
  (drinks[type] || drinks['default'])();

  // return a String with chosen drink
  return 'The drink I chose was ' + drink;
}

var drink = getDrink('coke');
```

### Typescript 참고

https://github.com/microsoft/TypeScript/issues/35859

## handler 네이밍

참고하자.
- https://jaketrent.com/post/naming-event-handlers-react/
- https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Event_handlers

## RORO 패턴

[참고](https://www.freecodecamp.org/news/elegant-patterns-in-modern-javascript-roro-be01e7669cbd/)

## Date

- ISO?
  - ISO 8601은 날짜와 시간의 표기에 관한 국제 표준 규격이다.
  - YYYY-DDD (확장 형식) 또는 YYYYDDD (기본 형식)으로 표기한다.
  - 시간의 표기에는 쌍점을 쓴 hh:mm:ss (확장 형식) 또는 hhmmss (기본 형식)을 사용한다.
  - 날짜와 시간을 함께 표기할 때에는, 날짜와 시간 사이에 T를 넣어 표기한다.
  - 시간대를 표기할 때에는 Z또는 +/- 기호를 사용한다.
    - UTC 시간대에서는 시각 뒤에 Z를 붙인다.
    - `예) 1981-02-22T09:00Z 또는 19810222T0900Z : UTC 시간대에서의 1981년 2월 22일 오전 9시`
    - UTC 외의 시간대에서는 시각 뒤에 +- hh:mm, +- hhmm, +- hh 를 덧붙여 쓴다.
    - `예) 1981-02-22T09:00:00+09:00 : UTC+9 시간대에서의 1981년 2월 22일 오전 9시`
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toISOString

- UTC?
  - 실제로 국제 전기 통신 연합은 통일된 약자를 원했지만,
영어권의 사람들과 프랑스어권의 사람들은 각각 자신의 언어로 된 약자를 사용하길 원했다.
영어권은 CUT(Coordinated Universal Time)을, 프랑스어권은 TUC(Temps Universel Coordonne)를 제안했으며,
결국 두 언어 모두 C, T, U로 구성되어 있는 것에 착안해 UTC로 약어를 결정하기로 했다.

뭐가 다른거지
- https://ohgyun.com/416

## 정규식 적용

`정규식.test(텍스트);`

```javascript
export const emailMatchRegex = new RegExp(
  '^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$',
  'i'
);

const isEmailForamt = (text: string) => emailMatchRegex.test(text);
```

## 객체의 key 값에 원하는 변수값을 할당하고 싶은 경우

```javascript
  WeverseAdminRoles.map(role => {
    return Object.assign(rolesObj, {[role]: roles.includes(role)});
  })
```

-> [] 괄호를 사용하면 가능하다!

## snakeToCamel

``` javascript
export const snakeToCamel = (str: string) => str.toLowerCase().replace(/[-_]([a-z])/g, (_, group) => group.toUpperCase());
```

## 스토리지 제어

비동기가 아닌 동기처리라서 I/O 읽기되는 만큼 모든 렌더링이 지연되기 때문에 스토리지는 이펙트에서 접근해야함.

## Event

`event.preventDefault()`: 이벤트를 취소할 수 있는 경우, 이벤트의 전파를 막지 않고 그 이벤트를 취소

`event.stopPropagation()`: 이벤트 캡쳐링과 버블링에 있어 현재 이벤트 이후의 전파를 막음

### 마우스 우클릭에 대한 이벤트

`MouseEvent`

`event.which`는 deprecated 됨 => event.button을 사용 (0 = left, 1 = center, 2 = right)

참고: https://stackoverflow.com/questions/2405771/is-right-click-a-javascript-event

### contextmenu

브라우저에서 마우스 우클릭시 노출되는 메뉴에 대한 이벤트

리액트에서 아래와 같이 해당 페이지에서 우클릭을 막을 수 있다.

``` typescript
  useEffect(() => {
    document.addEventListener('contextmenu', handleBlockRightClick);
    
    return (() => document.removeEventListener('contextmenu', handleBlockRightClick));
  }, []);

  const handleBlockRightClick = useCallback((event: MouseEvent) => {
    event.preventDefault();
    return false;
  }, []);
```
