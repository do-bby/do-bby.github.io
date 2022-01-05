---
title: "SVM python"
categories: 
  - blogging
last_modified_at: 2020-01-31T15:00:00+09:00
toc: true
---

SVM python code

~~~python

from sklearn.svm import SVC
import matplotlib.pyplot as plt
import numpy as np

X = np.array([[1,2],[5,8],[1.5,1.8],[8,8],[1,0.6],[9,11]])
y= [0,1,0,1,0,1]
clf =SVC(kernel = 'linear', C=1.0)
clf.fit(X,y)
print(clf.predict([[0.58,0.76]]))
print(clf.predict([[10.58,10.76]]))

w = clf.coef_[0]
print(w)
a = -w[0] / w[1]

xx = np.linspace(0,12)
yy = a * xx - clf.intercept_[0] / w[1]

h0 = plt.plot(xx, yy, 'k-', label="non weighted div")

plt.scatter(X[:, 0], X[:, 1], c = y)
plt.legend()
plt.show()

~~~


x데이터의 벡터는 2차원이고, 구분레이블은 y로 0,1 두 그룹으로 나눈다.
SVC리턴값으로 clf로 피팅을 하게되면
clf.predict()로 입력값 x에 대한 구분레이블y를 예측할 수 있다.
x데이터의 벡터요소를 x0,x1로 하고,
새로운 좌표계의 1차원 좌표축을 z라 하면
z=f(x0,x1),
z>=0이면 레이블 1, z<0이면 레이블 0

clf.coef로 w0와 w1을 얻고, intercept로 b를 얻는다.
w0,w1는 입력값의 가중치.b는 bias

z=w0*x0+w1*x1+b가 된다.

위 라인을 x1(y축)에 대해 정리하면
기울기는 -w0/w1

y절편은 -b/w1

이 라인이 구분선이 된다.


{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/svm.png" alt=""> {% endraw %}