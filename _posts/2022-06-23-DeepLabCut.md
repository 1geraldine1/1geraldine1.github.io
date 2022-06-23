---
title: "DeepLabCut"
date: 2022-06-22T18:08:30-04:00
categories:
  - '2022-06 TIL'
tags:
  - '20220622'
  - 'TIL'
  - 'Pose estimation'
  - '반려동물 행동 예측'
  - 'DeepLabCut'
---

# DeepLabCut

* Human Pose Estimate에 비해 Animal Pose Estimate는 라벨링된 데이터의 수가 적고, 신체 구조 역시 인간과 달라 같은 모델을 사용하는데 어려움이 있다.

* DeepLabCut은 50~200프레임 정도의 최소한의 학습데이터만으로 다양한 종의 포즈를 트래킹할수 있다.

## 사용 개요

1. config.yaml을 수정하여 bodyparts, skeleton등을 대상에 맞추어 변경

2. 동영상을 올려 프레임을 뽑아냄

3. 라벨링 실시

4. 트레이닝 할때 사용할 backbone CNN 알고리즘 선택<sup>[[1]](#footnote_1)</sup>

5. 트레이닝 및 모델 생성

6. 데이터 넣어서 추론. 결과를 보고 라벨링 툴을 이용하여 미세조정.

7. 결과가 불만족스럽다면, 다시 1번부터 반복

## 이론

* DeepLabCut의 기반이 되는 모델인 Deepercut은 Bottom-up<sup>[[2]](#footnote_2)</sup>방식의 pose estimation 모델이다.

### Integer Linear Program (ILP)

* CNN 모델을 통해 모든 joint를 찾아내고, 찾은 모든 joint를 잇는 dense graph를 생성.

* body parts의 후보 위치인 점을 $d,d'$로, body parts를 $c,c'$로 정의한다.

* 이때, body parts 후보 위치인 점들은 CNN 네트워크를 통해 선별한다.

![DeeperCut image1](https://miro.medium.com/max/1166/1*bEP4IQN5ckFd9Rz1Hw-ouQ.png)

![DeeperCut image2](https://miro.medium.com/max/1168/1*q6dlW0AKju8pGHHPXp89nQ.png)

  * $x(d,c) = 1$일때, body part $d$는 객체 $c$에 속한다.
  * $y(d,d') = 1$일때, body part $d,d'$는 같은 사람의 것이다.
  * $z(d,d',c,c') = x(d,c)x(d',c')y(d,d')$로 표현되는 이 수식은 정수 선형 계획법 문제로, 가지치기를 통해 풀수있다<sup>[[3]](#footnote_3)</sup>.
  * $z(d,d',c,c') = 1$일때, $d$ 점은 $c$ body parts, $d'$점은 $c'$ body parts이며, $d$와 $d'$는 같은 사람의 몸이다.

![DeeperCut image3](https://miro.medium.com/max/1170/1*ZbWebI3UGI3GtnXW0BW8aw.png)

# 프로젝트 및 데이터와의 비교.

* 이번 반려동물 행동 예측 프로젝트의 경우, AI HUB 데이터 특성상 단일 객체에 대한 포즈 예측이 주로 이루어질것 같다.

* 다중 객체에 대한 part labeling 및 pose estimation이 주를 이루는 DeeperCut은 그런 관점에서 보았을때, 이번 프로젝트와 크게 연관이 없을 가능성이 높아보인다.

* 또한, AI HUB 데이터의 경우 joint에 전부 라벨링이 되어있으므로, 해당 데이터를 구하기 위해 반복하여 라벨링 툴을 사용하는 경우 역시 드물것으로 예상된다.

## 결론.

* 프로젝트와 별개로 좋은 공부 한 셈 치기로 했다.
* Multiple Human Pose estimation같은건 CCTV 이상탐지등 많은 가능성을 가지고 있으니, 알아두면 언젠가 쓸일이 생길것 같다.


# 참고한 글

[East-rain님의 DeepLabCut 개요 번역](https://east-rain.github.io/docs/Deep%20Learning/deeplabcut/introduction.html)

[Sik-Ho Tsang님의 Review: DeepCut & DeeperCut — Multi Person Pose Estimation (Human Pose Estimation)](https://sh-tsang.medium.com/review-deepcut-deepercut-multi-person-pose-estimation-human-pose-estimation-da5b469cbbc3)




------

<a name="footnote_1">[1]</a> : ResNet, Mobilenet 지원.  

<a name="footnote_2">[2]</a> : 영상에서 키포인트를 찾고, 키포인트에서 관계를 분석하여 자세를 추정하는 방식.  
객체를 detecting한 후 해당 bounding box 내부에서 자세를 추정하는 Top-Down방식과 달리 객체를 detecting하는 과정이 생략되어 빠른 실행속도를 보인다.  
따라서, Real-time 모델에 적합하다.  

<a name="footnote_3">[3]</a> : By substituting z(d,d',c,c’)=x(d,c)x(d’,c’)y(d,d’), the objective is converted to Integer Linear Program (ILP), and solved by branch-and-cut. 
