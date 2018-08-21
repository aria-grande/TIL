# Background
## Paradigm Shift
기존의 코딩: 조건을 line by line으로 써내려 가는 일.

```
앞으로의 코딩: 조건을 학솝 모델의 여러 가중치로 변환하는 일.
```

# Machine Learning
데이터로부터 학습할 수 있는 시스템을 만드는 것. 학습은 더 나은 결정을 하는데 도움을 줄 것이다.

# ML 시스템 종류
## 지도학습과 비지도학습
### 지도학습(Supervised Learning)
파라미터(x)와 정답지(y)가 주어지고, 이를 통해 학습하게 하는 방법.
![supervised learning](images/supervised_learning.png)

- 분류(classification): 스팸 필터
- 회귀(regression): 예측 변수/특성 등을 사용해 중고차 가격 같은 타깃 수치를 예측하는 것이다. 두 변수 사이의 상관관계를 분석하기 위한 방법 중 하나.

### 비지도학습([Unsupervised Learning](https://en.wikipedia.org/wiki/Unsupervised_learning))
훈련 데이터에 label이 없이 학습하게 하는 방법.

- 블로그 방문자에 대한 데이터를 분석할 때. 단, 방문자가 어떤 그룹에 속하는지 알려줄 수 있는 데이터 포인트가 없다고 할 때, 알고리즘이 스스로 방문자 사이의 연결고리를 찾는다.
- 시각화 알고리즘: 레이블이 없는 대규모의 고차원 데이터를 넣으면 도식화가 가능한 2D/3D 표현을 만들어 준다.
- 이상치 탐지(anomaly detection): 부정 거래 방지 위한 비정상 신용 카드 거래 감지.
- 연관 규칙 학습(association rule learning): 마트에서 판매 기록에 이 규칙을 적용하면 주류를 산 사람이 만두를 사러 간다더라. 등의 연관 관계/경향을 찾을 수도 있다.

### 준지도학습(Semisupervised Learning)
레이블이 일부만 있는 데이터도 다룰 수 있다. 보통은 레이블이 없는 데이터가 많고, 레이블이 있는 데이터는 아주 조금인데, 이 때 semi-supervised learning을 할 수 있다. 

Supervised learning + Unsupervised learning

### Reinforcement Learning
학습하는 시스템을 agent라고 부르며 주어진 environment를 관찰해서 action하고 그에 따른 reward/penalty를 받는다.

시간이 지나면서 가장 큰 reward를 얻기 위한 policy를 스스로 학습하며, policy는 주어진 상황에서 agent가 어떤 행동을 선택해야 할지 정의한다.

## 학습 방법
### 배치 학습(Batch Learning)
시스템이 점진적으로 학습할 수 없다. 가용한 데이터를 모두 사용해 훈련시켜야 하며, 이 방식은 시간과 자원을 많이 소모하므로 보통 오프라인에서 수행된다.

시스템을 훈련시킨 후, 제품 시스템에 적용하면 더 이상의 학습 없이 실행된다. **즉, 학습한 것을 적용만 하며, 이를 offline learning이라고도 한다.**

배치 학습 시스템이 새로운 데이터에 대해 학습하려면 (이전 학습 데이터 + 세로운 데이터) 전체 데이터를 사용하여 시스템의 새로운 버전을 처음부터 다시 훈련해야 한다.

그런다음 이전 시스템을 중지시키고 새 시스템으로 교체하는 방식으로 구성된다.

간단하지만, 전체 데이터셋을 사용해 훈련하는 데 많은 컴퓨팅 자원이 필요하며, 몇 시간이 소요될 수 있다. 큰 비용이 발생 할 것.

시스템이 빠르게 변하는 데이터에 적응해야 한다면 더 능동적인 방법이 필요하다.(ex: 주식)

### 온라인 학습(Online Learning)

데이터를 순차적으로 한 개씩 또는 미니 배치라 부르는 작은 묶음 단위로 주입하여 시스템을 훈련시킨다. 

매 학습 단계가 빠르고 비용이 적게 들어 시스템은 데이터가 주입되는 대로 즉시 학습할 수 있다.

