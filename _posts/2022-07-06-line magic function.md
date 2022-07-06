---
title: "line magic function"
date: 2022-07-06T18:08:30-04:00
categories:
  - '2022-07 TIL'
tags:
  - '20220706'
  - 'TIL'
  - 'Jupyter Notebook'
  - 'Colab'
  - 'line magic function'
---

# Line Magic Function

* 주피터 노트북 또는 Colab에서 os명령어를 사용하기 위한 특수문자.

* cd등의 몇몇 명령어는 cell단위 명령어인 <B>```!```</B>와 전역 단위 명령 <B>```%```</B>의 결과가 다를수 있다.

  * !cd의 경우, 명령이 내려진 해당 cell에서만 디렉터리를 이동하고, 다음 셀에서는 다시 원래 디렉터리로 돌아간다.

  * 반면 %cd의 경우, 전역에 그 명령이 전해지므로 다른 모든 셀에도 동일하게 적용되어있음에 주의해야 한다.

* 이와 별개로, 종종 사용되는 ```%matplotlib inline```의 경우, 주피터 노트북이나 Colab에서 기본적으로 plotting된 matplotlib을 사용한다는 의미이다.

  * 현재는 default값으로 적용되기 때문에, 해당 코드를 따로 사용할 필요는 없다.


# 참고한 글

[inflearn, 권철민 님의 답변](https://www.inflearn.com/questions/291240)

  * 이분 강의에서도 mmdetection을 다루는것 같다. 정 프로젝트 하다 어딘가 막히게 된다면 참고할 강의가 있다는것만으로도 나름 위안이 되었다.


