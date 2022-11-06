---
title: Router
---

# Router

## historyApiFallback

서버에 존재하지 않는 path를 입력시 `Cannot GET /something`과 같은 에러가 나는데 원인은 서버쪽 라우터에서 요청에 맞는 패스가 없기 때문에 발생

webpack-dev-server에 추가해서 해결가능하다.

``` javascript
  devServer: {
    historyApiFallback: {
      index: 'index.html',
    },
  },
```
