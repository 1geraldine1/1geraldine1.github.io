---
title: "Dacon Daily Python Camp 3일차 공부"
date: 2021-11-15T18:30:00-04:00
categories:
  - '2021-11 TIL'
tags:
  - '20211115'
  - TIL
  - 의사결정나무
---


# TIL

## 모델 성능 평가 척도

* Residuals(잔차)
  * 회귀분석모델의 예측값과 실제 값의 차이
  * y축에 residuals, x축에 독립변수
  * 적합한 선형 모델 : residuals가 x축을 기준으로 랜덤하게 분포하는 상태.
  * 적합한 비선형 모델 : residuals가 패턴을 보이며 분포하는 상태.

* Mean Squared Error(MSE, 평균제곱오차)

  * 회귀선과 예측값 사이의 오차(residual)이용
  * 오차를 제곱한 값들의 평균

* Root Mean Squared Error(RMSE)

  * MSE에서 구한 값에 Root 적용


## 평가척도에 맞게 랜덤포레스트 모델을 훈련

> model = model = RandomForestRegressor(criterion = 'mse')

## 랜덤포레스트 - 모델 튜닝

* fit()으로 모델이 학습되고 나면 ```feature_importances_``` 속성으로 변수의 중요도를 파악할수 있음.

* 변수의 중요도란 예측변수를 결정할때 각 피쳐가 얼마나 중요한 역할을 하는지에 대한 척도.

* 변수의 중요도가 낮다면 해당 피쳐를 제거하는것이 모델의 성능을 높일 수 있음.

> model.feature_importances_

## 랜덤포레스트 - 하이퍼파라미터

* 랜덤포레스트에서의 하이퍼파라미터 튜닝은 '정지규칙'의 값들을 설정하는것을 의미.

* 최대깊이(max_depth)
  * 최대로 내려갈 수 있는 depth를 지정.
  * 뿌리 노드로부터 내려갈 수 있는 깊이를 지정하며 작을수록 트리가 작아짐.

* 최소 노드크기(min_samples_split)

* 최소 향상도(min_impurity_decrease)

* 비용복잡도(Cost-complexity)
