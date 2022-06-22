---
title: "Matplotlib 만들었던 코드 조각"
date: 2022-06-22T18:08:30-04:00
categories:
  - '2022-06 TIL'
tags:
  - '20220622'
  - 'TIL'
  - 'Matplotlib'
  - 'Seaborn'
  - 'Pie Chart'
---

# 개요

* 제로베이스에서 내준 세계 테러데이터 분석과제의 발표까지 끝냈다.

* 해당 과제는 업로드 불가 판정을 받았지만, 해당 과제를 진행하며 얻은 유용한 코드조각들은 상관없을것같아 업로드한다.

* 사용한 데이터셋은 [Global Terrorism Database](https://www.kaggle.com/datasets/START-UMD/gtd)이다.


# 테러 횟수 증가폭

## 코드

  ```py
  periods = 1
  terror_increase = terror['Year'].value_counts().sort_index().pct_change(periods=periods).sort_values(ascending=False)[1:]

  print("{0}년 단위로 보았을때, 테러 횟수의 증가폭이 가장 늘었던 때는 {1}년으로, {0}년 전인 {2}년에 비해 {3}% 증가했다.".format(periods,terror_increase.index[0],terror_increase.index[0]-periods,round(terror_increase.values[0] * 100,2)))
  print("수치상으로는 {0}회에서 {1}회로 증가했다.".format(terror['Year'].value_counts().loc[terror_increase.index[0]-periods],terror['Year'].value_counts().loc[terror_increase.index[0]]))
  ```

## 결과

  ```
  1년 단위로 보았을때, 테러 횟수의 증가폭이 가장 늘었던 때는 2005년으로, 1년 전인 2004년에 비해 72.98% 증가했다.
  수치상으로는 1166회에서 2017회로 증가했다.
  ```


# subplot + pie chart

## 코드

  ```py
  fig, axes = plt.subplots(3,4,figsize=(16,16))

  for i in range(12):
      ax = axes[i//4][i%4]
      ax.set_title(victims_rate.index[i],fontsize=15)
      ax = ax.pie(victims_rate.iloc[i],startangle=90,counterclock=True,autopct='%.1f%%')
      

  plt.suptitle("Type of Victims Rate of Each Region", fontsize = 40)
  fig.legend(loc='upper right',bbox_to_anchor=(1,0.93),labels = victims_rate.columns, fancybox=True,ncol=4, shadow=True)
  plt.show()
  ```

## 결과

  <img src=https://1geraldine1.github.io/assets/images/Study/zerobase/terrordata/fig1.png  />


# subplot + pie chart 2

## 코드

  ```py
  fig, axes = plt.subplots(3,4,figsize=(16,16))

  color_table = {x:y for x,y in zip(list(region_attacktype.columns) + ['etc'],sns.color_palette('RdYlGn',10))}

  for i in range(12):
      ax = axes[i//4][i%4]
      ax.set_title(region_attacktype.index[i],fontsize=15)
      atype = region_attacktype.iloc[i].sort_values(ascending=False)
      atype['etc'] = atype[5:].sum()
      atype[5:-1] = 0
      atype = pd.concat([atype.iloc[:5],atype[-1:]])
      ax.pie(atype,startangle=90,counterclock=False,autopct=lambda p: "{0}%".format(round(p,2)) if p > 7 else None, colors=[color_table[keys] for keys in atype.index])
      ax.legend(loc="lower center",bbox_to_anchor=(0.5,-0.4),labels=[x for x in atype.index if atype[x] > 0], fontsize=10)
      
  plt.suptitle("AttackType of Each Region\n(Order by Killed Rate)", fontsize = 40)
  plt.show()
  ```

## 결과

  <img src=https://1geraldine1.github.io/assets/images/Study/zerobase/terrordata/fig2.png  />

## 해설
  * 일정 이하의 비율을 가진 데이터들의 레이블을 꺼버린 버전의 차트다.

  * 상위 5개 데이터를 제외한 나머지는 etc로 통합하여 파이 차트의 가시성을 높였다.

  * 덤으로, color_table 딕셔너리를 통해 같은 유형의 범주라면 같은 색이 나오도록 작성했다.


# 누적막대그래프 개조

## 코드

  ```py

  ct_before_2004 = pd.crosstab(before_2004.Region,before_2004.AttackType)
  new_index = {x:x+"_before_2004" for x in ct_before_2004.index}
  ct_before_2004.rename(index=new_index,inplace=True)

  ct_after_2004 = pd.crosstab(after_2004.Region,after_2004.AttackType)
  new_index = {x:x+"_after_2004" for x in ct_after_2004.index}
  ct_after_2004.rename(index=new_index,inplace=True)

  # divide_by_2004 = pd.concat([ct_before_2004,ct_after_2004])

  divide_by_2004 = pd.DataFrame()

  for i in range(12):
      divide_by_2004 = divide_by_2004.append(ct_after_2004.iloc[i])
      divide_by_2004 = divide_by_2004.append(ct_before_2004.iloc[i])
      

  divide_by_2004.plot.barh(stacked=True,width=1,color=sns.color_palette('RdYlGn',9))

  fig=plt.gcf()
  fig.set_size_inches(12,8)
  plt.show()

  ```

## 결과

  <img src=https://1geraldine1.github.io/assets/images/Study/zerobase/terrordata/fig3.png  />


## 해설

  * 특정 시점을 기준으로 누적 막대 그래프를 비교해 보여주고 싶었다.

  * 단순 concat의 경우, 기준점을 전후해 바뀌는 범주의 변화를 보여주기에 좋지 않았다.

  * 반복문을 통해 시점 이전과 이후의 데이터프레임에서 iloc으로 범주를 뽑아내 새 데이터프레임에 붙이는 방식으로 진행했다.

  * 범주를 두개단위로 뭉치는것이 최선이겠지만, 그래프를 여러개 그리는건 별로일것 같아 하나의 그래프에 뭉쳐두었다.

  * 더 나은 방법을 모르는 이상, 이쪽이 제일 직관적일것 같아보였다. 