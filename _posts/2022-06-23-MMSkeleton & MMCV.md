---
title: "MMSkeleton & MMCV"
date: 2022-06-22T18:08:30-04:00
categories:
  - '2022-06 TIL'
tags:
  - '20220622'
  - 'TIL'
  - 'Pose estimation'
  - '반려동물 행동 예측'
  - 'openMMlab'
  - 'MMdetection'
  - 'MMSkeleton'
---

# 개요

* AI HUB에서 제공한 반려동물 행동 데이터셋에는, 해당 데이터셋을 이용하여 만든 예제 모델이 존재했다.

  * 객체 검출 개발 모델(코드프로)
  * 행동 분류 개발 모델(유니스트)

* 다음에 진행할 프로젝트에서는 반려동물 행동 분류기가 가장 필요했기에, 유니스트에서 개발한 행동 분류 개발 모델을 분석하기로 했다.

* 해당 개발진이 어떻게 관절의 좌표로 스켈레톤을 구축했을지 코드를 관심있게 보자, MMSkeleton과 MMcv라는 처음보는 라이브러리가 있어 조사하기로 했다.

# openMMlab

* [Homepage](https://openmmlab.com/home)

* The CUHK Multimedia Lab에서 제공하는 Open Source Project의 프로젝트들의 총칭이다.

* 다양한 프로젝트들을 toolbox처럼 만들어 제공한다.

* 데모코드 개발진은 여기서 스켈레톤 기반 포즈 인식 라이브러리인 MMSkeleton과 Computer Vision 유틸리티인 MMCV를 사용했다.

# MMSkeleton

* [Github](https://github.com/open-mmlab/mmskeleton)

![MMSkeleton image](https://github.com/open-mmlab/mmskeleton/raw/master/demo/recognition/demo_video.gif)

* 스켈레톤 기반 포즈 인식 라이브러리.

* ST-GCN<sup>[[1]](#footnote_1)</sup> 기반으로 만들어졌다.

* 좋은 확장성으로 인해 행동 인식에 관한 여러 연구에서 활용 가능하다.

# ST-GCN

## 진행 방식

  ![ST-GCN image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fmcha0%2FbtqxECHKZR6%2FhZtIxTUkxSP4eU6KL84CUK%2Fimg.png)

  1. 영상의 각 프레임에서 Skeleton을 추출.
  2. Skeleton data를 그래프로 제작함. 이때, 각 joint가 node, 각 node가 이어지는 부분(시간/공간)을 edge로 연결
  3. 9개의 ST-GCN 모듈을 통해 feature를 추출
  4. softmax 함수를 사용하여 행동을 분류

## Skeleton Graph Construction

  ![ST-GCN image2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcFnvuF%2FbtqxFTI5Aa5%2F5x1kE1X0vRCC5QU5k1pITk%2Fimg.png)

* 각 joint가 공간적으로 연결되거나(인접한 부위), 시간에 따라 연결(같은 부위의 시간에 따른 이동)된다.

* joint와 시공간에 따른 edge를 통해 그래프를 형성하므로, 인간 외의 다른 골격에도 활용 가능하며, dataset의 구분을 받지 않는다.

* vertex의 집합은 다음과 같은 수식으로 표기된다.
  * $T$는 frame 개수, $N$은 한 skeleton에서 joint의 갯수이다.
  * $V = \big\{ vti|t = 1, . . . , T, i = 1, . . . , N \big\}$


# 참고한 글

* 

* [mmskeleton - Start Action Recognition Using ST-GCN](https://github.com/open-mmlab/mmskeleton/blob/master/doc/START_RECOGNITION.md)

* [논문 읽어주는 석사생 님의 ST-GCN 논문 정리글](https://reading-cv-paper.tistory.com/entry/AAAI-2018Spatial-Temporal-Graph-Convolutional-Networks-for-Skeleton-Based-Action-Recognition#recentComments)






------

<a name="footnote_1">[1]</a> : 
