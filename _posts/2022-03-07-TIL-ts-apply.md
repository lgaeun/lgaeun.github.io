---
title: "🌀 3/7 TS -  점진적으로 적용하기 (1)"
date: 2022-03-07 10:32:00 +0900
categories: [TIL]
tags: [typescript]
---

## JS 코드에 TS를 적용할 때 주의할 점

- 기능적인 변경은 절대 X
- 테스트 커버리지가 낮을 땐 함부로 ts 적용하지 말 것
- 점진적으로 strict 레벨을 증가시킬 것 (처음부터 엄격하게 타입 적용 x)

## TS를 점진적으로 적용하는 방법

( 0. 순수 JS : JSDoc을 이용해 순수 JS 코드에 힌트를 제공하기 )

1. ts 환경 설정 및 .ts 파일로 변환
2. any 타입 선언
3. any 타입을 더 적절한 타입으로 변경

### 1. typescript 프로젝트 환경 구성

- 프로젝트 생성 후 `npm init -y` 로 package.json 생성
- `npm i typescript -D` 로 타입스크립트 라이브러리 생성
- 타입스크립트 설정파일 tsconfig.json을 생성하고 기본값 추가하기
  ```jsx
  {
    "compilerOptions": {
      "allowJs": true,
      "target": "ES5",
      "outDir": "./dist",
      "moduleResolution": "Node",
      "lib": ["ES2015", "DOM", "DOM.Iterable"]
    },
    "include": ["./src/**/*"],
    "exclude": ["node_modules", "dist"]
  }
  ```
- 서비스 코드가 포함된 .js → .ts 로 변환 (app.js → app.ts)
- 타입스크립트 컴파일 명렁어 tsc 로 타입스크립트 파일을 자바스크립트 파일로 변환하기

### 2. 엄격하지 않은 타입 환경(loose type)에서 프로젝트 돌려보기

- 테스트 코드가 있다면 테스트 코드가 통과하는지 먼저 확인
- 모든 js 파일 → ts 파일
- 컴파일 에러 나는 것들 위주로만 에러 잡기 (**여기서 기능을 사소하게라도 변경하지 않도록 주의**)
- 테스트 코드가 성공하는지 확인

### 3. 명시적인 any 선언하기

- 타입스크립트 설정파일에 `noImplicitAny: true` 추가하기
- 가능한 타입을 적용할 수 있는 모든 곳에 타입을 적용하기
  - library를 쓰는 경우 [DefinitelyTyped](https://definitelytyped.org/)에서 `@types` 관련 라이브러리를 찾아 설치한다.
- 타입을 정하기 어려운 곳이 있으면 명시적으로라도 `any` 선언하기

### 4. strict 모드 설정하기

- 타입스크립트 설정 파일에 아래 설정을 추가한다

```jsx
{
  "strict": true,
  "strictNullChecks": true,
  "strictFunctionTypes": true,
  "strictBindCallApply": true,
  "strictPropertyInitialization": true,
  "noImplicitThis": true,
  "alwaysStrict": true,
}
```

- `any`로 되어있는 타입을 최대한 더 적절한 타입으로 변환
- `as` 와 같은 키워드를 최대한 사용하지 않도록 고민해서 변경한다

## Q.

- 테스트코드 작성

[reference](https://joshua1988.github.io/ts/etc/convert-js-to-ts.html#자바스크립트-프로젝트에-타입스크립트-적용하는-절차)
