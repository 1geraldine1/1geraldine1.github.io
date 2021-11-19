---
title: "Dacon Daily Python Camp 6일차 공부"
date: 2021-11-19T18:30:00-04:00
categories:
  - '2021-11 TIL'
tags:
  - '20211119'
  - TIL
---


# TIL

## One-Hot-Encoding

* 컴퓨터는 문자로 된 데이터를 학습할수 없기에 변환 작업을 진행해야 하는데, 이를 One-Hot-Encoding이라 한다.

* 하나만 Hot, 나머지는 Cold한 데이터라는 의미.

  * 자기 자신이 해당되는 값은 1을, 나머지 값에는 0을 주는 방식으로 진행.

> from sklearn.preprocessing import OneHotEncoder  
> encoder = OneHotEncoder()  
> encoder.fit(데이터프레임[['피쳐명']])  
> onehot = encoder.transform(데이터프레임[['피쳐명']])  
> onehot = onehot.toarray()  
> onehot = pd.DataFrame(onehot)  
> onehot.columns = encoder.get_feature_names()  
> onehot = pd.concat([기존데이터, onehot], axis = 1)  
> 


