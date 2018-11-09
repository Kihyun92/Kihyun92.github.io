---
title: [Jest] Getting Started
date: 2018-11-09 10:51:02
categories:
    - jest
    - unit test
tags:
    - jest
    - getting started
---

이 문서는 [Jest Docs](https://jestjs.io/docs/en/getting-started)를 번역한 내용입니다.

# 시작하기

[`yarn`](https://yarnpkg.com/en/package/jest)으로 jest 설치하기 :
``` bash
    yarn add --dev jest
```

[`npm`](https://www.npmjs.com/)으로 설치 :
``` bash
    npm install --save-dev jest
```

이제 두 수의 합을 더해서 리턴하는 함수를 만들어서 테스트를 시작해봅시다. 먼저, `sum.js` 파일을 생성합니다.

``` javascript
    function sum(a, b) {
        return a + b;
    }
    module.exports = sum;
```
그 다음, `sum.test.js`파일을 생성합니다. 이 파일에서 실제 테스트가 진행됩니다.

``` javascript
    const sum = require('./sum');

    test('adds 1 + 2 to equal 3', () => {
        expect(sum(1, 2)).toBe(3);
    });
```

다음으로 `package.json`에 다음 코드를 추가합니다.
``` javascript
    {
        "scripts": {
            "test": "jest"
        }
    }
```

마지막으로 `yarn test` 혹은 `npm run test`를 해주시면 콘솔에 아래와 같은 메시지가 찍히는 것을 볼 수 있습니다.

``` bash
    PASS  ./sum.test.js
    ✓ adds 1 + 2 to equal 3 (5ms)
```

*이것으로 당신의 Jest를 사용한 첫 테스트를 성공적으로 작성했습니다!*


이번 테스트에선 `expect`와 `toBe`를 사용하여 두 value들이 완전히 똑같다는 것을 테스트해 보았습니다. Jest로 테스트할 수 있는 다른 것들을 배우고 싶으시면, [Using Matchers](https://jestjs.io/docs/en/using-matchers)를 보세요.

## 커맨드라인으로 실행하기

CLI를 통해 다양하고, 유용한 옵션들을 사용하여 Jest를 실행할 수 있습니다.
