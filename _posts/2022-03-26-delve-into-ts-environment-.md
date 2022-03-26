---
title: "🌀 Delve into TS environment - eslint, prettier, babel"
date: 2022-03-26 10:35:23 +0900
categories: [TIL]
tags: [typescript]
---

이번에 js 프로젝트를 ts로 바꾸는 강의를 들으면서 typescript 환경에 대해 궁금해져서 정리해 보게 되었다.

# ESlint

- code level에서 에러가 날 만한 부분을 짚어준다
- 문법오류체크, 자동완성, formatting 지원
- .eslintrc.{js, yml, json} 여러가지 확장자로 할 수 있는데 js로 하면 주석 달 수 있어서 좋음

```js
module.exports = {
  root: true, //lint가 root:true라고 지정하면 이 위치까지만 configuration 파일들을 찾음
  env: { //프로젝트의 사용 환경을 설정
    browser: true,
    node: true,
  },
  extends: [
    'eslint:recommended', //eslint의 기본 권장하는 옵션으로 validation 하겠음
    'plugin:@typescript-eslint/eslint-recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  ignorePatterns: ["temp.js", "**/vendor/*.js"], //이 파일들은 건너뜀
  plugins: ['react', 'prettier', '@typescript-eslint'], //
  rules: {
    'prettier/prettier': [ //prettier 설정 - eslint-plugin-prettier
      'error', //error level로 설정
      {
        singleQuote: true, //prettier 관련 설정은 아래에서 설명
        semi: true,
        useTabs: false,
        tabWidth: 2,
        printWidth: 80,
        bracketSpacing: true,
        arrowParens: 'avoid',
      },
    ],
  },
  parserOptions: {
    parser: '@typescript-eslint/parser', //ts파일을 파싱하기 위해 다음과 같은 parser를 사용하겠다.
  },
};
```

(1) extends 옵션: 
  - 상속받을 모든 파일 configuration file을 지정할 수 있음
  - 여러 개는 array형식으로 적으면 됌
  - extends에서 기본적으로 따를 형식을 정해놓고, 이후에 'rules' option에서 override 할 수 있음
  - eslint/recommended, eslint:all 이 있는데 후자는 잘 쓰지 않음(안 쓰는게 안전함)
  - `eslint-config` prefix를 생략할 수 있음
  ```js
  // example
  extends: ['eslint-config-airbnb', 'eslint-config-standard'] 
  extends: ['airbnb', 'standard']//위와 동일함
  ```
(2) rules 옵션:
  - 규칙들을 override(또는 확장) 할 수 있음
  ```js
  "rules": {
        // enable additional rules
        "indent": ["error", 4], // indent 4
        "linebreak-style": ["error", "unix"],
        "quotes": ["error", "double"], //double quote면 error로
        "semi": ["error", "always"], //semi colon 항상 - 없으면 error

        // override configuration set by extending "eslint:recommended"
        "no-empty": "warn",
        "no-cond-assign": ["error", "always"],

        // disable rules from base configurations
         "for-direction": "off",
    }
  ```
  아래처럼 객체형식으로 적어도 됌. array의 첫 번째 원소는 'error'처럼 적어도 되지만 숫자로 적어도 됌.  
  0=off, 1=warn, 2=error
  ```js
  "max-lines": ["error", { "max": 100 }]
  "react/jsx-filename-extension": [2, { "extensions": [".jsx", ".tsx"] }],
  ```

(3) plugin 옵션:
  - eslint에 추가하고 싶은 npm package
  - 마찬가지로 `eslint-plugin-` prefix를 앞에 생략할 수 있음
  ( `react` === `eslint-plugin-react`)

그 외에 굉장히 많은 rule 들을 지정할 수 있는데 [홈페이지](https://eslint.org/docs/rules/) 참고.  

그리고 prettier와 함께 쓰면 eslint 자체에서도 formatting하는 기능이 있기 때문에 conflict가 생긴다. 따라서 plugin들을 설치해서 eslint의 formatting을 disable해주고, prettier에게 모든 formatting을 일임해줄 수 있다. 
  - **eslint-config-prettier**: eslint의 prettier와 충돌나는 formatting 비활성화
  - **eslint-plugin-prettier**: prettier를 eslint에 plugin으로 추가해서 사용하기 위함  


추가로 prettier 공식 document에서는 **eslint-plugin-prettier** 플러그인을 사용하는 게 **generally not recommended**라고 다음과 같은 이유로 써있긴 하다. 

    - 직접적으로 prettier을 돌렸을 때보다 느리다
    - 에러 라인이 너무 많아질 수 있다(?)


# Prettier
보통 .prettierrc 파일을 추가해서 사용하면 되지만, eslint에 plugin 깔아서 거기서 설정해줘도 된다.
- 팀 단위 코딩 컨벤션을 정의할 때 사용하는 도구
- 보통 이정도 셋팅해두고, 팀에서 협의해서 추가/삭제하면 된다
```js
{
    "singleQuote": true, // 문자열은 따옴표로 formatting
    "semi": true, //코드 마지막에 세미콜른이 있게 formatting
    "useTabs": false, //탭의 사용을 금하고 스페이스바 사용으로 대체하게 formatting
    "tabWidth": 2, // 들여쓰기 너비는 2칸
    "trailingComma": 'all', // 객체나 배열 키:값 뒤에 항상 콤마를 붙히도록 formatting
    "printWidth": 120, // 코드 한줄이 maximum 120칸
    "arrowParens": 'avoid', // 화살표 함수가 하나의 매개변수를 받을 때 괄호를 생략하게 formatting
}
```

# Babel
- javascript compiler(최신 js 문법이 최대한 많은 브라우저에 호환될 수 있도록 바꿔주는 도구)  





----
reference  

  [Eslint configuration doc](https://eslint.org/docs/user-guide/configuring/)  
  [TS강의 - section.5 플젝 환경 구성](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8B%A4%EC%A0%84/dashboard)  
  [ESLint, Prettier 적용하기](https://velog.io/@recordboy/ESLint-Prettier-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)