연속적으로 데이터를 받고 빠른 변화에 스스로 적응해야 하는 시스템에 적합한 학습 방법이며, 컴퓨팅 자원이 제한된 경우에도 좋은 선택이다.

새로운 데이터 샘플을 학습하면, 학습이 끝난 데이터는 더 이상 필요치 않으므로 버려도 된다.(이전 상태로 되돌릴 수 있도록 데이터를 재사용 하기 위해 보관할 필요가 없다면).

공간도 줄일 수 있고, 새로 주입되는 데이터셋만 학습하면 되므로 offline learning에 비해 컴퓨팅 자원도 줄일 수 있다.

많은 양의 데이터가 들어올 경우, 데이터를 부분으로 나누어 online learning!

문제점은 시스템에 나쁜 데이터가 주입되었을 때 시스템의 성능이 점진적으로 감소한다는 점이다.

#### 학습률(Learning rate)
파라미터가 변화하는 데이터에 얼마나 빠르게 적응할 것인가?

학습률을 높게 하면 시스템이 데이터에 빠르게 적응하지만 예전 데이터를 금방 잊어버릴 것이다.

학습률이 낮으면 시스템의 관성이 더 커져 느리게 학습되지만, 새로운 데이터에 있는 잡음이나 대표성 없는 데이터 포인트에 덜 민감해진다.

## 사례 기반 학습과 모델 기반 학습
시스템이 어떻게 일반화되는가에 따른 분류.

