---
title: "Dacon Daily Python Camp 4일차 공부"
date: 2021-11-16T18:30:00-04:00
categories:
  - '2021-11 TIL'
tags:
  - '20211116'
  - TIL
  - 의사결정나무
---


# TIL

## DataFrame.describe()

* 각 열의 결측치는 제외한 수치형 데이터에 한해 데이터 요약을 수행

* 기본적으로 count, mean, std, min, 일사분위수, 이사분위수, 삼사분위수, max값이 출력됨.

## 변수분포 시각화

* matplotlib, seaborn 라이브러리를 통해 시각화를 출력할수 있음.

* 이러한 시각화 결과를 통해 머신러닝 방향성을 잡을수 있음.

> import matplotlib  
> import matplotlib.pyplot as plt  
> import seaborn as sns

* 시각화를 진행할때는 copy()메서드로 복사본을 생성한 후 진행

> dfcopy = df.copy()

* seaborn의 distplot() 메서드를 이용

  * df['피쳐명'] : 출력하고자 하는 컬럼  

  * kde : '그래프에 선을 출력할지 여부'  

  * bins : '출력할 막대그래프 갯수'

> sns.distplot(df['피쳐명'], kde=True, bins=None)  

* 


## 용어 해설

* 분위수(Quantile)

  * 정렬되어있는 자료를 특정 개수로 나눌때 그 기준이 되는 수
  * 2분위수라면 자료 전체를 2등분하는 수를 나타냄.
  * 2분위수는 median, 4분위수는 quartiles, 10분위수는 deciles라고 부름.
  * 4분위수의 3개 분위수는 각각 일사분위수, 이사분위수, 삼사분위수라고 부름.
  


