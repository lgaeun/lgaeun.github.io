---
title: "🌀 3/7 TS - 점진적으로 적용하기 (2) - JSDoc으로 js에서 type check하기"
date: 2022-03-07 10:55:00 +0900
categories: [TIL]
tags: [typescript]
---

순수 js코드에 다음과 같은 주석을 추가하면 type 체크가 가능하다.

```js
// @ts-check
```

이는 JSDoc을 이용하면 타입에 대한 힌트를 제공할 수 있다

## JSDoc이란?

자바스크립트 API 문서 생성기로, API를 설명하는 HTML을 생성할 수 있다. 일반 주석과 마찬가지로 무시됌.

1 변수타입

```js
/**
 * @type {string}
 */
let str;
```

2 함수타입

```js
// TypeScript syntax를 사용하는 방법
/**
 * @type {(a:number, b: number) => number}
 */
const add = (a, b) => a + b;

// Closure syntax를 사용하는 방법
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

3 타입 정의 - 복잡한 타입을 정의할 때 사용한다

```js
/**
 * 할 일
 * @typedef {Object} Todo
 * @property {number} id - 할일 id
 * @property {string} content - 할일 내용
 * @property {boolean} completed - 할일 완료 여부
 */

/**
 * 할일 목록
 * @typedef {Todo[]}
 */
const todos = [
  { id: 1, content: "HTML", completed: false },
  { id: 2, content: "CSS", completed: true },
];
```

4 `@callback`
: @typedef와 유사하지만 object 타입 대신 특정한 function 타입을 지정한다.
