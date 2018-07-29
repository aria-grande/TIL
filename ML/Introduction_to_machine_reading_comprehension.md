# Introduction to Machine Reading Comprehension

## MRC(Machine Reading Comprehension)
기계가 다양한 주제의 글을 읽어서 뜻을 이해하고, 이해력을 평가하기 위한 질의 응답 기술이다.

개발을 위해 **질문-정답-정답단락**의 트리플로 구성된 대규모 데이터 셋으로 주로 구성되어 있다.

Example. 구글 바로 검색
```
지구에서 달까지의 거리가 어느정도 되나요? 
-> keyword를 통한 문서들 검색
-> Sentence selection
```

## Dataset Shares
- [Stanford, SQuAD](https://rajpurkar.github.io/SQuAD-explorer/explore/1.1/dev/)
- [MS, Macro](http://www.msmarco.org/)

## 구성
### 1. Extranction

지문 추출. 질문과 문단을 주면 해당하는 정답을 지분에서 추출하여 찾아낸다.

지문에 답이 없어도 어떤 값이라도 내보내게 된다.

Passage
```
The Rhine(Romansh: Rein, German: Rhein, French:	le Rhin, Dutch: Rijn) is a European river that begins 
in the Swiss canton of Graubünden in the southeastern Swiss Alps, forms part of the Swiss-Austrian, 
Swiss-Liechtenstein border, Swiss-German and then the Franco-German border, then flows through the Rhineland 
and eventually empties into the North Sea in the Netherlands. The biggest city on the river Rhine is Cologne, 
Germany	with a population of more than 1,050,000 people. It is the second-longest river in Central and 
Western Europe (after the Danube), at about 1,230 km(760mi), with an average discharge of about 2,900 m3/s (100,000 cu ft/s).	
```

Question
```
What river is larger than the Rhine?
```

Answer
```
Danbe
```

### 2. Synthesis & Generation

여러 개의 지문을 통해 답을 찾아낸다.

Passage
```
P1: Impact on Japan's Economy. The Triple Disaster devastated Japan's economy in four ways. 
First, it destroyed 138,000 buildings and cost $360 billion in economic damage. 
This is more than the $250 billion cost estimate for Hurricane Katrina. 

P2: apan’s 2011 Earthquake and Tsunami: Economic Effects and Implications for the U.S. Congressional Research Service 3 construction supplies.
If imports of certain products from Japan become scarce, China, South Korea, or other nations may gain at Japan’s expense.
```

Question
```
What is the economic impact of the Japan earthquake?
```

Answer
```
Japan have $360 billion economic damage because of earthquake.
```

### 3. Reasoning & Interface
지문 내에서 답안을 추론한다.

아직은 딥러닝으로 퀄리티 있는 결과를 도출해내기가 어렵다.

Passage
```
During the construction of the Quebec Bridge in 1907, the bridge’s designer, Theodore Cooper, received word that
the suspended span being built out from the bridge’s cantilever was deflecting downward by a fraction of an inch (2.54 centimeters). 
Before he could telegraph to freeze the project, the whole cantilever arm broke off and plunged, along with seven dozen workers, into the St. Lawrence River. 
It was the worst bridge construc(on disaster in history. As a direct result of the inquiry that followed, 
the engineering “rules of thumb” by which thousands of bridges had been built around the world went down with the Quebec Bridge. 
Twentieth-century bridge engineers would thereaaer depend on far more rigorous applications of mathematical analysis. 
```

Question
```
Which one of the following statements can be properly inferred from the passage? 
```

Answer
```
(A): Bridges built before about 1907 were built without thorough mathematical analysis and, therefore, were unsafe for the public to use. 
(B): Cooper’s absence from the Quebec Bridge construction site resulted in the breaking off of the cantilever. 
(C): Nineteenth-century bridge engineers relied on their rules of thumb because analytical methods were inadequate to solve their design problems. 
(D): Only a more rigorous application of mathematical analysis to the design of the Quebec Bridge could have prevented its collapse. 
(E): Prior to 1907 the mathematical analysis incorporated in engineering rules of thumb was insufficient to completely assure the safety of bridges under construction.

The Answer is (E).
```


## 핵심
- Word Embedding, Character Embedding, Knowledge Embedding
- [RNN](https://en.wikipedia.org/wiki/Recurrent_neural_network) 구조
- Attention(sequention-attention, self-attention, ...)

### 속도가 느려요!
1. RNN 구조상 속도가 느려진다.
2. 문서의 길이

### 개선 포인트!
1. 속도 개선을 위해 selection 함수 사용(미분이 불가한 함수)

  문장 seletions를 통한 개선: 여러 문장 중 답과 관련 있어 보이는 몇몇 문장들로만 모델링. RNN을 통해 최종 답 추론.
  
2. 강화 학습을 이용한 Approximation

