---
title: "Minimal-mistake에서의 Latex 설정 및 그외의 세부 설정"
date: 2021-08-23T18:08:30-04:00
categories:
  - '2022-06 TIL'
tags:
  - '20220610'
  - 'Minimal-mistake'
  - 'Github.io'
  - 'Minimal-mistake'
  - 'Latex'
---

# 개요

* 요즘 다루는 글들에 수식을 쓸 일이 많아서 마크다운에서 수식을 적을수 있는 [LaTeX](https://en.wikipedia.org/wiki/LaTeX)의 문법을 사용하는 일들이 많았다.
* 블로그 글이 커밋 직후에 바로 갱신이 안되는 일이 많아 글 확인을 Github로만 하고 있느라 블로그에 LaTeX문법이 적용 안되는것을 뒤늦게 확인하고, 해당 사항을 수정하기로 했다.

# Jekyll

* 우선, 이 블로그는 GithubPage이고, Jekyll을 기반으로 만들어졌다.

* Jekyll은 마크다운 언어를 기반으로 글을 작성해야 하므로, 이 블로그에서 [초창기에 쓴 포스트](https://1geraldine1.github.io/2021-08%20til/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4-%EB%AC%B8%EB%B2%95/) 역시 마크다운 언어 공부 글 이었다.

* Jykell은 간단하게 블로그를 제작할수 있도록 유저들이 제작한 테마들을 공유하는 사이트가 있다.([1](https://github.com/topics/jekyll-theme), [2](http://jekyllthemes.org/))
  * 이 블로그의 경우 [Minimal-mistake](https://github.com/mmistakes/minimal-mistakes) 라는 테마로 제작되었다.

# Minimal-mistake

* [소개 페이지](https://mmistakes.github.io/minimal-mistakes/), [공식 docs](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)

* 공식 docs를 뒤져보았지만 내 문제의 해결책은 마땅히 찾지 못했고, 대신 몇가지 블로그에 흥미로운 기능들이 보여 기록하기로 했다.

  * [작성일 표시](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#post-dates)
  
  * [댓글 기능 추가](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#comments)
  
  * [미리보기 추가](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#site-default-teaser-image)

  * [블로그 내 검색기능](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#site-search)

  * [검색 엔진 최적화](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#seo-social-sharing-and-analytics-settings)
    * 당장은 내 블로그를 검색하여 나오게 할 생각이 없어 따로 추가하지는 않았으나, 관심이 고프게 되면 언젠가는 하게될것같아 기록해둔다.


# Minimal-mistake Latex 적용

* 결국, 원하던 답은 [다른 블로그 글](https://www.janmeppe.com/blog/How-to-add-mathjax-to-minimal-mistakes/)에서 얻을수 있었다.

* 이하의 방법은 위 블로그 글의 방법을 번역한것 + 실행하면서 얻은 내용들을 기반으로 작성했음을 밝힌다.

  ### 1. markdown엔진 kramdown으로 설정  
     * _config.yml 내부에서의 설정을 다음과 같이 변경한다.
        ```yml
        # Build settings
        markdown: kramdown
        remote_theme: mmistakes/minimal-mistakes
        ``` 
  ### 2. scripts.html 복사해오기
    * [minimal-mistake의 원본 레포지토리](https://github.com/mmistakes/mm-github-pages-starter)에서 <B>\_include</B> 폴더 내부에 있는 scripts.html 파일을 복사한다.

    * 내 블로그 레포지토리에도 동일하게 _include폴더를 생성하여 안에 복사해온 scripts.html파일을 넣는다.

  ### 3. scripts.html 수정

    * scripts.html 파일에 다음의 코드를 추가한다.

      ```html
        <script type="text/javascript" async
          src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML">
        </script>

        <script type="text/x-mathjax-config">
          MathJax.Hub.Config({
            extensions: ["tex2jax.js"],
            jax: ["input/TeX", "output/HTML-CSS"],
            tex2jax: {
              inlineMath: [ ['$','$'], ["\\(","\\)"] ],
              displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
              processEscapes: true
            },
            "HTML-CSS": { availableFonts: ["TeX"] }
          });
        </script>

      ```

    * 해당 코드는 [Mathjax](https://en.wikipedia.org/wiki/MathJax)를 웹페이지에서 사용할수 있도록 하는 코드이다.

    * 모든 블로그의 포스트에 이 scripts.html의 내용이 적용되기 때문에 Mathjax가 모든 포스트에서 활성화된다.

# 적용 결과

* $R^2 = \frac{\Sigma_{i=1}^{n}(\hat{y}-\mu)^2}{\Sigma_{i=1}^{n}(y-\mu)^2}$

  * 회귀분석에서 사용되는 결정계수 공식을 가져왔다.

* 수식이 정상적으로 출력되는것을 확인할수 있다.

