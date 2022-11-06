---
title: Javascript Testing Introduction Tutorial
date: 2018-10-16 11:50:33
tags:
    - javascript
    - test
---

[Javascript test tutorial 영상](https://www.youtube.com/watch?v=r9HdJ8P6GQI&feature=push-sd&attr_tag=KRUQImvHMMCLBFNo%3A6)을 정리해보자.

---

## What is "Testing"?

![](/images/javascript_test_capture1.png)

- 테스트를 함으로써 Test -> Failure -> Modify & Fix -> Test 까지의 일련의 과정을 Automate & Simplify 할 수 있다!


## Why Test?

- Get an Error if you break code
    - 일일이 까보지 않고, 즉시 모든 테스트 결과를 볼 수 있다!
- Save time
    - 매뉴얼대로 일일이 테스트 하지 않아도됨
- Think about possible issues & bugs
    - 테스트를 작성하면서 우리가 뭘 테스트 하고 싶은지
    - 어떻게 올바른 테스트를 작성해야하는지
- Integrate into build workflow
- Break up complex ependencies
- imporove your code


## Different Kinds of Tests

- Fully Isolated(순수 함수) -> Unit Tests

- With Dependencies -> Integration Tests

- Full Flow (UI 조작이 필요한 경우 or 앱 전체 동작을 테스팅) -> End-to-End(E2E) Tests

> 아래로 갈수록 복잡도는 높아진다.

> 올라갈수록 Frequency(테스트 개수는 늘어난다)

## Testing Setup

![](/images/javascript_test_capture2.png)

---

예제 코드를 통해 어떻게 하는지 알아보자.

## Unit Tests
- input parameter가 있고, return이 있는 순수함수
- 실패하는 테스트를 짜면서 점점 케이스를 생각하고 늘려가자

## Integration Test
- 다른 함수에 의존성이 있는 함수의 경우
- input param, return value가 없는 경우
- DOM 조작하는 경우

> 일단 원본 source를 수정해야함 -> test할 부분을 module화

> 이제 이 모듈을 테스트!


## e2e Test
- 영상 29분 부터!


