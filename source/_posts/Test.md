---
title: Test
---

# 패턴

## Given, When, Then

[참고](https://github.com/ahastudio/til/blob/main/blog/2018/12-08-given-when-then.md)

## Testing Best Practices

- https://github.com/goldbergyoni/javascript-testing-best-practices/blob/master/readme.kr.md

## input에 있는 값을 찾게 테스트하려면 getByDisplayValue를 사용하기

## getBy*, queryBy*

`getBy*` 는 get을 했을때 못찾으면 그 자리에서 `바로 에러`를 냄

`queryBy*`는 `null`을 냄

## test, webpack 이슈

자바스크립트는 css 파일이나 image 파일들을 import할 수 없습니다. 그래서 webpack은 css-loader나 file-loader등을 사용해서 자바스크립트가 해당 리소스를 불러올 수 있도록 해줘야 합니다. 하지만 테스트 코드에서는 webpack으로 빌드한게 아니기 때문에 올바르게 동작하지 않습니다. 따라서 실제 코드에서는 동작하지만 테스트 코드에서는 필요없는 리소스들은 mocking해야 합니다.

jest.config.js에 다음과 같이 코드를 추가해서 리소스 파일을 불러올 때 마다 내가 지정한 가짜 코드를 불러오도록 할 수 있습니다.

```javascript
module.exports = {
  moduleNameMapper: {
    '\\.(css|less)$': '<rootDir>/__mocks__/fileMock.js'
  },
};
```

`<rootDir>/__mocks__/fileMock.js`

``` javascript
module.exports = {};
```

See also

- https://jestjs.io/docs/en/configuration#modulenamemapper-objectstring-string--arraystring

## jest mock 관련 문서

- https://dev.to/dylanju/jest-mocks-18l9
