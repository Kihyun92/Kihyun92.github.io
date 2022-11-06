---
title: style CSS
---

# CSS

## css → disabled일때 스타일 처리하는 법

```css
&:disabled {
    cursor: not-allowed;
    color: ${Color.white};
    border: 1px solid ${Color.white};
    opacity: 0.4;
  }
```

## input → props를 디스트럭쳐링해서 넘길때, styled-component → white list 정책이어서 아마 문제 없을듯(필요한것만 알아서 등록)

---

## flexbox

- 컨테이너를 꾸며주는 속성값들이 있고, 아이템들을 꾸며주는 속성값들이 있다
- 아이템들의 배치 방향에 따라 중심 축이 결정된다.
- `display: flex;`
- `flex-direction: row;`  -> 방향을 정해줘야함. default는 row
- `flex-wrap: nowrap;` -> default는 nowrap. 화면이 좁아질 경우 어떻게 표시할지
- `flex-flow: column wrap` -> 한번에 표현

### justify-content -> **중심축(main axis)**에서 아이템을 어떻게 배치할지

- flex-start, center, flex-end
- space-around -> 박스를 둘러싸서 스페이스를 넣어줌. 맨 앞뒤는 일정하지만, 겹치는 부분은 각각 적용되어 좀더 두껍
- space-evenly -> space-around와 비슷하지만 겹치는 부분까지 맨앞뒤와 동일하게 일정하다.
- space-between -> 맨 앞뒤는 공간 없고, 사이만 공간을 줌

### align-items -> **반대축(cross axis)**에서 아이템을 어떻게 배치할지

- baseline -> text를 기준으로 동일하게 정렬하고 싶을때

### align-content -> **반대축**에서 아이템을 어떻게 배치할지(justify-content와 반대)

### flex-grow

- 아이템이 점점 켜졌을때, 어떻게 노출할지
- content를 채우도록 할지 -> ex) 모든 아이템들을 `flex-grow: 1`로 하면 각 아이템들의 할당영역이 같게됨

### flex-shrink

- 반대로 아이템이 점점 줄어들때 어떻게 노출할지

### flex-basis (default: auto)

- 공간을 얼마나 차지할지 좀 더 세부적으로 조절할 수 있게 해줌
- ex) item1은 60%, item2는 30%, item3은 10% 차지하게 할 수도 있음

### align-self

- 아이템 별로 아이템을 정렬할 수 있음

## flex box 내에서 특정 자식 요소만 왼쪽/오른쪽에 두고 싶은 경우 -> margin-left: auto / margin-right: auto

정리 굳 사이트
- https://d2.naver.com/helloworld/8540176

---

## vh

- view height -> `height: 100vh` 로 할 경우, 부모의 height와 상관없이 view port를 100% 사용하겠다 라는 의미

## item center 정렬

```css
  .Aligner {
    display: flex;
    align-items: center;
    justify-content: center;
  }
```

## [pseudo-class](https://developer.mozilla.org/ko/docs/Web/CSS/:nth-child)

선택자에 추가하는 키워드

### :nth-child

형제 엘리먼트(group of siblings) 간의 순서에 따라 요소를 선택함

- odd, even
- 함수형으로 표기 가능

### [nth-last-child](https://developer.mozilla.org/ko/docs/Web/CSS/:nth-last-child)

끝부터 계산하여 형제 그룹간의 위치에 따라 엘리먼트 선택

## [content-visibility](https://wit.nts-corp.com/2020/09/11/6223)

Chrome 85에 새롭게 추가, 렌더링 성능 향상에 도움

- 화면 밖 콘텐츠의 렌더링을 생략함으로써 초기 로드 시간을 개선
- UserAgent가 layout, painting을 포함한 요소의 렌더링 작업을 필요로할 때까지 생략할 수 있도록 합니다.
- 콘텐츠의 대부분이 화면 밖에 있을 때, content-visibility을 활용해서 렌더링을 생략하게 되면 사용자의 초기 로드 시간이 훨씬 빨라집니다. 또한, 화면 내 콘텐츠와 더 빠르게 상호작용할 수 있습니다.

### CSS Containment

CSS Containment의 핵심이자 목적은 페이지 전체에서 DOM subtree의 분리를 제공하여 렌더링 성능을 향상시키는 것 입니다.

## 연속 공백 제거

``` css
  white-space: pre-wrap;
```

## styled-component anti-pattern

[!!!주의] SC props에 boolean 등 정해져있는 값이 아닌 string, number 등 임의의 값이 넘어가게되면 runtime에 class 를 매번 생성해서 효율이 확 떨어짐. 절대적으로 피해야할 anti-pattern 입니당.

변하는 값을 넘기면 런타임때 클래스를 생성하는 방식이라 계속 다른 클래스가 생성되버림

## && 이란?

## display: box일때, 우측정렬 -> float: right!

## CSS 선언시 정리 순서 -> 박스 모델 중심
[참고](https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/%EC%83%81%EC%9E%90_%EB%AA%A8%EB%8D%B8)

``` javascript
fontSize
fontWeight
position
top
left
...
display
margin
padding
width
height
border
...
background
color
...
```

관련된 애들끼리 모아놓은 걸 보실 수 있습니다. 읽기가 좋죠.
boxmodel 이외의  background, color와 같이 꾸며주는 애들은 좀 뒤로

## box 안에서 우측 버튼 고정에 나머지는 인풋과 같은 블락으로 채우고 싶은경우

부모 클래스에서 `display: flex;` 해주고 브라우저 크기에 따라 줄어들게 할 자식에서 `flex: auto`
이때 `width: 100%` 를 주면 의도치않게 동작

## overscroll-behavior

- https://developer.mozilla.org/en-US/docs/Web/CSS/overscroll-behavior

스크롤링이 끝났을때 브라우저에게 어떤 처리를 할지 설정해줌.

ex) 알림에서 스크롤 끝까지 갔을때 뒤쪽 브라우저 스크롤되지 않도록 처리할때 사용
`overscroll-behavior: contain;`

## px, em, rem 차이

[참고 문서](https://medium.com/watcha/watcha-%EA%B0%9C%EB%B0%9C-%EC%A7%80%EC%8B%9D-px-em-rem-f569c6e76e66)

- px로 font-size를 지정할 경우 미디어 쿼리나 자바스크립트를 사용하지 않는 이상 변경하기 매우 어려움. 반응형 웹 작업에서는 효율적이지 못함
- em은 font-size 기준으로 곱해서 계산한다
- font-size는 부모의 값을 상속하는 속성이기 때문에 em 을 사용할때 원하지 않는 결과가 나올 수 있음. 필요한 곳에만 사용하길

### rem

em과 마찬가지로 font-size에 비례하는 속성.
em과의 차이는 오직 html 태그의 글자 크기만 참조함.
계산하기 쉽게 글자 크기를 10픽셀로 맞추고 시작하는 경우가 많음.

## white-space

요소의 공백을 어떻게 처리할지에 대한 스타일

- normal → 여러 공백이나 줄바꿈을 하나의 공백으로 처리, 필요하다면 긴 줄을 줄바꿈처리함
- nowrap → 여러 공백이나 줄바꿈을 하나의 공백으로 처리. 긴 줄을 줄바꿈 처리하지 않음
- pre → 여러 공백을 그대로 처리. 긴 줄을 줄바꿈 하지 않음
- pre-wrap → 연속 공백 그대로 유지. 행의 줄바꿈은 행의 박스를 채우기 위해 필요한 경우 처리
- pre-line → 연속 공백 하나의 공백으로 처리. 행의 줄바꿈은 행의 박스를 채우기 위해 필요한 경우 처리
