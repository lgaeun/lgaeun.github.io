---
title: "[Jekyll] Chirpy theme - push시 blank page만 뜨는 이슈 해결해보기 "
date: 2022-03-14 15:27:09 +0900
categories: [TIL]
tags: [jekyll]
---

## 서문

---

원래 스케쥴러, 일기 등 무언가를 잘 적지 않는 편이지만 요즘 기록의 중요성을 실감했다. 이제부터 휘발성인 기억을 믿는다면 내가 바보다. 조리 있게 글을 잘 적는 편도 아니고 누군가가 내 글을 읽을 수 있다는 것이 아직은 부끄럽다. 그럼에도 정제가 덜 된 글이라도 일단 적기 시작해보려 한다. 그게 이 소소한 블로그를 다시 시작한 이유이다.

근데 github에 push 후 `{username}.github.io` 에 들어가면 이렇게 빈 화면만 뜨는데..환장..
![screenshot](/assets/img/posts/screenshot.png)

화가 나버려..
그렇지만 좌절하지 않는다.
역시나 구글링으로 해결할 수 없는 문제는 없었다.
해결 과정 또한 기록으로 남겨놓는다. (나와 같은 이슈를 겪은 사람들은 더 빨리 해결하기를..)

<br/>

## 해결방법

---

1. repository에서 브랜치명을 `main` -> `master`로 변경한다. `pages-deploy.yml`에서도 마찬가지로 변경한다. 이 파일은 `.github > workflows` 디렉토리 안에 있음. (없으면 [tutorial]('https://chirpy.cotes.page/posts/getting-started/#deploy-by-using-github-actions') 다시 읽고 생성해보길)
   <br/>

   ```yml
   name: "Automatic build"
   on:
   push:
     branches:
       - master # 이 부분을 main -> master로 변경
     paths-ignore:
       - .gitignore
       - README.md
       - LICENSE
   ```

   우선 나는 chirpy-starter를 이용해 블로그를 구축하였는데, 이 때 default 브랜치명이 `main`으로 설정된다. Chirpy의 버그인지, 브랜치명이 main이면 제대로 동작하지 않고 반드시 `master`여야 하나보다.

2. push를 하고 나면 `gh-pages`라는 브랜치가 생성되어 있다. repository setting > Pages > GitHub Pages 설정에 들어가서 다음과 같이 소스 브랜치를 `gh-pages`로 바꿔 주고 <kbd>Save</kbd> 버튼을 누르면 끝이다.
   <br/>

   ![GH-PAGES](/assets/img/posts/gh-pages.png){: w="600" h="400"}

<br/>
<br/>
## 레퍼런스
-----

[참고한 사이트1]('https://github.com/cotes2020/jekyll-theme-chirpy/issues/502')

[참고한 사이트2]('https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site')