### 사례 기반 학습(Instance-based Learning)
사례를 기억함으로써 학습하며, 데이터 간의 유사도(similarity)를 측정하여 새로운 데이터에 일반화한다.
![instance-based learning](https://www.safaribooksonline.com/library/view/hands-on-machine-learning/9781491962282/assets/mlst_0115.png)

> Example: 
스팸 필터. 스팸 메일과 동일한 메일을 스팸이라고 지정하는 대신 스팸 메일과 매우 유사한 메일을 구분하도록 필터를 구현할 수 있다. 그러기 위해서는 두 메일 사이의 유사도를 측정해야 한다. 아주 간단하게는 두 메일이 공통으로 포함한 단어의 수를 세는 것이다. 스팸 메일과 공통으로 가지고 있는 단어가 많으면 스팸으로 분류!

### 모델 기반 학습(Model-based Learning)
샘플로부터 일반화시키는 다른 방법은 이 샘플들의 모델을 만들어 예측에 사용하는 것이며, 이를 model-based learning이라 한다.
![model-based learning](https://www.safaribooksonline.com/library/view/hands-on-machine-learning/9781491962282/assets/mlst_0116.png)

_Instance-based learning에는 tuning할 parameters가 없지만, model-based learning은 모델을 생성하므로 tuning할 parameters가 존재한다._

# 테스트와 검증
모델이 새로운 샘플에 얼마나 잘 일반화될지 아는 유일한 방법은 새로운 샘플에 실제로 적용해보는 것이다. 

훈련 데이터를 training set와 test set 두 개로 나누어 훈련 및 검증한다.(보통 training : test = 80: 20)

새로운 샘플에 대한 오류 비율을 일반화 오차(generalization error or out-of-sample error)이라 하며, 테스트 세트에서 모델을 평가함으로써 이 오차에 대한 추정값을 얻는다. 이 값은 이전에 본 적이 없는 새로운 샘플에 모델이 얼마나 잘 작동할지 알려준다.

**훈련 오차가 낮지만(훈련 세트에서의 모델 오차가 적음) 일반화 오차가 높다면 이는 모델이 훈련 데이터에 overfitting 되었다는 뜻이다.**

모델 평가는 테스트 세트를 이용하면 된다.

선형 모델이 잘 일반화 되었다고 가정하고, 서비스에 투입해본다. 하지만 성능이 예상만큼 좋지 않을 것이다.

일반화 오차를 테스트 세트에서 여러 번 측정했으므로 모델과 hyper-parameter가 테스트 세트에 최적화된 모델을 만들었기 때문이다.

이 문제에 대한 일반적인 해결 방법은 validation set라 부르는 두번째 holdout set를 만드는 것이다.

1. training set로 다양한 하이퍼파라미터로 여러 모델을 훈련 시키고
2. validation set에서 최상의 성능을 내는 모델과 hyper-parameter를 선택
3. 만족스러운 모델을 찾으면 일반화 오차의 추정값을 얻기 위해 test set로 **단 한 번**의 최종 테스트를 진행한다.

training data에서 validation set로 너무 많은 양의 데이터를 뺏기지 않기 위해 일반적으로 cross-validation 기법을 사용한다.

training data를 여러 subset으로 나누고, 각 모델을 이 subset의 조합으로 훈련시키고 나머지 부분으로 검증한다.

### Model Parameter vs HyperParameter
```
모델 내 파라미터: 새로운 샘플이 주어지면 무엇을 예측할지 결정한다. 학습 알고리즘은 모델이 새로운 샘플에 잘 일반화 되도록 파라미터들의 최적값을 찾는다.
Hyper-parameter: 모델이 아니라 학습 알고리즘 자체의 파라미터이다.
```

<hr/>

## [Linear Regression](https://ko.wikipedia.org/wiki/%EC%84%A0%ED%98%95_%ED%9A%8C%EA%B7%80)
종속 변수 y에 대해 한 개 이상의 독립 변수(x)가  선형 상관 관계를 모델링하는 회귀분석 기법.

연속형 변수, 목록이 되기도 하며, 가중치(w)를 찾는 것이 목적이고 이 것이 곧 모델이다.

![linear_regression](images/linear_regression.png)

## Example
[타이타닉 생존자 예측하기](https://www.kaggle.com/c/titanic/data)

<hr/>

# Neural Network
XOR problem을 생각해보자.

![xor problem](images/xor_problem.png)

Logistic은 linear 모형으로, 평면을 단순하게 나누는 것이라고 생각할 수 있다. 

![xor_linear](images/xor_linear.png)

Neural은 hidden layer를 여러 개 사용하여 모델을 생성하는 것이다.

![xor_neural](images/xor_neural.png)

각 노드에 대해 activation function을 추가하는 것이 중요하다. 

activation function을 추가해야 비선형 모델이 되게 되며, activation function을 추가하지 않는다면 계속 linear하게 될 것이다.

![activation function flow](https://www.researchgate.net/profile/Gregory_OHare/publication/224155275/figure/fig4/AS:340655919386626@1458230108928/Single-neuron-showing-input-weigths-weighted-sum-and-activation-function.png)

![activation functions](images/activation_functions.png)


# [ANN(Artifical Nueral Network)](https://ko.wikipedia.org/wiki/%EC%9D%B8%EA%B3%B5%EC%8B%A0%EA%B2%BD%EB%A7%9D)
생물학의 신경망(뉴런)에서 영감을 얻은 통계학적 학습 알고리즘으로, 사람의 뇌구조를 수치화 한 모델이다.

ANN에서는 노드가 인공 뉴런의 역할을 하며, 노드 간의 결합이 모여 신경망을 구성하게 된다.

뉴런에는 크게 세가지의 기능으로 구성되어 있다.
1. 이전 뉴런에서 정보를 수신한다.
2. 정보를 조합해서 활성화 여부를 판단한다.
3. 뉴런에서 조합한 정보를 내보낸다.

ANN도 마찬가지이다.

![뉴런과 ANN](images/ann.png)

# [DNN(Deep Neural Network)](https://ko.wikipedia.org/wiki/%EB%94%A5_%EB%9F%AC%EB%8B%9D#%EC%8B%AC%EC%B8%B5_%EC%8B%A0%EA%B2%BD%EB%A7%9D(Deep_Neural_Network,_DNN))
한 레이어의 뉴런으로는 복잡한 문제를 학습시키기가 어렵다. 

하여, 입력층(input layer)과 출력층(output layer) 사이에 여러 개의 hidden layer를 둔 ANN이라고 이해하면 된다.

한 개의 layer만 있는 경우를 생각해보자. 
![DNN](images/dnn.png)

이때, 각 노드는 '다른 관점'이라고 볼 수 있다. 

**주어진 input에 대해 다양한 관점에서 학습을 한 후, 이를 종합해서 output으로 내려주는 기본적인 구조를 가지고 있다.**

## Hidden layer가 여러개라면?
![DNN, multiple hidden layers](https://cdn-images-1.medium.com/max/800/1*dnvGC-PORSoCo7VXT3PV_A.png)

복잡한 문제를 다양한 관점에서 관찰하고 그 output을 다시 input 으로 취급해서 학습을 시켜나가니 복잡한 문제를 풀기에 좋다.

그렇다면 DNN은 몇 겹의 hidden layer를 가져가야 할까? 이 것은 상황에 따라 다르며, 설계자(우리)가 설계하기 나름이다.

항상 깊은(deep hidden layers) 네트워크가 좋은 구성은 아니다. 

뭐든 적정점이 있으며, 불필요하게 깊게 구성할 경우 [overfitting](#overfitting) 현상이 발생한다.

적절한 점을 찾는 것이 중요하다.

### [Overfitting](https://en.wikipedia.org/wiki/Overfitting)
너무 과도하게 데이터에 대해 모델을 learning한 경우를 의미한다. 과도 학습된 탓에 전보다 poor 결과를 내놓게 된다.

#### reference
- http://sanghyukchun.github.io/59/
- http://wiki.fast.ai/index.php/Over-fitting

## Neural Network 학습 방법
Error function을 정의 한 후, error가 제일 작은 weights(global minimum)를 찾는다.

### 1. Gradient Descent
미분값이 0에 가장 가까운 값을 구하면 됨.
한 개의 weight에 대해 global minimum 값을 구할 때는 괜찮지만, weight가 한 두 개가 아니라면 구하기 어렵다.

### 2. [Chain Rule](https://ratsgo.github.io/deep%20learning/2017/05/14/backprop/)
forward, backward propagation 두 가지의 방법으로 학습시킨다. 
 
#### Forward propagation
- 주어진 weights로 input data로 output을 계산해 내는 input -> output의 일반적인 흐름이다.
- loss = label - output

#### [Backward propagation](https://en.wikipedia.org/wiki/Backpropagation)
- backward의 경우, output에서 얻어진 weight를 미분해서 다시 layer 내의 가중치 값을 업데이트 시켜주는 방법으로 loss를 최소화 하기 위한 방법이다.
- 실제 뉴럴 네트워크에는 노드가 많은 꽤 큰 계산 그래프를 이루고 있다. 이 네트워크는 최종 정답과 비교한 후, loss를 계산한다.
- 목적은 뉴럴 네트워크의 오차를 줄이는 것이므로, output neuron에서 계산된 error(loss)를 각 edge들의 weight로 사용해 바로 이전 layer의 neuron들이 얼마나 error에 영향을 미쳤는지 계산한다.
- reference: http://sanghyukchun.github.io/74/

## 학습 시키려면?
1. Neural Network 구조를 만든다.
2. Error(=Loss) function을 정의한다.
3. 데이터 학습
4. Loss가 최소가 되는 weight를 찾는다.

## 뭘 해볼 수 있을까?
### [GAN(Generative Adversarial Network)](https://en.wikipedia.org/wiki/Generative_adversarial_network)
Unsupervised ML에서 사용되는 알고리즘 중 하나로, (서로 잡고 쫓기는) 두 개의 neural networks로 구성되어 있다.

### 어떻게?
1. 가짜와 진짜를 잘 판별하는 모델을 만든다.
2. 진짜 같은 가짜를 만들어내는 모델을 만든다.
3. 두 모델 모두 학습 시킨다.
4. 1번 모델이 잘 판별해낼 수 없을 때까지 2번을 학습시키다보면, 이런 재밌는 것들을 해볼 수 있게 된다.
![내가 늙으면?](https://cdn-images-1.medium.com/max/1600/1*UE7Pp_DW7XdCacD2dpz1Ow.png)
