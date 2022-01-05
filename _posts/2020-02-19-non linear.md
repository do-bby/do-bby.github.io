---
title: "비선형"
categories: 
  - blogging
last_modified_at: 2020-02-19 T15:00:00+09:00
toc: true
---


~~~python




from sklearn import svm
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import accuracy_score
from matplotlib.colors import ListedColormap
from mlxtend.plotting import plot_decision_regions



X_xor = np.random.randn(200,2)
y_xor=np.logical_xor(X_xor [:, 0]>0,X_xor[:, 1]>0)
y_xor = np.where (y_xor, 1, -1)


plt.scatter (X_xor [y_xor == 1, 0], X_xor [y_xor == 1, 1], c = 'b', marker = 'x', label = '1')
plt.scatter (X_xor [y_xor ==-1, 0], X_xor [y_xor ==-1, 1], c = 'r', marker = 's', label = '-1')
plt.ylim (-3.0)
plt.legend (loc=2)
plt.show ()

X_train, X_test, y_train, y_test=train_test_split(X_xor,y_xor,test_size=0.3, random_state=0)
sc=StandardScaler() #기본 스케일, 평균과 표준편차 사용
                    #평균을 제거하고 데이터를 단위 분산으로 조정

sc.fit(X_train)
X_train_std=sc.transform(X_train)
X_test_std=sc.transform(X_test)

ml=svm.SVC(kernel='rbf', C=10000.0, gamma=0.10, random_state=0)
ml.fit(X_train_std, y_train)
y_pred = ml.predict(X_test_std)
print('테스트개수: %d, 오류개수:%d' %(len(y_test), (y_test != y_pred).sum()))
print ('정확도: %.2f' %accuracy_score(y_test, y_pred))

X_combined_std = np.vstack((X_train_std, X_test_std)) #행을 추가
y_combined = np.hstack((y_train, y_test)) #열을 추가
plot_decision_regions(X_combined_std,y_combined,ml)
plt.legend()
plt.tight_layout() #여백조절
plt.show() #화면 표시 jupyter나 ipython에서 호출안해도댐





~~~



# cost = 10

![cost =10](https://user-images.githubusercontent.com/58400107/148207293-d56e5851-c0d7-44a1-84a0-9c6caa8c2cba.png)


# cost = 100

![cost =100](https://user-images.githubusercontent.com/58400107/148207295-9e3ae896-b592-4b66-aebe-18acc7b58261.png)

# cost = 10000

![cost = 10000](https://user-images.githubusercontent.com/58400107/148207291-8db3b18d-2536-4d49-94bd-882be26fe25b.png)


# gamma = 1

![gamma=1](https://user-images.githubusercontent.com/58400107/148207411-2f494377-08a0-4056-8b2b-3c638c7f635c.png)


# gamma = 10


![gamma=10](https://user-images.githubusercontent.com/58400107/148207414-6c59baaf-cc16-4ee1-a8d7-0ee3388bc2ae.png)



# gamma = 100


![gamma=100](https://user-images.githubusercontent.com/58400107/148207407-639a4514-27ae-4d99-9497-2622bb241183.png)






