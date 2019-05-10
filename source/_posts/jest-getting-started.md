---
title: Jest - Getting Started
date: 2018-11-09 10:51:02
categories:
    - Jest
    - 공식 문서
tags:
    - Jest
    - Getting Started
    - Jest 번역
---

해당 포스트의 내용은 Jest 공식 문서의 [Getting Started](https://jestjs.io/docs/en/getting-started)를 개인 공부를 위해 번역한 것 입니다. 오역이 있을 수 있으니, 정정해야할 내용은 댓글로 알려 주시면 감사하겠습니다.

---

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

**이것으로 당신은 Jest를 사용한 첫 테스트를 성공적으로 작성했습니다!**


이번 테스트에선 `expect`와 `toBe`를 사용하여 두 값이 완전히 똑같다는 것을 테스트 했습니다. Jest로 테스트할 수 있는 다른 것들을 배우고 싶으시면, [Using Matchers](https://jestjs.io/docs/en/using-matchers)를 보세요.



## 커맨드라인으로 실행하기

CLI를 통해 다양하고, 유용한 옵션들을 사용하여 Jest를 실행할 수 있습니다.

my-test와 일치하는 파일에서 Jest를 실행하고, config.json을 구성 파일로 사용하고 실행 후 native OS 알림을 표시하는 방법은 다음과 같습니다.
``` bash
    jest my-test --notify --config=config.json
```

커맨드 라인을 통해 jest를 실행하는 것에 대해 더 알고 싶다면, [Jest CLI Options](https://jestjs.io/docs/en/cli) 페이지를 보십시오.


# 추가 구성

## 기본 구성 파일 생성
프로젝트에 따라 Jest는 몇 가지 질문을 하고 각 옵션에 대한 간단한 설명과 함께 기본 구성 파일을 만듭니다.
``` bash
    jest --init
```

## Babel 사용하기
[Babel](https://babeljs.io/)을 사용하려면 `babel-jest` 및 `regenerator-runtime` 패키지를 설치하십시오.
``` bash
    yarn add --dev babel-jest babel-core regenerator-runtime
```

> 참고: Babel 버전 7을 사용하고 있다면 다음 명령으로 `babel-jest`, `babel-core@^7.0.0-bridge.0` 및 `@ babel/core`를 설치해야합니다.

``` bash
    yarn add --dev babel-jest babel-core@^7.0.0-bridge.0 @babel/core regenerator-runtime
```
> node_module을 트랜스파일하려면 `babel.config.js`를 사용해야합니다. 자세한 내용은 [https://babeljs.io/docs/en/next/config-files](https://babeljs.io/docs/en/next/config-files)를 참조하십시오.<br /><br />Jest 레포지토리에서 예제를 볼 수 있습니다.<br />[https://github.com/facebook/jest/tree/master/examples/babel-7](https://github.com/facebook/jest/tree/master/examples/babel-7)


_참고: npm 3 또는 4 또는 Yarn을 사용하는 경우 `regenerator-runtime`을 설치하지 않아도됩니다._

프로젝트의 루트 폴더에 `.babelrc` 파일을 추가하는 것을 잊지 마십시오. 예를 들어, `babel-preset-env` 및 `babel-preset-react` presets과 함께 ES6 및 [React.js](https://reactjs.org/)를 사용하는 경우 :

``` bash
    {
        "presets": ["env", "react"]
    }
```

이제 모든 ES6 기능과 React specific syntax를 사용하도록 설정되었습니다.

> 참고: Babel의 `env` 옵션을 사용하여 더 복잡한 Babel 구성을 사용하는 경우, Jest는 자동으로 `NODE_ENV`를 `테스트`로 정의합니다. `NODE_ENV`가 설정되어 있지 않으면 Babel과 같은 `개발` 섹션을 사용하지 않습니다.

> 참고: `{ "modules": false}` 옵션을 사용하여 ES6 모듈의 transpilation이 해제 된 경우, 테스트 환경에서 이 기능을 활성화해야 합니다.

``` bash
{
    "presets": [["env", {"modules": false}], "react"],
    "env": {
    "test": {
      "presets": [["env"], "react"]
      }
    }
}
```

> 참고: `babel-jest`는 Jest를 설치할 때 자동으로 설치되며 프로젝트에 babel 구성이 있으면 파일을 자동으로 변환합니다. 이 문제를 방지하려면 명시적으로 `transform` 구성 옵션을 재설정 할 수 있습니다.
``` bash
// package.json
{
    "jest": {
        "transform": {}
    }
}
```

## 웹팩 사용하기
Jest는 assets, 스타일 및 컴파일을 관리하기 위해 [webpack](https://webpack.github.io/)을 사용하는 프로젝트에서 사용할 수 있습니다. webpack은 다른 도구에 비해 몇 가지 독특한 도전 과제를 제시합니다. 시작하려면 [webpack 안내서](https://jestjs.io/docs/en/webpack)를 참조하십시오.

## 타입스크립트 사용하기
테스트에서 TypeScript를 사용하려면 [ts-jest](https://github.com/kulshekhar/ts-jest)를 사용할 수 있습니다.