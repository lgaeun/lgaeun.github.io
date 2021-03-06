---
title: "๐ Delve into TS environment - eslint, prettier, babel"
date: 2022-03-26 10:35:23 +0900
categories: [TIL]
tags: [typescript]
---

์ด๋ฒ์ js ํ๋ก์ ํธ๋ฅผ ts๋ก ๋ฐ๊พธ๋ ๊ฐ์๋ฅผ ๋ค์ผ๋ฉด์ typescript ํ๊ฒฝ์ ๋ํด ๊ถ๊ธํด์ ธ์ ์ ๋ฆฌํด ๋ณด๊ฒ ๋์๋ค.

# ESlint

- code level์์ ์๋ฌ๊ฐ ๋  ๋งํ ๋ถ๋ถ์ ์ง์ด์ค๋ค
- ๋ฌธ๋ฒ์ค๋ฅ์ฒดํฌ, ์๋์์ฑ, formatting ์ง์
- .eslintrc.{js, yml, json} ์ฌ๋ฌ๊ฐ์ง ํ์ฅ์๋ก ํ  ์ ์๋๋ฐ js๋ก ํ๋ฉด ์ฃผ์ ๋ฌ ์ ์์ด์ ์ข์

```js
module.exports = {
  root: true, //lint๊ฐ root:true๋ผ๊ณ  ์ง์ ํ๋ฉด ์ด ์์น๊น์ง๋ง configuration ํ์ผ๋ค์ ์ฐพ์
  env: { //ํ๋ก์ ํธ์ ์ฌ์ฉ ํ๊ฒฝ์ ์ค์ 
    browser: true,
    node: true,
  },
  extends: [
    'eslint:recommended', //eslint์ ๊ธฐ๋ณธ ๊ถ์ฅํ๋ ์ต์์ผ๋ก validation ํ๊ฒ ์
    'plugin:@typescript-eslint/eslint-recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  ignorePatterns: ["temp.js", "**/vendor/*.js"], //์ด ํ์ผ๋ค์ ๊ฑด๋๋
  plugins: ['react', 'prettier', '@typescript-eslint'], //
  rules: {
    'prettier/prettier': [ //prettier ์ค์  - eslint-plugin-prettier
      'error', //error level๋ก ์ค์ 
      {
        singleQuote: true, //prettier ๊ด๋ จ ์ค์ ์ ์๋์์ ์ค๋ช
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
    parser: '@typescript-eslint/parser', //tsํ์ผ์ ํ์ฑํ๊ธฐ ์ํด ๋ค์๊ณผ ๊ฐ์ parser๋ฅผ ์ฌ์ฉํ๊ฒ ๋ค.
  },
};
```

(1) extends ์ต์: 
  - ์์๋ฐ์ ๋ชจ๋  ํ์ผ configuration file์ ์ง์ ํ  ์ ์์
  - ์ฌ๋ฌ ๊ฐ๋ arrayํ์์ผ๋ก ์ ์ผ๋ฉด ๋
  - extends์์ ๊ธฐ๋ณธ์ ์ผ๋ก ๋ฐ๋ฅผ ํ์์ ์ ํด๋๊ณ , ์ดํ์ 'rules' option์์ override ํ  ์ ์์
  - eslint/recommended, eslint:all ์ด ์๋๋ฐ ํ์๋ ์ ์ฐ์ง ์์(์ ์ฐ๋๊ฒ ์์ ํจ)
  - `eslint-config` prefix๋ฅผ ์๋ตํ  ์ ์์
  ```js
  // example
  extends: ['eslint-config-airbnb', 'eslint-config-standard'] 
  extends: ['airbnb', 'standard']//์์ ๋์ผํจ
  ```
(2) rules ์ต์:
  - ๊ท์น๋ค์ override(๋๋ ํ์ฅ) ํ  ์ ์์
  ```js
  "rules": {
        // enable additional rules
        "indent": ["error", 4], // indent 4
        "linebreak-style": ["error", "unix"],
        "quotes": ["error", "double"], //double quote๋ฉด error๋ก
        "semi": ["error", "always"], //semi colon ํญ์ - ์์ผ๋ฉด error

        // override configuration set by extending "eslint:recommended"
        "no-empty": "warn",
        "no-cond-assign": ["error", "always"],

        // disable rules from base configurations
         "for-direction": "off",
    }
  ```
  ์๋์ฒ๋ผ ๊ฐ์ฒดํ์์ผ๋ก ์ ์ด๋ ๋. array์ ์ฒซ ๋ฒ์งธ ์์๋ 'error'์ฒ๋ผ ์ ์ด๋ ๋์ง๋ง ์ซ์๋ก ์ ์ด๋ ๋.  
  0=off, 1=warn, 2=error
  ```js
  "max-lines": ["error", { "max": 100 }]
  "react/jsx-filename-extension": [2, { "extensions": [".jsx", ".tsx"] }],
  ```

