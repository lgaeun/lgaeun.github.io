---
title: "๐ Event, Axios type ์ ์"
date: 2022-03-23 12:32:01 +0900
categories: [TIL]
tags: [typescript]
---
## ํ๋ผ๋ฏธํฐ ํ์๋ค ์ ์ํ๊ธฐ

parameter, return value๋ฑ์ ๋ํด ๋ฐ๋ก ๋นผ์ interface๋ type์ผ๋ก ์ ์ํด์ ์ฌ์ฉํ๋ฉด ๋๋ค.

## Event type

```jsx
function initEvents() {
  list.addEventListener('click', handleListClick);
}

async function handleListClick(event: any) {
 // ...
}
```

์์ click ์ด๋ฒคํธ์ด๋ฏ๋ก MouseEvent๋ก ๋ฐ๊ฟ ์ ์๋ค.

```jsx
async function handleListClick(event: MouseEvent) {
 // ...
}
```

์ด๋ฒคํธ ํ์์ event์์ ๋ง์ฐ์ค๋ฅผ ์ฌ๋ฆฌ๋ฉด ์ ์ ์๋ค.

![Untitled](../assets/img/posts/2022-03-23/1.png)

## Axios

Promise๋ฅผ ๋ฆฌํดํ๋ ํจ์๋ Promise<AxiosResponse<< **Type** >> ์ผ๋ก ์ ์ํด์ฃผ๋ฉด ๋๋ค.

------


> [TS๊ฐ์](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8B%A4%EC%A0%84/dashboard)๋ฅผ ๋ค์ผ๋ฉฐ ์ ๋ฆฌํ ๋ด์ฉ์๋๋ค.
