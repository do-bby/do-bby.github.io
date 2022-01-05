---
title: "kNN기계학습 python"
categories: 
  - blogging
last_modified_at: 2020-01-20 T16:23:00+09:00
toc: true
---
kNN기계학습을 python으로 구현


~~~python

import numpy as np
import matplotlib.pyplot as plt

grape = [8, 5]
fish = [2, 3]
carrot = [7, 10]
orange = [7, 3]
celery = [3, 8]
cheese = [1, 1]
category = ['과일', '단백질', '채소', '과일', '채소', '단백질']

#분류대상
dan = int(input('단맛 입력(1~10):'))
asac =  int(input('아삭거림 입력(1~10):'))
target = [dan, asac]

~~~

카테고리는 '과일','단백질','채소' 이렇게 3가지로 구분되며,
데이터의 단맛과 아삭거림의 정도에 따라 카테고리가 정해진다.
단맛과 아삭거림을 사용자로부터 입력받아 새롭게 분류할 데이터 target생성

~~~python

def data_set():
    dataset = np.array([grape,fish,carrot,orange,celery,cheese]) #분류집단
    size = len(dataset)
    class_target = np.tile(target, (size, 1))   #분류대상
    class_category = np.array(category)         #분류범주
    
    return dataset, class_target, class_category

#dataset 생성
dataset, class_target, class_categoty = data_set()   #data_set()함수 호출

~~~

분류집단을 np.array()를 이용해 행렬형태로 만들고 분류대상,분류범주를 생성

~~~python

def classify(dataset, class_target, class_categoty, k):
    # 유클리드 거리 계산
    diffMat = class_target - dataset   #두 점의 차
    sqDiffMat = diffMat**2             #차에 대한 제곱
    row_sum = sqDiffMat.sum(axis=1)    #차에 대한 제곱에 대한 합
    distance = np.sqrt(row_sum)        #차에 대한 제곱에 대한 합의 제곱근(최종거리)
    
    # 가까운 거리 오름차순 정렬
    sortDist = distance.argsort()
    
    # 이웃한 k개 선정
    class_result = {}
    for i in range(k):
        c = class_categoty[sortDist[i]]
        class_result[c] = class_result.get(c, 0) + 1

    return class_result
~~~

유클리드 거리 계산 식을 이용해 분류할 대상과 분류범주거리를 구한다.
가까운거리에 있는 순으로 오름차순으로 정렬 후 값에 따라 어떤 카테고리에 가까운지 분류

~~~python

#함수 호출
k = int(input('k값 입력(1~3):'))
class_result = classify(dataset, class_target, class_categoty, k)  # classify()함수호출
print(class_result)

#분류결과 출력 함수 정의

def classify_result(class_result):
    protein = fruit = vegetable = 0
    
    for c in class_result.keys():
        if c == '단백질':
            protein = class_result[c]
        elif c =='과일':
            fruit = class_result[c]
        else :
            vegetable = class_result[c]

    if protein > fruit and protein > vegetable:
        result = "분류대상은 단백질 입니다."
    elif fruit > protein and fruit > vegetable:
        result = "분류대상은 과일 입니다"
    else:
        result = "분류대상은 채소 입니다."
        
    return result


a = classify_result(class_result)
print(a)
~~~

~~~python

# 시각화(o= 과일, +=단밸질, *=채소
plt.scatter(8, 5, marker='o')
plt.scatter(2, 3, marker='+')   
plt.scatter(7, 10, marker='*') 
plt.scatter(7, 3, marker='o')
plt.scatter(3, 8, marker='+')
plt.scatter(1, 1, marker='*')
plt.scatter(dan, asac, color='red') # 분류대상 -> B집단 

plt.show()

~~~

거리를 쉽게 파악할 수 있도록 plt.scatter()함수를 이용했고,
o는 과일 +는 단백질, *는 채소 카테고리입니다.



