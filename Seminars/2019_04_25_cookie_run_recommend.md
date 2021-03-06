# 데이터 기반의 조합 추천

DEVSISTERS 여찬구, 신현석



떼탈출을 할 쿠키들을 추천해주는 것에 대한 이야기를 할 것.

```
쿠키: 탈출하는 running character
떼탈출: 여러 쿠키를 배치해서 이어달리기 하는 것
```

## 왜 만들게 되었을까?

쿠키 80종, 펫 80종 이상

80여 종의 쿠키와 펫으로 20가지의 조합을 구성하라고?

언제 순서대로 배치하지..? 머리 아프다!

80P20*80P20 = ??? .....



### 유저들은 이 문제를 어떻게 해결하고 있을까?

유투브에서 빌드를 검색하거나 커뮤니티에서 공략 질문을 올리고 있었음.



### 떼탈출 조합 복사 기능

떼탈출 탑랭킹을 조회에서 복사하자!

하지만 잘 working하지 않았다. 보유 중인 쿠키와 펫 레벨이 랭커와 다르기 때문. 복사한 랭커의 조합과 점수를 재현하기 어렵다.



### 추천의 필요성을 수치화해보자

유저를 위한 것은 좋은데, **비지니스적으로** 임팩트가 있을까?

#### 1. 떼탈출 이용자들의 등급 분포를 봤더니

최고 등급 달성자 비율: 94.7%

=> 대다수의 유저 분들이 추천 서비스의 혜택을 받을 수 있겠구나!

#### 2. 추가 분석: 신규 유저 기준 구매액 분석

동일 기간으로 분석시, 60% 이상의 신규 유저들은 최고 등급 도달 이전보다 **도달 이후에 구매를 더 많이 하는 경향**

더 많은 유저들을 최고 등급 이후로 올려 보내드려야 겠다! => 매출 상승에 기여할 수 있겠다! 라는 결론

<u>수치화를 통해 추천의 당위성 확립. 자연스러운 공감대 형성</u>



## Engineering & Algorithm 

### 조합 추천의 핵심 및 목표

유저의 쿠키+펫으로 재현 가능한 조합



### 알고리즘

```
조합: 떼탈출에서 최대 20개까지 달라지는 하나의 릴레이(N개의 이어달리기)
기록: 떼탈출에서의 한 유닛(N)
```

전체 유저의 떼탈출 플레이 기록 -> 필터된 조합 테이블(A의 쿠키&펫으로 재현 가능한 조합들) -> 추천 알고리즘 -> 추천 결과(릴레이)

#### 시도 1. 전체조합(릴레이) 가져오기

전체 유저의 조합을 가져온다.

**결론: 잘 working하지 않았다. 레벨 차이 때문에 적합한 기록을 얻기 힘들다.**

#### 시도 2. 여러 유저의 기록을 조립하기

추천이 안끝나게 됨..너무 많은 조합이라서..천문학적인 조합 갯수..

전체 탐색으로는 서비스 하기 어렵다.

#### 시도 3. 일부분만 탐색하면 어떨까? Greedy Algorithm

해당 지점에서 최고점을 내는 쿠키로 정의

다음 주자를 선택하는 방법: 20번 탐색만 하면 됨

FEEDBACK: "추천을 받더니 점수가 떨어지는데요? 제가 만든 조합보다도 못해요"

Greedy의 특성상 전체가 아니라 일부만 탐색하는 것이기 때문에 최선의 추천이라고 장담할 수 없다. 

#### 시도 4. Greedy 탐색 + 유저의 기존 조합을 합쳐서 추천하자

기존 조합의 일부분을 사용하여 2번

총점이 가장 높은 조합을 선택 => 유저는 최소한 자신의 기존 조합 이상의 점수를 추천 받게 된다.



### 알고리즘의 성능 측정 지표

점수가 상승하는 경험을 제공하려면 기존 조합 반환을 최소화해야 합니다.

그래서 기존 조합 반환을 모니터링 하자

**10000명의 유저 샘플링 실험한 결과: 6.2%가 본인의 기존 조합으로 전환!**



#### 하지만, 부정적인 피드백 "내가 한 것보다 높은 점수는 안나와!"

##### 문제는 뭘까?

Greedy 탐색에서 앞 주자가 쓰러지는 지점에서 다음 주자를 찾아야 하는데, 다음 주자를 찾지 못하면 검색이 중단되게 된다. 

##### 어떻게 했을까?

모든 것은 하이퍼파라미터의 문제

검색 범위 k를 넓혔다

**전환율: 6.2% -> 0.46%**



### 성과

#### 최고 등급 달성이 터닝포인트라고 말했는데,  

최고 등급 도달율 증가: 5배 증가

최고 등급 도달한 신규 유저 PUR: 3.3배 증가

신규 유저 매출 상승: 79% 증가

이건 발표자료 꼭 보자!



### Q&A

Q: 유저가 플레이한 기록이 없다면?

A: 추천을 받고자 하는 유저는 기록과 관계 없음. 기록이 없다면 순전히 greedy 탐색의 결과만 받게 된다.



Q: 전체 프로젝트 기간

A: 2018년 10월 부터 3개월 초기 개발 기간



Q: 매출이 늘어난 것에 다른 변수는 없었나?

A: 당연히 매출에는 다른 변수들도 많이 작용하겠지만, 트렌드가 통제된 상태에서 데이터를 분석한 것임!



Q: margin k의 범위를 높일 수록 오차가 많아지고, 좁힐수록 추천할 게 없어질텐데 어떤걸 기준으로 선정?

A: 원래는 신뢰도 있게 하자고 해서 k를 좁게 설정. 나중에 피드백을 받고 k를 조금 넓혀봤는데, 바로 잘 동작해서 그대로 적용

