---
title: "Dacon Daily Python Camp 2일차 공부"
date: 2021-11-12T18:30:00-04:00
categories:
  - '2021-11 TIL'
tags:
  - '20211112'
  - TIL
  - 의사결정나무
---


# TIL

## 의사결정나무 모델 사용

> from sklearn.tree import DecisionTreeClassifier  
> model = DecisionTreeClassifier()


## 결측치 대체 평균

* 결측치들의 데이터를 피쳐의 평균값으로 채워넣는 경우.

> df.fillna({'칼럼명':int(df['칼럼명'].mean)}, inplace=True)

## 결측치 대체 보간

* 해당 튜토리얼에서 다루는 따릉이 데이터의 경우, 피쳐들은 기상정보, 데이터의 순서는 시간순서로 정렬되어있음.

* 따라서 결측치의 경우, 이전 행(이전 시간)과 다음 행(다음 시간)의 평균으로 보간하는것은 상당히 신뢰성 높은 방법이라 할 수 있음.

* 데이터의 특성에 따라 결측치를 어떻게 대체할지는 엔지니어의 역량.

> df.interpolate(inplace=True)

    
## 랜덤 포레스트

* 여러개의 의사결정 나무를 만들어서 이들의 평균으로 예측의 성능을 높이는 방법.

* 이런식으로 모델 여러개에서 데이터의 평균을 내는 방식을 앙상블 기법이라 함.

![앙상블 기법의 이해](https://camo.githubusercontent.com/163813d4cc5bd416e2a5249b1a0300a35c6c1496ab894446e5de5233fb9703ee/68747470733a2f2f69302e77702e636f6d2f687567727970696767796b696d2e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031392f30342f72616e646f6d666f72657374332e706e673f726573697a653d383337253243383635)

## 앙상블의 두가지 접근법

### 배깅(Bagging; bootstrap aggregating)

* 하나의 주어진 데이터에서 여러개의 모델을 만들어 각 모델들 결과값의 평균을 통해 성능을 높이는 기법.

* 주어진 데이터에 대해 복원추출(Bootstrap)을 여러번 함으로서 여러개의 데이터셋을 생성할수 있음.
 
* 예측 결과에 따라서 <U><strong>분류라면 다수결, 회귀라면 평균</strong></U>으로 결과를 결정한다.

### 부스팅(Boosting)

* 매번 학습을 할때마다 오분류된 확률변수에 대해 가중치를 부여한 후, 다시 학습을 하며, 이 과정을 반복하면서 매번의 결과들을 앙상블하는것이다.

![부스팅 기법 이미지](https://camo.githubusercontent.com/56c9394a305fed783361563b6fda0bfac34cf7d0e8c8ae717208d35d703c3696/68747470733a2f2f64617461736369656e63652e65752f77702d636f6e74656e742f75706c6f6164732f323032302f30382f3438323234365f315f456e5f32355f466967325f48544d4c2d393738783635322e706e67)

* 대표적으로 AdaBoost 알고리즘, Gradient Boost 알고리즘이 있다.

* AdaBoost 알고리즘은 <U><strong>오분류 관찰치에 대한 가중치를 올림</strong></U>

* Gradient Boost 알고리즘은 <U><strong>직전 단계의 오차를 학습함</strong></U>

![알고리즘 수식 이미지](https://camo.githubusercontent.com/5b182060ed226e415465b0f9b6ddc4bbca7883faa0189582f4e59688e4538cb0/68747470733a2f2f692e737461636b2e696d6775722e636f6d2f743656434f2e706e67)
