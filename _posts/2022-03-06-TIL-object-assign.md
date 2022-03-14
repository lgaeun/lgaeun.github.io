---
title: "☀️ 3/6 - Object.assign()"
date: 2022-03-06 10:32:00 +0900
categories: [TIL]
tags: [javascript]
---

## 객체 복사 by Object.assign()

같은 속성(key)가 있다면, 새로운 값으로 덮어쓰고, 아니라면 새로 추가해서 복사한다.
같은 레퍼런스를 같도록 만든다.

```js
const target = { a: 1, b: 2 };
const object = { b: 4, c: 2 };

const copy = Object.assign(target, object); //target값이 변화

console.log(target); // {a:1, b:4, c:2}
console.log(copy); // {a:1, b:4, c:2}
console.log(target === copy); // true
```

여러 개도 가능

```js
const target = { a: 1, b: 2 };
const sources = [
  { b: 4, c: 5 },
  { b: 6, c: 7, d: 8 },
  { b: 9, c: 10, d: 11 },
  { b: 12, c: 13, d: 14, e: 15 },
];

Object.assign(target, ...sources);
Object.assign(target, sources[0], sources[1], sources[2], sources[3]); //same

//리스트를 그대로 assign한다면(X), index를 키로 갖는 속성을 새로 추가해버림
```

깊은 복사는 이루어지지 않는다

## Spread 연산자와 비교

```js
{...obj}
Object.assign({}, obj)
```

기본적으로 아래와 위 코드는 동일하다

다만, Objec.assign(obj1, obj2) 는 obj1의 원본값을 변화시키므로

값이 동일한 다른 객체를 생성하려면 반드시 첫 번째 파라미터로 {} 빈 객체를 넘겨주어야 한다.

따라서 불변성(immutability)를 유지하려면, spread 쓰는 것을 권장
