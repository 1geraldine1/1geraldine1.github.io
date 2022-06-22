---
title: "Pose estimation 공부"
date: 2022-06-22T18:08:30-04:00
categories:
  - '2022-06 TIL'
tags:
  - '20220622'
  - 'TIL'
  - 'Pose estimation'
---

# 개요

* 제로베이스에서 내주었던 세계테러데이터 분석<sup>[[1]](#footnote_1)</sup>과제를 진행하느라 FormNet 논문 공부 원고를 진행하지 못했다.

* 추가로, 다음에 진행될 프로젝트의 주제가 문서독해와는 저 멀리 떨어져있는 관계로 당분간 FormNet 관련 글은 작성하지 못할것으로 보인다.

* 대신, 다음 프로젝트 주제로 쓸 "애완동물 행동 예측" 프로젝트와 그에 필요한 내용을 공부하며 글을 업로드 할 것 같다.

* 강사님께서 제시했던 주제가 세개 있었다.
    1. 물 탐지 (비정형 object detection)

    2. 치과 석션 대상 탐지 (의료데이터, object detection)

    3. 반려동물 행동 예측 (animal pose estimate)

* 비정형 object detection은 도저히 접근법이 생각나지 않으므로 열외.

* 치과 석션 대상 탐지의 경우, 데이터셋을 리서치 해보았으나, 구강암 점막조직 데이터셋이나 치아 관련 데이터셋만 나왔다.
  * 직접 데이터셋을 구축하라는 소린데, 병원에서 직접 데이터 얻어오라는 소리는 아닐테니 열외.

* 결국 AI HUB에서 봤던 데이터셋이 생각나 반려동물 행동 예측을 주제로 선정했다.

# 사용 데이터셋(예상)

* [AI HUB, 반려동물 구분을 위한 동물 영상](https://aihub.or.kr/aidata/34146)

  * 내가 이 주제를 선정했던 가장 큰 이유.

  * 동물 joint 라벨링, 행동 라벨링, 촬영당시 병력 여부, 촬영당시 동물 감정상태 등 다양한 데이터들이 포함되어있다.

  * 특징

    * 이 데이터는 


# Animal Pose Estimation

## What is Pose Estimation?

* 주어진 데이터에서 관절 또는 부위를 예측하는 분야.

* 관절이 움직이면 그것이 포즈가 되고, 포즈를 안다는것은 행동을 아는것이 된다.

  * 따라서, 행동 인식에 매우 중요한 역할을 담당한다.

## 2D Human Pose Estimation

* 주어진 영상 또는 이미지 데이터에서 사람의 관절 또는 부위를 예측하는 분야.

* 대표적인 2D Human Pose Estimation 방식은 OpenPose, CPN, AlphaPose, HRNet등이 제안되었음.

## 2D Animal Pose Estimation

* 주로 사람에게 적용된 모델을 동물에게 적용하는 Transfer-learning 방식을 많이 사용해왔음.

  * DeepLabCut이 이러한 방식이다.


## Main Challenges of Pose Detection



  
  



------

<a name="footnote_1">[1]</a> : 아쉽게도 업로드 불가 판정을 받았다. 나름 만지는 맛이 출중했던 데이터라서 개인적으로 한번 다뤄보고싶기는 하다.