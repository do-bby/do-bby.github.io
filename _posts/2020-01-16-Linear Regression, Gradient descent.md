---
title: "선형 회귀와 경사하강법"
categories: 
  - blogging
last_modified_at: 2020-01-16 T18:23:00+09:00
toc: true
---
선형 회귀 분석은 지도학습의 일종으로, 예측 모델을 만들어 
알려지지않은 데이터가 들어왔을 때 결과를 예측하는 기술을 말합니다.

{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/LR.png" alt=""> {% endraw %}


학습 데이터는 2차원데이터 (x,y)로 구성되어 있는데,
목적은 학습 데이터에 없는 x값이 들어오면 y값을 예측하는 모델을 만드는 것입니다.

데이터가 완전한 일차원 선형 분포를 갖고있진 않지만
1차방정식을 알아내면 오차가 있어도 대략적인 y값을 알 수 있습니다.

{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/LR2.png" alt=""> {% endraw %}


모델은 1차 방정식이 되고,
W와b는 가중치(weight)와 편향(bias)라 부릅니다.
선형 회귀의 목적은 데이터를 제일 잘 설명하고 있는 W와 b를 찾는 것 입니다.

W=1,b=3이라고 가정하고, 데이터(10,6)을 1차 방정식 , 즉 모델에 적용하면 Y=13이됩니다.
원래의 값 6과 함수를 계산해서 나온 값 13은 -7의 차이가 나며 이를 오차 혹은 비용이라고 합니다.
이런 오차를 정의하는 함수를 손실함수(Loss Function)이라고 하는데 
오차는 양인지 음인지 중요하지 않기 때문에 제곱을 취했습니다.

{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/GD.png" alt=""> {% endraw %}

경사하강법은 오차를 최소화하기 위한 최적의 매개 변수(Weight, bias)를 찾기위해 사용되는 방법 중 하나로,
함수 기울기(경사)를 낮은 쪽으로 계속 이동시켜 극값에 이를 때까지 반복시키는 것을 경사 하강법이라고 합니다.

{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/GD2.png" alt=""> {% endraw %}

경사하강법 과정은 다음과 같습니다.


Step 1. 특정 매개변수로 시작(가중치 w1에 대한 시작 값 선택, 보통 0이거나 임의의 값 선택)

Step 2. Loss Function 계산(시작점에서 곡선의 기울기 계산)

Step 3. 매개변수 값 업데이트 (w2 = w1 - 학습율(learning rate) * dw1(기울기)

Step 4. 앞선 과정을 n번 반복 진행하여 최솟값을 향해 수렴