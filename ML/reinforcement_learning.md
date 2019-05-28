# Reinforcement Learning
Machine learning에는 supervised, unsupervised, reinforcement learning이 있다.

그 중에서 [강화 학습](https://ko.wikipedia.org/wiki/%EA%B0%95%ED%99%94_%ED%95%99%EC%8A%B5)에 대해 알아보자.

## 동물은 어떻게 학습하나?
Law of effect: 어떤 행동의 결과가 만족스러우면 다음 행동에서 이전 학습 결과가 반영됨.

## 사람은 어떻게 배우나?
- Reinforcement: 이전에 일어난 행동을 반복하게 하는 자극
- Punishment: 이전에 일어난 행동을 피하게 만드는 자극


# Definition
```
행동 심리학에서 영감을 받았으며, 
정의된 에이전트가 현재의 상태를 인식하여 선택 가능한 행동들 중 보상을 최대화 하는 행동 혹은 순서를 선택하는 방법이다.
```
동물, 사람이 환경과 상호작용을 하며 학습하는 것과 같이, 기계가 수학적인 분석 방법을 통해 학습하는 것이다.

학습하는 시스템을 agent라고 부르며 environment를 관찰해서 action하고, 그 결과로 reward or penalty를 받는다.

가장 큰 보상을 얻기 위해 policy라고 부르는 최상의 전략을 스스로 학습한다. 정책은 주어진 상황에서 에이전트가 어떤 행동을 선택해야 할지 정의한다.

## MDP(Markov Decision Process)
순차적 의사 결정 문제를 다루기 위해 사용하는 일종의 수학적 기술
1. A set of states
2. A set of actions
3. A transition function
4. A reward function

![reinforcement](http://www.popit.kr/wp-content/uploads/2017/02/Screen-Shot-2017-02-28-at-4.00.34-PM-600x251.png)

## Issues
- 학습을 하기 위해서는 반드시 환경이 필요하다.
- 학습 시간이 오래 걸린다.
- 주어진 환경이 아니라 내가 궁금한 문제를 풀기 위해 환경을 만드는 것이 가능할까?

  [Unity ML-Agent](https://blogs.unity3d.com/kr/2017/09/19/introducing-unity-machine-learning-agents/)를 사용해보자.
  
  Unity를 사용하여 개인이 강화 학습 환경 제작 가능. 게임 뿐만 아니라 real simulator도 제작 할 수 있다.
  
## [Q-learning](https://en.wikipedia.org/wiki/Q-function)
- 대표적인 Tabular learning이다.
- 통계학에서, Q-function은 정규 분포의 tail distribution function이다.
- 다음 가능한 Q function 중 최대를 뽑아서 현재 Q function을 update하고, 움직일 때는 max 값을 알면서도 가끔 다른 action을 한다.
- Q function: state와 action을 인풋으로 하면 expected reward가 output으로 나온다.
- 낮은 차원에서는 가능하지만 이미지처럼 차원이 높아질 경우 학습이 얼벼다.

- refer: https://dnddnjs.gitbooks.io/rl/content/deep_q_networks.html

## Deep Q-learning
- 학습하기 위한 데이터를 메모리에 올려놓고 학습한다. replay memory라고 하는데 많은 메모리가 요구된다.
- target network를 따로 운영한다. 학습 속도 저하
- 가치 기반을 통해 행동을 학습한다. 확률 기반이 아님.
- Policy의 경우 확률을 사용하는데, 매번 같은 action을 하는게 아니라 확률에 기반한 가중치를 가지고 random하게 select & action을 함.

## Genetic Algorithm
생명체의 진화를 모방하여 가장 적절한 해집단을 찾아간다.

프로그래머가 정의한 적합도 함수(fitness function)을 통해 유전자를 평가하고, 자연 선택과 같이 살안마을 유전자들을 **선택**한다.

이 때, 유전적 다양성을 해치지 않기 위해서 선택을 **박하게**하지 않는다. 일부 유전자에 일정 확률로 **변이**를 주기도 한다.

0세대에서 시작하여 n세대까지 교배를 통하여 모델을 진화 학습 시킨다.

### 선택 연산
자연 선택을 통해 생명체가 진화하려면 '좋은' 유전자들을 선별 및 이들이 살아남게끔 설정되어야 한다. 유전 알고리즘에서 이런 역할을 수행하는 것이 선택연산이다.
- 토너먼트 선택 연산
- 품질 비례 룰렛휠 연산

### 교차 연산
선택 연산을 통과한 생명체들은 감수분열과 교배를 통해 자신을 닮은 또 다른 자손을 만들어 낸다. 이 과정에서 모체와 부체의 염색체가 섞이게 되며, 이 과정으로 환경에 적응하고, 이겨내고 살아남을 수 있게 될 것이다.
- n점 교차
- 균등 교차

### Example
- https://www.youtube.com/watch?v=Yr_nRnqeDp0
- https://www.youtube.com/watch?v=7ZDvt4to7vU

### Refer
http://invalidid.tistory.com/entry/05-%EC%9C%A0%EC%A0%84-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Genetic-Algorihm


## Multi-agent를 이용한 학습
여러 agent가 경쟁을 해야 하는 상황도 있겠다.

## Adversarial Learning
대부분 게임 플레잉 상황에서 사용 된다. 축구가 대표적인 learning example.

90년 대 부터 있던 개념이더라.


## Imitiation Learning
잘하는 사람, 전문가를 보고 따라하며 학습하면 빨리 배울 수 있지 않을까?

`Teacher - Student` 구조로, teacher의 행동을 학습한다.

Teacher가 잘못된 행동을 했을 경우에도 그대로 배우기 때문에, teacher를 선택하는 것도 관건.

Teacher는 '사람'이 될 수도 있고, optimal planners/controllers가 될 수도 있다.

즉, **teacher에 의해 생성된 training data로 supervised learning**을 하는 것.

[참고자료, immitation_learning.pdf](https://katefvision.github.io/katefSlides/immitation_learning_I_katef.pdf)

## Curriculum learning
사람은 태어나서 바로 달리는 것이 불가하다.
`기고 -> 걷고 ->...-> 달리기`

단계 별로 학습을 하다가 달리기를 할 수 있게 되며, 발전하는 것이다.

관련 paper: https://www.ijcai.org/proceedings/2017/0757.pdf
