---
title: "Decision Tree"
categories: 
  - blogging
last_modified_at: 2020-02-24 T17:00:00+09:00
toc: true
---

Decision Tree

결정트리는 분류(Classification)와 회귀(Regression)모두 가능한 지도학습 모델 중 하나입니다.
결정트리는 예/아니오 질문을 이어가며 학습을 하는데,
예를 들어 펭귄,곰,매,돌고래를 구분한다고 할때,
매와 펭귄은 날개가 있지만 곰와 돌고래는 날개가 없습니다.
'날개가 있나요?'라는 질문으로 매,펭귄/돌고래,곰으로 나눌 수 있습니다.




{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/d.png" alt=""> {% endraw %}



특정 질문에 따라 데이터를 구분하는 모델을 결정 트리 모델이라고 하는데,
한번의 분기 때마다 변수 영역을 두개로 구분합니다.
결정 트리에서 질문이나 정답을 담은 네모상자를 노드(Node)라고 하고,
첫 분류 기준(첫 질문)을 Root Node라고 하고, 마지막 노드를 Terminal Node 혹은 Leaf Node라고 합니다.



{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/dt.png" alt=""> {% endraw %}



전체적인 모양이 나무를 뒤짚어 놓은 것과 같아서 Decision Tree입니다.


Decision Tree의 프로세스는 먼저 데이터를 가장 잘 구분할 수 있는 질문을 기준으로 나누고,
나뉜 각 범주에서 또 다시 데이터를 가장 잘 구분 할 수 있는 질문을 기준으로 나눕니다.
이런 과정을 지나치게 많이 하면 Overfitting이 됩니다.
어떤 파라미터를 주지 않고 모델링하면 Overfitting이 발생합니다.



# 가지치기

Overfitting을 막기 위한 전략으로 가지치기(Pruning)이라는 기법이 있습니다.
트리에 가지가 너무 많다면 Overfitting이라 볼 수 있습니다.
가지치기란 나무의 가지를 치는 작업을 말합니다.
즉 최대 깊이나 너미널 노드의 최대 개수, 혹은 한 노드가 분할 하기 위한 최소 데이터 수를 제한하는 것입니다.

# 엔토르피(Entropy), 불순도(Impurity)


불순도란 해당 범주 안에 서로 다른 데이터가 얼마나 섞여 있는지를 뜻합니다.
아래 그림에서 위쪽 범주는 불순도가 낮고, 아래쪽 범주는 불순도가 높습니다.
바꿔말하면 위쪽 범주는 순도가 높고, 아래쪽은 순도가 낮습니다.



{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/e.png" alt=""> {% endraw %}



엔트로피는 불순도를 수치적으로 나타낸 척도입니다.
엔트로피가 높다는 것은 불순도도 높다는 뜻이고,
엔트로피가 낮다는 것은 불순도도 낮다는 뜻입니다.

엔트로피가 1이면 불순도가 최대입니다.
즉, 한 범주 안에 데이터가 정확히 반반 있다는 뜻입니다.
엔트로피가 0이면 불순도는 최소이고, 한 범주 안에 하나의 데이터만 있다는 뜻입니다.



{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/entropy.png" alt=""> {% endraw %}