(3) plugin ์ต์:
  - eslint์ ์ถ๊ฐํ๊ณ  ์ถ์ npm package
  - ๋ง์ฐฌ๊ฐ์ง๋ก `eslint-plugin-` prefix๋ฅผ ์์ ์๋ตํ  ์ ์์
  ( `react` === `eslint-plugin-react`)

๊ทธ ์ธ์ ๊ต์ฅํ ๋ง์ rule ๋ค์ ์ง์ ํ  ์ ์๋๋ฐ [ํํ์ด์ง](https://eslint.org/docs/rules/) ์ฐธ๊ณ .  

๊ทธ๋ฆฌ๊ณ  prettier์ ํจ๊ป ์ฐ๋ฉด eslint ์์ฒด์์๋ formattingํ๋ ๊ธฐ๋ฅ์ด ์๊ธฐ ๋๋ฌธ์ conflict๊ฐ ์๊ธด๋ค. ๋ฐ๋ผ์ plugin๋ค์ ์ค์นํด์ eslint์ formatting์ disableํด์ฃผ๊ณ , prettier์๊ฒ ๋ชจ๋  formatting์ ์ผ์ํด์ค ์ ์๋ค. 
  - **eslint-config-prettier**: eslint์ prettier์ ์ถฉ๋๋๋ formatting ๋นํ์ฑํ
  - **eslint-plugin-prettier**: prettier๋ฅผ eslint์ plugin์ผ๋ก ์ถ๊ฐํด์ ์ฌ์ฉํ๊ธฐ ์ํจ  


์ถ๊ฐ๋ก prettier ๊ณต์ document์์๋ **eslint-plugin-prettier** ํ๋ฌ๊ทธ์ธ์ ์ฌ์ฉํ๋ ๊ฒ **generally not recommended**๋ผ๊ณ  ๋ค์๊ณผ ๊ฐ์ ์ด์ ๋ก ์จ์๊ธด ํ๋ค. 

    - ์ง์ ์ ์ผ๋ก prettier์ ๋๋ ธ์ ๋๋ณด๋ค ๋๋ฆฌ๋ค
    - ์๋ฌ ๋ผ์ธ์ด ๋๋ฌด ๋ง์์ง ์ ์๋ค(?)


# Prettier
๋ณดํต .prettierrc ํ์ผ์ ์ถ๊ฐํด์ ์ฌ์ฉํ๋ฉด ๋์ง๋ง, eslint์ plugin ๊น์์ ๊ฑฐ๊ธฐ์ ์ค์ ํด์ค๋ ๋๋ค.
- ํ ๋จ์ ์ฝ๋ฉ ์ปจ๋ฒค์์ ์ ์ํ  ๋ ์ฌ์ฉํ๋ ๋๊ตฌ
- ๋ณดํต ์ด์ ๋ ์ํํด๋๊ณ , ํ์์ ํ์ํด์ ์ถ๊ฐ/์ญ์ ํ๋ฉด ๋๋ค
```js
{
    "singleQuote": true, // ๋ฌธ์์ด์ ๋ฐ์ดํ๋ก formatting
    "semi": true, //์ฝ๋ ๋ง์ง๋ง์ ์ธ๋ฏธ์ฝ๋ฅธ์ด ์๊ฒ formatting
    "useTabs": false, //ํญ์ ์ฌ์ฉ์ ๊ธํ๊ณ  ์คํ์ด์ค๋ฐ ์ฌ์ฉ์ผ๋ก ๋์ฒดํ๊ฒ formatting
    "tabWidth": 2, // ๋ค์ฌ์ฐ๊ธฐ ๋๋น๋ 2์นธ
    "trailingComma": 'all', // ๊ฐ์ฒด๋ ๋ฐฐ์ด ํค:๊ฐ ๋ค์ ํญ์ ์ฝค๋ง๋ฅผ ๋ถํ๋๋ก formatting
    "printWidth": 120, // ์ฝ๋ ํ์ค์ด maximum 120์นธ
    "arrowParens": 'avoid', // ํ์ดํ ํจ์๊ฐ ํ๋์ ๋งค๊ฐ๋ณ์๋ฅผ ๋ฐ์ ๋ ๊ดํธ๋ฅผ ์๋ตํ๊ฒ formatting
}
```

# Babel
- javascript compiler(์ต์  js ๋ฌธ๋ฒ์ด ์ต๋ํ ๋ง์ ๋ธ๋ผ์ฐ์ ์ ํธํ๋  ์ ์๋๋ก ๋ฐ๊ฟ์ฃผ๋ ๋๊ตฌ)  





----
reference  

  [Eslint configuration doc](https://eslint.org/docs/user-guide/configuring/)  
  [TS๊ฐ์ - section.5 ํ์  ํ๊ฒฝ ๊ตฌ์ฑ](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8B%A4%EC%A0%84/dashboard)  
  [ESLint, Prettier ์ ์ฉํ๊ธฐ](https://velog.io/@recordboy/ESLint-Prettier-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)