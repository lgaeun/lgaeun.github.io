---
title: "🌀 3/16 TS - DOM 함수 타입 오류 해결하기 (ref. ts:2740)"
date: 2022-03-16 12:35:23 +0900
categories: [TIL]
tags: [typescript]
---

## DOM Element type

```jsx
function $(selector: string) {
  return document.querySelector(selector);
}

const confirmedTotal = $(".confirmed-total");
const deathsTotal = $(".deaths");
const recoveredTotal = $(".recovered");
```

위와 같은 util 함수를 작성했을 때, 반환되는 타입은 `Element`인 것을 알 수 있다.

querySelectyor로 가져온 DOM Element의 타입은 어떻게 될까?

타입을 단언해주지 않으면 다음과 같은 메소드를 사용할 때 에러가 발생한다.

```jsx
deathsTotal.innerText = data[0].Cases; // error here(ts:2740)
```

## Solution

DOM element의 타입은 다음과 같이 extend될 수 있다. 따라서 tag의 종류에 따라 아래와 같이 type을 단언해주면 에러가 없어진다.

```jsx
// Dom Element의 type들
var DomElement: Element | HTMLElement | HTMLParagraphElement;

// wrong solution - 타입 간에 호환 할 수 없기 때문에 여전히 에러
const confirmedTotal: HTMLSpanElement = $(".confirmed-total"); //<span>
const deathsTotal: HTMLParagraphElement = $(".deaths"); //<p>
const recoveredTotal: HTMLParagraphElement = $(".recovered"); //<p>

// correct solution
const confirmedTotal = $(".confirmed-total") as HTMLSpanElement; //<span>
const deathsTotal = $(".deaths") as HTMLParagraphElement; //<p>
const recoveredTotal = $(".recovered") as HTMLParagraphElement; //<p>
```

또한 앞으로 `as`를 이용해 type 단언 해주는 경우가 많아지면 util함수로 저 부분을 빼서 코드를 더 깔끔하게 작성할 수도 있다.

> [TS강의](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8B%A4%EC%A0%84/dashboard)를 들으며 정리한 내용입니다.
