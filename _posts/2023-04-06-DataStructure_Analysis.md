---
title: "Data Structure : Analysis"
categories:
  - INU/Data_Structure
tags:
  - Data Structure
  - Dynamic analysis
  - Static analysis
  - Complexity analysis
toc: true
toc_sticky: true
toc_label: "Carefree to See"
---
---
# Data Structure: Analysis

```
Data Structure : 알고리즘의 성능 분석
```

<img src="/assets/images/INU/analysis.png" alt="analysis_Procdess" width="100%" min-width="200px" itemprop="image">`사진출처:`[AIHR](https://www.aihr.com/blog/job-analysis/)<br>

> 과학과 기술은 시간이 갈수록 기하급수적으로 방대해지고, 발전에 발전을 거듭하게 된다.<br><br>
이는 어떠한 기술이 생겨나고, upgrade 될수록 그것을 바탕으로 또 다른 길이 열릴 수 있기 때문이다.<br><br>
이와 마찬가지로 컴퓨터 공학도 시간이 흐를수록 큰 변화가 생겨 이전 단계와는 이질적으로 Upgrade 되는 것을 우리는 실생활에서 느낄 수 있다.<br><br>
엄청난 계산 속도와 메모리를 가진 요즘의 컴퓨터들은 ChatGPT와 같은 AI기술과 함께 인류에게 새로운 길을 열어 주었다.<br><br>
이와 같이 급격한 시대의 흐름 속에서 우리는 <span style="color:blue">`가장 이상적인 알고리즘`</span>을 설계하는 것에<br>대부분의 시간을 사용하며 개발해왔다.<br><br>
```
이유는 Limited Resources (한정된 컴퓨터 자원).
컴퓨터의 자원(CPU, Memory...etc)이 한정되어 있기 때문이다.
```
<br>
- 그렇다면, 풍부한 Resources 를 손에 넣은 우리는,<br>
더 이상 알고리즘과 프로그램의 효율성 등은 신경쓰지 않아도 되는가?<br><br>
<u>나는 <span style="color:red"> "NO" </span> 라고 생각한다. (정답은 아무도 모른다.)</u><br>


```
"이유는?"
```
>
1. <span style="color:red">`급격한 과학기술의 발전 속에서 그것에 순전히 의지만 하는 행위는 "안주" 라고 생각한다.`</span><br>
~~그 "안주" 아닙니다..~~<br>
그릇이 커진다면 그 안에 담을 수 있는 물도 더 많아진다는 것.<br>Resources가 풍부해질수록,<span style="color:green">`우리는 분명히 더 좋은 프로그램을 설계 할 수 있기 때문.`</span><br><br>
2. <span style="color:red">`개발자들의 결과물은 결국 소비자들에게 priority 가 주어지기 때문이다.`</span><br><br>
아무리 미세한 데이터 처리 속도의 차이더라도 소비자들에게는 선택권이 많다.<br><br>
자신이 설계한 프로그램의 선호도를 높이기 위해서, 개발자는 끊임없는 고심을 통해 더 좋고, 더 나은 개발을 할 수 있어야 하기 때문이다.<br><br>
미래의 우리 소비자들에게 남들과는 다른, <span style="color:green">***Carefree*** 한 서비스를 제공하기 위해 Data Structure 을 학습한다.</span><br>

## 프로그램의 효율성 측정: Execution time
```
프로그램의 효율성 측정 방법 1. Execution time
```
> **- Execution time을 측정하는 데에는 두 가지 방법이 있다.**
```
1.  Dynamic analysis : 가장 원시적이지만 가장 직관적인 방법이다.
```
<br>
바로 해당 알고리즘을 프로그래밍 언어로 작성하여<br><span style="color:green">`Prototype을 개발 후 execute 해보는 것이다.`</span><br><br>
<img src="/assets/images/INU/Algorithm_After_EDF.png" alt="Algorithm_After_EDF_Procdess" width="100%" min-width="200px" itemprop="image"><br>
위 사진은 운영체제 수업 실습 과정에서 RM algorithm 과 EDF algorithm을 직접 분석해 본 것인데, 동일한 Simulation Environment 에서 동일한 Task를 처리하는 것 임에도<br><span style="color:blue">***`어떠한 방식의 algorithm을 적용하는지에 따라 수행 능력이 달라지는 것을 볼 수 있다.`***</span><br><br>
- 아쉽게도 Dynamic analysis는 단점이 존재한다.<br>당연히, ***Prototype 을 구현하고 테스트 해야 한다는 것 자체가 단점이다.***<br>
- 또한 본문의 Simulation 처럼, 같은 Environment에서 Prototype을 구현하고 테스트 해봐야 한다는 것이다.<br>
- 더 뛰어난 Environment에서는 알고리즘의 Execution time이 줄어들 수 있기 때문이다.<br>
- 이와 같은 문제점 덕분에 <span style="color:green">`Static analysis, 알고리즘의 복잡도 분석방법`</span>이 개발되었다.<br>
>
```
2.  Static analysis : Complexity analysis (알고리즘의 복잡도 분석)
```





<br><br><br>
[처음으로~](#){: .btn .btn--primary }



`참고: 나무위키` [Data_Structure]()<br>
<span style="color:grey">`참고: C언어로 쉽게 풀어쓴 자료구조 <개정 3판> 천인국, 공용해, 하상국 지음`</span><br><br><br>





### Task Lists
> 
- [x] Data Structure : 알고리즘의 성능 분석
- [x] 프로그램의 효율성 측정 방법 1. Execution time
- [x] Dynamic analysis
- [x] Static analysis : Complexity analysis (알고리즘의 복잡도 분석)