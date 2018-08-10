# tensorflow로 타이타닉 생존자 예측하기

## 참고
https://github.com/kidokim509/kaggle_titanic


weight. activation function이 의미하는것이 무엇일까?

학습의 목적

ㄴ w의 최적 값을 찾는 것이 목적.

perceptron : single neuron object

n개의 연립 방정식 예시

w1, w2 값을 알지 못하는 상태에서, x, y 값만 주고 w를 찾아라!

tensorflow의 placeholder: 데이터를 받아줄 곳

w는 변수다. gradient descendent graph의 x축


Q

환경 parameter가 여러개더라도 train_set_x, train_set_y 두개만 필요한가?

age, pclass, sex에 대한 절대적인 값의 범위는 서로 다르므로 가중치가 예상과는 다르게 적용될 수도 있다.
하여 mean reduced해서 가중치 편차를 최소한으로 

Tensor type: 3 이상의 n차원 행렬 연산

softmax: input -> 상호간의 확률로 표현해주는 func

7         0.7

    ->
    
3         0.3


