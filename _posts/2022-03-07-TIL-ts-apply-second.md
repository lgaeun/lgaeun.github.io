---
title: "๐ 3/7 TS - ์ ์ง์ ์ผ๋ก ์ ์ฉํ๊ธฐ (2) - JSDoc์ผ๋ก js์์ type checkํ๊ธฐ"
date: 2022-03-07 10:55:00 +0900
categories: [TIL]
tags: [typescript]
---

์์ js์ฝ๋์ ๋ค์๊ณผ ๊ฐ์ ์ฃผ์์ ์ถ๊ฐํ๋ฉด type ์ฒดํฌ๊ฐ ๊ฐ๋ฅํ๋ค.

```js
// @ts-check
```

์ด๋ JSDoc์ ์ด์ฉํ๋ฉด ํ์์ ๋ํ ํํธ๋ฅผ ์ ๊ณตํ  ์ ์๋ค

## JSDoc์ด๋?

์๋ฐ์คํฌ๋ฆฝํธ API ๋ฌธ์ ์์ฑ๊ธฐ๋ก, API๋ฅผ ์ค๋ชํ๋ HTML์ ์์ฑํ  ์ ์๋ค. ์ผ๋ฐ ์ฃผ์๊ณผ ๋ง์ฐฌ๊ฐ์ง๋ก ๋ฌด์๋.

1 ๋ณ์ํ์

```js
/**
 * @type {string}
 */
let str;
```

2 ํจ์ํ์

```js
// TypeScript syntax๋ฅผ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ
/**
 * @type {(a:number, b: number) => number}
 */
const add = (a, b) => a + b;

// Closure syntax๋ฅผ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ
/**
 * @type {function(number, number): number}
 */
const multiply = (a, b) => a * b;

/**
 * @param {string} p1 - A string of param
 * @param {string=} p2 - An optional param(Closure syntax)
 * @param {string} [p3] - Another optional param (JSDoc syntax)
 * @param {string} [p4="test"] - An optional param with a default value
 * @return {string} This is the result
 */
function stringsStringStrings(p1, p2, p3, p4) {
  //...
}
```

3 ํ์ ์ ์ - ๋ณต์กํ ํ์์ ์ ์ํ  ๋ ์ฌ์ฉํ๋ค

```js
/**
 * ํ  ์ผ
 * @typedef {Object} Todo
 * @property {number} id - ํ ์ผ id
 * @property {string} content - ํ ์ผ ๋ด์ฉ
 * @property {boolean} completed - ํ ์ผ ์๋ฃ ์ฌ๋ถ
 */

/**
 * ํ ์ผ ๋ชฉ๋ก
 * @typedef {Todo[]}
 */
const todos = [
  { id: 1, content: "HTML", completed: false },
  { id: 2, content: "CSS", completed: true },
];
```

4 `@callback`
: @typedef์ ์ ์ฌํ์ง๋ง object ํ์ ๋์  ํน์ ํ function ํ์์ ์ง์ ํ๋ค.
