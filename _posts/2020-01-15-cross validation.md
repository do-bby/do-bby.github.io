---
title: "교차 검증"
categories: 
  - blogging
last_modified_at: 2020-01-15 T18:23:00+09:00
toc: true
---

모델 평가
모델 평가란 모델이 얼마나 좋은 성능을 보일지 평가하는 방법을 말합니다.
모델 평가를 할 때, 학습 데이터 뿐만아니라 새로운 데이터가 들어왔을 때 잘 동작하는지 측정을 하는 방법을 일반화라고 하는데,
일반화가 중요한 이유는 학습데이터는 편향되어 있을 수 있기 때문입니다.

from sklearn.datasets import make_blobs
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
scipy은 과학 계산용 python모듈로 scikit-learn을 사용하기 위한 모듈입니다.

임의의 Data set을 생성

x, y = make_blobs(random_state=0)

데이터와 타깃 레이블을 train set와 test set으로 나눕니다

x_train, x_test, y_train, y_test = train_test_split(x, y, random_state=0)

# 모델 객체를 만들고 훈련 세트로 학습시킵니다

logreg = LogisticRegression().fit(x_train, y_train)

모델을 테스트 세트로 평가합니다

print("테스트 세트 점수: {:.2f}".format(logreg.score(x_test, y_test)))

모델을 평가하기 위한  train_test_split함수를 사용하여 Data set과 train set으로 나누고,
모델을 만들기 위해 train set에 fit메소드를 적용했고,
모델을 평가하기 위해 test set에 분류된 샘플의 비율을 계산하는 score메소드를 사용했습니다.
데이터를 train set과 test set으로 나누는 이유는 
새로운 데이터를 모델에 잘 적용되는지 측정하기 위함입니다.

교차 검증
교차 검증(cross-validation)은 모델을 평가하는 한 가지 방법 중 하나로,
여러 번 반복해서 나누고 여러 모델을 학습하는데,
가장 널리 사용되고 있는 교차 검증 방법은 k-fold cross-validation입니다.
교차 검증이 필요한 이유는 데이터가 test set 과 train set으로 구성되어 있는데,
train set을 분리하지 않으면 모델 검증을 위해 고정된 test set을 사용해야 할 것입니다.
고정된 test set으로 모델을 평가하게 되면 그 모델은 해당 test set에만 잘 동작하는 모델이 되기 때문에,
새로운 데이터가 들어왔을 때 예측을 제대로 수행하지 못하게 됩니다.

모델을 평가할 때 test set이 고정되어 있기 때문에 문제가 발생하는데,
교차 검증은 test set을 고정시키지 않고 데이터의 모든 부분을 사용해 모델을 검증함으로써 문제를 해결합니다.

전체 데이터를 k개로 나누고 k번 평가를 실행하는데, test set은 중복없이 위치를 바꾸면서 평가를 합니다.
즉 k번째 데이터는 k-1개의 train set과 1개의 test set으로 구성됩니다.
다음으로 k개의 평가의 평균을 내어서 모델의 성능을 평가합니다.

k-fold cross-validation 예제 코드(데이터가 1,2,3,4인 경우)

import numpy as np
from sklearn.model_selection import KFold

y=np.array([1,2,3,4])

fold의 개수. 4개의 fold 이면 3개의 train set과 1개의 test set으로 쓰인다.

kf=KFold(n_splits=4)
print(kf)

split메소드는 split 되는 index를 알려줍니다.
for train_index, test_index in kf.split(y):
    print("train:", train_index, "test:", test_index)
    y_train, y_test = y[train_index], y[test_index]
    print("y_train:", y_train)
    print("y_test:", y_test)

샘플이 4개로 나눠져 총 4번의 iteration이 이루어집니다.






 


