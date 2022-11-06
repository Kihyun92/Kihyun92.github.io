---
title: Webpack
---

# Webpack
## webpack-preprocessor-loader

[참고](https://github.com/afterwind-io/preprocessor-loader)

아래와 같이 주석으로 조건문을 사용해서 환경에 따라 코드를 포함시킬 수 있습니다.

``` markdown
// #!if ENV === 'development'
여기에 작성되는 코드는 development 환경에서만 포함됩니다.
// #!endif
```

## [HtmlWebpackPlugin](https://webpack.js.org/plugins/html-webpack-plugin/)

htmlWebpackPlugin > bundle 생성해주는걸 도와줌 (index.html)

- entry, output 설정
- plugin을 추가해줘야함
    - template: index.html
    - 이렇게 하면 dist/index.html에 body가 생김
