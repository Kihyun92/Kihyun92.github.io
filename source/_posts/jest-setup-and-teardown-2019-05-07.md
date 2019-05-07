---
title: Jest - Setup and Teardown
date: 2019-05-07 14:36:14
categories:
    - jest
    - unit test
tags:
    - Jest
    - Unit Test
    - Jest 번역
    - 설정 및 해제
    - Setup and Teardown
---

해당 포스트의 내용은 Jest 공식 문서의 [Setup and Teardown](https://jestjs.io/docs/en/setup-teardown)을 개인 공부를 위해 번역한 것 입니다. 오역이 있을 수 있으니, 정정해야할 내용은 댓글로 알려 주시면 감사하겠습니다.

---

# 설정 및 해제

테스트를 작성하는 동안 테스트를 실행하기 전에 수행해야하는 설정 작업이 있으며 테스트를 실행 한 후에 해야 할 작업이 있습니다. Jest는 이것을 처리 할 도우미 함수를 제공합니다.
