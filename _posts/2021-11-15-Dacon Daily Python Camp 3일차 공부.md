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
  * 노드를 분할하기 위한 데이터 수
  * 해당 노드에 이 값보다 적은 확률변수 수가 있다면 stop.
  * 작을수록 트리는 커짐.

* 최소 향상도(min_impurity_decrease)
  * 노드를 분할하기 위한 최소 향상도
  * 향상도가 설정값 이하라면 더이상 분할하지 않음.
  * 작을수록 트리는 커짐.

* 비용복잡도(Cost-complexity)
  * 트리가 커지는것에 대한 패널티 계수
  * 불순도와 트리가 커지는것에 대한 복잡도를 계산함.

* 위와 같은 정지규칙들을 종합적으로 고려해 최적의 조건값을 찾는것을 하이퍼파라미터 튜닝이라함.

* 다양한 방법론이 존재하지만, Best 성능을 나타내는 GridSearch는 완전탐색을 사용.

  * 가능한 모든 조합중 가장 우수한 조합을 찾아줌.
  * 하지만 완전탐색이므로 Best 조합을 찾을때까지 시간이 매우 오래 걸림. 

## GridSearch 구현

> from sklearn.model_selection import GridSearchCV  
> model = RandomForestRegressor(criterion = 'mse', random_state=2020)  
> params = {'n_estimators': [200, 300, 500],
          'max_features': [5, 6, 8],
          'min_samples_leaf': [1, 3, 5]}  
> greedy_CV = GridSearchCV(model, param_grid=params, cv = 3, n_jobs = -1)
greedy_CV.fit(X_train, Y_train)
