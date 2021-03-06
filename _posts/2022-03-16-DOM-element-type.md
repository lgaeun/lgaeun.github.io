---
title: "๐ 3/16 TS - DOM ํจ์ ํ์ ์ค๋ฅ ํด๊ฒฐํ๊ธฐ (ref. ts:2740)"
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

์์ ๊ฐ์ util ํจ์๋ฅผ ์์ฑํ์ ๋, ๋ฐํ๋๋ ํ์์ `Element`์ธ ๊ฒ์ ์ ์ ์๋ค.

querySelectyor๋ก ๊ฐ์ ธ์จ DOM Element์ ํ์์ ์ด๋ป๊ฒ ๋ ๊น?

ํ์์ ๋จ์ธํด์ฃผ์ง ์์ผ๋ฉด ๋ค์๊ณผ ๊ฐ์ ๋ฉ์๋๋ฅผ ์ฌ์ฉํ  ๋ ์๋ฌ๊ฐ ๋ฐ์ํ๋ค.

```jsx
deathsTotal.innerText = data[0].Cases; // error here(ts:2740)
```

## Solution

DOM element์ ํ์์ ๋ค์๊ณผ ๊ฐ์ด extend๋  ์ ์๋ค. ๋ฐ๋ผ์ tag์ ์ข๋ฅ์ ๋ฐ๋ผ ์๋์ ๊ฐ์ด type์ ๋จ์ธํด์ฃผ๋ฉด ์๋ฌ๊ฐ ์์ด์ง๋ค.

```jsx
// Dom Element์ type๋ค
var DomElement: Element | HTMLElement | HTMLParagraphElement;

// wrong solution - ํ์ ๊ฐ์ ํธํ ํ  ์ ์๊ธฐ ๋๋ฌธ์ ์ฌ์ ํ ์๋ฌ
const confirmedTotal: HTMLSpanElement = $(".confirmed-total"); //<span>
const deathsTotal: HTMLParagraphElement = $(".deaths"); //<p>
const recoveredTotal: HTMLParagraphElement = $(".recovered"); //<p>

// correct solution
const confirmedTotal = $(".confirmed-total") as HTMLSpanElement; //<span>
const deathsTotal = $(".deaths") as HTMLParagraphElement; //<p>
const recoveredTotal = $(".recovered") as HTMLParagraphElement; //<p>
```

๋ํ ์์ผ๋ก `as`๋ฅผ ์ด์ฉํด type ๋จ์ธ ํด์ฃผ๋ ๊ฒฝ์ฐ๊ฐ ๋ง์์ง๋ฉด utilํจ์๋ก ์  ๋ถ๋ถ์ ๋นผ์ ์ฝ๋๋ฅผ ๋ ๊น๋ํ๊ฒ ์์ฑํ  ์๋ ์๋ค.

> [TS๊ฐ์](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8B%A4%EC%A0%84/dashboard)๋ฅผ ๋ค์ผ๋ฉฐ ์ ๋ฆฌํ ๋ด์ฉ์๋๋ค.
