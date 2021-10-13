---
title: "Page_build_failure"
date: 2021-10-13T18:30:00-04:00
categories:
  - '2021-10 TIL'
tags:
  - '20211013'
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

## 해결 과정

* 블로그를 확인해보자, 22일차부터 업데이트가 진행되지 않고 있었다.

* 깃허브에 블로그에 사용되는 이미지들을 저장했고, 특히 이 오류가 나기 시작한 22일차부터는 데이터모델 테스트를 위해 여러장의 사진을 업로드하던 때였다.

* [관련 docs](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github)에 따르면, Git에서 한번에 업로드 할 수 있는 파일크기의 제한은 약 50MB라고 한다.

* 확인해보니 images 폴더가 48MB인것을 확인할수 있었다.

* images 폴더 전체를 구글 드라이브로 옮기고, 글에 있던 내용들을 전부 구글 드라이브의 공유링크로 바꾸면 되지 않을까 라는 생각이 들어 실행에 옮기기로 했다.

* 먼저, github의 images폴더를 전부 삭제한 후, 정상적으로 블로그 글이 갱신되는지부터 확인해보았지만, 여전히 블로그 갱신은 진행되지 않았다.

* 분명 github.io 블로그는 github에 저장된 내용을 기반으로 띄워주는것일텐데, 내 github 저장소에 images 폴더가 없음에도 불구하고 블로그에서는 마치 있는것처럼 이미지가 정상적으로 출력되고 있었다.

* github에 "업로드 되는 파일의 크기제한"이 50MB인데 github저장소에 이미 존재했던 images폴더의 크기때문에 오류가 발생한것도 그렇고, 아무래도 블로그에 커밋을 진행할때마다 다른 어딘가에 별도로 업로드가 진행되는것 같다는 느낌을 받았다.

* config.yml파일을 수정하여 블로그 테마를 수정하는것이 어떨까 싶어 Github에서 직접 config.yml을 확인해보기로 했다.

* x 표시를 클릭하니 다음과 같은 오류 메시지를 확인할수 있었다.

* 즉, 내가 생각했던 이미지 용량 부족이 원인이 아니라 3일차의 글에서 오류가 발생했다는것.
  * 왜 3일차에 쓴 글이 이제와서 오류가 발생한건지는 납득할수 없었지만, 그즈음에 뭔가 수정했겠거니 하고 넘어가기로 했다.

* 비슷한 오류들이 지속적으로 발견됨에 따라 하나의 공통점을 찾을수 있었는데, 해당 문제점이 템플릿 문법이 글 내부에 들어가있을때 나타나는 오류들이었다.

* 3일차에 쓴 글에서는   
  
    > {% raw %} {{json이름.key이름}} {% endraw %}
    
  라는 부분에서 오류가 발생했다.

* 24일차의 글에서도 유사한 오류가 발생했는데, 
  
  > submit으로 폼 전체를 보내줄 때에는 {% raw %} ```{% csrf_token %}``` {% endraw %} 을 통해 csrf토큰을 전송해주었다.

  라는 부분에서 오류가 발생했다.

* 해결법은 [이 글](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=guseod24&logNo=221483037145)에서 찾을수 있었다.
  * 템플릿 문법이 들어가는곳을 역슬래시를 제외한 {% \raw %} {% \endraw %} 태그로 감싸주면 템플릿 문법을 문자 그대로 인식하여 문제가 해결된다.

* 결과적으로 github 리포지토리의 용량 제한이 문제가 아니었기에 images폴더는 전부 복구해두었다.


 

  
