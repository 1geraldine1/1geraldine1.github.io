---
title: "Page_build_failure"
date: 2021-10-12T22:30:00-04:00
categories:
  - '2021-10 TIL'
tags:
  - '20211012'
  - Github.io 오류
  - 'TIL'
---


# Intro

* 한동안 글 작성하기에만 정신이 급급해서 정작 블로그에 제대로 글이 올라갔는지조차 확인을 안하고 있었는데, 네이버 메일에 Github로부터 다음 내용의 메일이 산더미같이 쌓여있었다.

  > The page build failed for the `master` branch with the following error:
  > Unable to build page. Please try again later.
  >
  >For information on troubleshooting Jekyll see:
  >https://docs.github.com/articles/troubleshooting-jekyll-builds
  >
  >If you have any questions you can submit a request at https://support.github.com/contact?tags=dotcom-pages&repo_id=399015564&page_build_id=285680920
  >

## 원인

* github의 파일 크기 제한이 원인이었다.

* 깃허브에 블로그에 사용되는 이미지들을 저장했고, 특히 이 오류가 나기 시작한 22일차부터는 데이터모델 테스트를 위해 여러장의 사진을 업로드하던 때였다.

* 확인해보니 images 폴더가 48MB인것을 확인할수 있었다.

* [관련 docs](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github)에 따르면, Git에서 한번에 업로드 할 수 있는 파일크기의 제한은 약 50MB라고 한다.

  * 아무래도 매번 이미지를 커밋하며 업데이트를 하는것이 이미지 폴더 전체를 갱신하는 방식으로 진행되는것인지, 해당 부분에 걸려 오류가 발생하는것.

## 해결

* 