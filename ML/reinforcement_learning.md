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

![reinforcement](http://www.popit.kr/wp-content/uploads/2017/02/Screen-Shot-2017-02-28-at-4.00.34-PM-600x251.png)

## Issues
- 학습을 하기 위해서는 반드시 환경이 필요하다.
- 학습 시간이 오래 걸린다.
- 주어진 환경이 아니라 내가 궁금한 문제를 풀기 위해 환경을 만드는 것이 가능할까?

  [Unity ML-Agent](https://blogs.unity3d.com/kr/2017/09/19/introducing-unity-machine-learning-agents/)를 사용해보자.
  
  Unity를 사용하여 개인이 강화 학습 환경 제작 가능. 게임 뿐만 아니라 real simulator도 제작 할 수 있다.
  
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
