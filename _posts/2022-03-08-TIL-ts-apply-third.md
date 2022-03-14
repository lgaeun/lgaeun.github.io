---
title: "🌀 3/8 TS -  점진적으로 적용하기 (3)"
date: 2022-03-08 9:32:00 +0900
categories: [TIL]
tags: [typescript]
---

- 일단 any로 설정을 해둔 후, 조금 더 적절한 타입으로 바꿔나가기
- string, any 등도 가능하지만 타입의 값이 한정된 경우, 직접 타입 선언하는 것도 좋다

  ```jsx
  enum CovidStatus {
  	Confirmed = 'confirmed',
  	Deaths = 'deaths',
  	Recovered = 'recovered'
  }

  const fetchCovidCountry(id: string, status: CovidStatus): string {
     //...
  }
  ```

- new Date(), getTime() 등과 같은 내장 js 라이브러리 같은 경우는 자동으로 타입이 추론된다.
