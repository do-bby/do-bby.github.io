---
title: "분류(Classification)"
categories: 
  - blogging
last_modified_at: 2020-01-17 T16:23:00+09:00
toc: true
---

Machine Learning에서 지도학습,비지도학습,강화학습이 있었다고 했는데,
이 중 지도학습 중에서 회귀와 분류가 있습니다.


간단하게 회귀와 분류를 구분하자면, 아래와 같이 구분할 수 있습니다.

{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/classification.png" alt=""> {% endraw %}

회귀와 분류의 차이라면
출력값에 연속성이 있다면 회귀 문제라고 볼 수 있습니다. 


예를 들어 연봉을 예상할 때 1억이든 1억 1만원이든 큰 문제가 되지 않습니다.


하지만 분류 문제에서는 중간은 없습니다.


예를 들어 스팸메일을 분류한다면 스팸 메일이거나 아니거나 두 가지로 나누어지는 것이지 중간인 메일은 없습니다.

#분류(Classification)

{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/C.png" alt=""> {% endraw %}

분류는 미리 정의된, 가능성 있는 여러 클래스 레이블중 하나를 예측하는 것 인데,
얼굴 인식, 유명한 숫자 판별(MNIST) 등이 분류에 속합니다.


분류에서도 두개로만 나누는 이진 분류(binary classification)와

셋 이상의 클래스로 분류하는 다중 준류(multiclass classification)으로 나뉩니다.

#이진 분류(Binary classification)

{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/binary classification.png" alt=""> {% endraw %}

이진 분류는 예측해야 할 class가 두가지인 경우입니다.


내가 받은 메일이 스팸인지 아닌지,
누군가가 나에게 보낸 메세지가 욕설이냐와 같이 대답이 예/아니요로 구분될 수 있는 문제들을 주로 포함합니다.


두가지 class는 positive class, negative class로 나눌 수 있습니다.


알려지지 않은 데이터가 들어왔을 때 어디에 속하는지 아는 것이 이진 분류의 목적입니다.

{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/sigmoid.png" alt=""> {% endraw %}

1차 선형함수를 어떻게 이진 분류에 적용하느냐가 문제인데,


이때 등장하는 개념이 활성함수(Activation Function)입니다. 


대표적인 활성 함수는 시그모이드(sigmoid)함수인데,


시그모이드 함수는 입력된 데이터를 일정 기준에 따라 0과1로 표현해주는 단순 함수입니다.


선형데이터를 비선형 데이터로 만들어주는 특성이 있기 때문에 머신러닝에서 다양한 방식으로 많이 사용됩니다.

---

> 선형과 비선형의 차이
>
>
> 데이터가 선형적이란 얘기는 직선에 가까운 분포를 갖고 있다는 뜻인데, 
>
>
> 상대적으로 예측하기 쉽습니다.
>
>
> 데이터가 비선형일때는 데이터의 분포가 직선의 형태가 아닌 곡선이거나 극단적 값에 수렴하는 형태를 갖고있습니다.
>
>
> 선형데이터와 다르게 예측하기 힘듭니다.
>
>
> 머신러닝에서 다루는 대부분 데이터는 비선형적입니다.
>
>
> 따라서 1차적으로 선형 함수로 계산하고 데이터의 특징을 구체적으로 표현하기 위해 활성 함수를 사용해
>
>
> 비선형 성을 추가합니다.

---

{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/function.png" alt=""> {% endraw %}

이진 분류 함수를 수학적으로 표현하면 위와 같습니다.


활성 함수에는 ReLU, tanh함수가 사용됩니다.



#다중 분류(Multi-class classification)

{% raw %} <img src="https://qkrdbstn15.github.io/assets/img/multi class.png" alt=""> {% endraw %}

다중 분류는 예측해야 할 class가 여러 가지인 경우입니다.


언어 분류 모델 같은 경우, 입력 text가 영어/한국어/중국어 등 어느 언어인지 분류합니다.


