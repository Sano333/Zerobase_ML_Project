![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/d6313c1b-547d-4dad-9617-86e8032d14ee)

-----

# Introduction

1. 프로젝트명 : 고객 정보 기반 대출 등급 예측 AI 모델 개발
2. 수행자 : 김민수(조장), 이진주, 채주은
3. 수행 기간 : 1달 (2024.01.25 ~ 2024.02.22)
4. 목표 : 높은 성능을 가지는 예측 모델 개발하기
-----

# Contents

* 1.프로젝트 개발 계획
    - 주제 선정배경
    - 사전학습
    - 프로젝트 개요
    - 데이터 출처
* 2.EDA
    - 데이터 전처리
* 3.시각화
    - 상관계수 확인
    - 근로기간(Unknown) 영향 분석
    - 대출등급별 경향 파악
* 4.모델링
    - 모델 기본 설계
    - 모델 성능 평가
* 5.결론
    - 최종모델
    - Insight 도출
 
-----

# 1. 프로젝트 개발 계획

## 주제 선정배경

고객 정보 분석을 통해 대출등급을 예측하여 금융사 및 고객에게 도움을 주고자 한다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/bb90b796-f08e-4a51-9f88-34e67e1b0817)

## 사전학습

데이터를 분석하기 전 도메인에 대한 이해를 위해 사전학습을 실시하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/9edc635f-9b7c-4835-a65a-6a4290f023ac)

## 프로젝트 개요

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/71e52e74-4eb8-49a9-9b81-439f598b8821)

## 데이터 출처

https://dacon.io/competitions/official/236214/data

데이콘에서 진행한 고객 대출등급 분류 AI 해커톤 데이터를 사용하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/c399baf1-b44a-4cd3-9d95-1fed8b980886)

-----

# 2. EDA

## 데이터 전처리

✅ 데이터 특성 파악

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/70797a4c-cbc1-4903-a83b-efab7d7e3e55)

✅ 전처리 로직

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/de2d0167-1c8a-41f0-9c8d-5d796f09f0d4)

✅ Outlier 처리 (부채 대비 소득 비율)

이상치 처리 후 분포가 균일해짐을 확인하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/0c991eb7-002f-4cea-aa1b-6ed57076488a)

✅ Outlier 처리 (최근 2년간 연체 횟수)

1인 1대출을 전제로 2년간 연체 횟수가 24번을 초과하는 데이터를 이상치로 판단 후 제거하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/9dc22250-4824-460c-b377-a30f0da313ca)

✅ Outlier 처리 (주택소유상태)

'ANY'라는 데이터가 하나만 존재하므로 이상치로 판단 후 제거하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/821a25c2-a0ae-4f81-a8fe-a651142ae64e)


✅ 데이터 수치화 (대출기간)

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/b99ea7b6-d3c9-49d4-bf3a-b86814293ed5)

✅ 데이터 수치화 (근로기간)

근로기간에는 Unknown이라는 데이터가 존재하는데, 전체 데이터의 5%를 차지하기 때문에 이상치로 판단하지 않고 

이후 모델링 단계에서 여러가지 시도를 통해 성능을 비교할 예정이다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/cca725bc-3d16-4775-b5e6-20d309e85d29)

-----

# 3. 시각화

📊 상관계수 확인

대출기간, 총상환이자가 상대적으로 대출등급과 높은 상관계수를 보였다. (0.44)

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/3fd6998c-d17d-420b-876b-eaa57c65449e)

📊 target-feature 관계 시각화

대출 등급이 낮아질수록 대출금액, 총상환이자, 부채 대비 소득 비율, 총연체금액은 증가하는 경향을 보이고

연간소득과 총상환원금은 감소하는 경향을 보였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/e8b864ed-a9a4-4c2c-b30d-49a1350f4e6f)

📊 근로기간에 따른 특성 분포

근로기간의 Unknown 데이터의 경우, MORTGAGE가 가장 많은 비중을 차지하지만 
다른 집단과 비교하였을 때 OWN의 비중이 상대적으로 높게 나타난다. 

ʻOWN’이 많은 Unknown에는 연소득이 높은 사람들이 많을 것으로 예상했다.

그러나 데이터를 확인해보니 연간소득 1억원 미만의 분포가 89%를 차지했다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/80198cd1-688f-43d4-9c68-a59b9b1812e9)

📊 Unknown 데이터 유무에 따른 경향 파악

Unknown을 포함한 데이터와 제외한 데이터의 대출 등급별 주택소유상태를 비교한 결과

Unknown 값을 제외하여도 전체적 경향은 크게 변하지 않았다.

이를 통해 Unknown 값이 모델링 성능에 크게 영향을 미치지 않을 것이라고 판단하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/72e0184d-5e8b-4cef-b36d-89ce5132574b)

📊 대출 등급별 대출 특성 시각화

A~C등급은 주로 3년짜리 대출이 많았고, D등급 부터는 5년짜리 대출이 많았다.

대출 등급이 높을 수록 상환능력이 좋아서 짧게 설정했거나, 금리가 낮기 때문에 이자 부담이 상대적으로 적으므로 대출 기간을 짧게 설정한 것으로 판단하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/0cc4dc3e-bfb2-468b-80c1-85b97be66959)

대출 등급이 높을 수록 고소득자가 많았다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/608888d3-1f7b-47b4-8e9a-afb85367a2d7)

A ~ D등급은 2천만원 미만의 대출이 주를 이루었고, E ~ G등급은 2천만원 이상의 대출이 주를 이루었다.

2천만원이 기준인 이유는 데이터에서 최대 대출금액이 4200만원으로 중간 정도의 2천만원으로 분포를 비교하고자 하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/d577c47c-039a-48b0-af27-636cf6718dc6)

-----

# 4. 모델링

## 모델 기본 설계

정석대로라면 모든 모델과 모든 파라미터에서 Standard, MinMax, Robust 스케일러의 성능을 확인하여 채택해야 하지만
시간 관계상 첫번째 Case에서만 성능을 확인하여 가장 성능이 우수했던 Standard 스케일러를 채택하였다.

하이퍼 파라미터 튜닝의 경우 RandomForest에서 n_estimators, min_sample_leaf, min_sample_split, max_feature, max_depth 5가지 파라미터에 대해
5가지 경우의 수를 매칭(5^5 = 총 3125개의 경우의 수)하여 GridSearch로 탐색하였더니 13시간이 지나도 결과가 출력되지 않아 RandomizedSeach를 이용하여 파라미터를 탐색하였다.

RandomizedSearch의 폴드 수는 5, 경우의 수는 10가지만 돌려서 결과를 출력하였다.

분류문제이기 때문에 StratifiedKFold를 사용하였고, 타깃 데이터의 불균형이 존재하였기 때문에 macro_f1_score를 통해 성능을 검증하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/d5af5cbd-9f1f-4bbf-ba4a-4943e1071931)

## 모델 성능 평가

✅ CASE 1 - 근로기간 Unknown 값 제외 모델링

최고 성능 모델의 파라미터 : XGBClassifier(objective='multi:softmax', n_estimators=100, max_depth=30, learning_rate=0.1, n_jobs=-1, random_state=42)

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/1f097546-f693-4455-bdd5-81fc810456c2)

✅ CASE 2 - 근로기간 Unknown 값 포함 모델링



![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/debfdd20-ba9b-44c5-9666-d0c299df2cd5)

✅ CASE 3 - 근로기간 Unknown 값 KNN Imputer로 대체 후 모델링



![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/593185d2-7705-4535-88b8-72b5e3592dc1)

📊 특성 중요도를 통한 인사이트

CASE 1~3의 모델별 특성 중요도 평균 값을 계산하여 그래프를 그린 결과

총상환원금, 총상환이자, 대출기간에 대한 특성중요도가 높게 나타났다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/7ea5d836-78da-4953-931f-5ca77b4d05d8)

대출등급별 총상환원금과 총상환이자의 분포를 확인해보니 군집이 명확하게 분류되는 것을 확인하였다.

총상환원금 대비 총상환이자가 많을 경우 대출등급이 낮게 나타났다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/a7abf093-966b-4bed-ad08-25aeae88cc3d)

또한 대출기간별로 그룹을 나누어 대출등급별 경향을 확인한 결과 마찬가지로 군집이 명확하게 분류되는 것을 확인하였다.

최종적으로 총상환원금, 총상환이자 그리고 대출기간 3개의 데이터가 대출 등급을 결정하는 핵심 요소임을 확인하였고, 이를 이용하여 후행 모델링을 진행하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/7cb125db-95ab-497e-8030-f870b2adc49c)

✅ CASE 4 - CASE 1~3 결과에서 특성 중요도가 낮은 컬럼 4개 제외 후 모델링

총상환원금, 총상환이자, 대출기간을 이용하여 특성공학을 수행하기 전 임의로 특성중요도가 가장 낮았던 4개 컬럼을 제거한 후 모델링을 진행하였다.

모델 복잡도가 낮아진다고 성능이 무조건 좋아지는 것은 아니지만, 여기에서는 복잡도를 줄여 성능 향상을 얻어냈다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/83303357-b040-4312-b96b-1caf95153d63)

✅ CASE 5 - Feature Engineering 적용 (총상환원금, 총상환이자, 대출기간 이용)

총상환원금, 총상환이자, 대출기간으로 사칙연산, 제곱, 제곱근을 이용하여 파생변수를 생성하였다.

여러가지 시도를 통해 총상환원금과 이자를 대출기간에 곱하고, 나눈 컬럼을 이용하여 모델링 했을 때 최상의 결과를 출력했다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/5a5529b5-735e-45e7-967a-c486a5404c9b)


✅ CASE 6 - CASE 5 결과에서 RFE를 적용 -> 최종결과

RFE를 적용하여 특성 중요도가 가장 높은 컬럼 5개를 이용하여 모델링 한 결과 가장 우수한 성능을 얻어냈다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/5564500c-e101-4754-8649-b3a5a9a44985)

-----

# 5. 결론

## 최종모델

Raw Data에서 여러가지 시도를 통해 특성 중요도를 가지고 특성 공학을 수행한 뒤, RFE를 적용했을 때 최적의 모델 성능을 뽑아낼 수 있었다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/066d3740-9905-416e-88a8-1a42bf2529a7)


## Insight 도출

최종 결과인 85%의 결과가 모델 성능이 좋다/나쁘다를 논하기는 어렵지만, 다양한 시도를 통해 모델 성능을 향상시키는 과정을 지나온 것이 유의미했다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/0b93f699-7572-424a-9856-9013d3813207)

-----

✅ **최종적으로 얻은 인사이트**

1. 모델링으로 얻은 특성중요도를 통해 EDA에서 파악하지 못한 데이터에 대한 새로운 경향을 파악할 수 있었다.
2. 특성 공학을 활용하여 모델 성능을 높일 수 있었다.
3. (분석한 데이터를 기준으로) 대출등급 결정하는 핵심 요소가 총상환원금, 총상환이자 그리고 대출기간임을 확인할 수 있었다.
4. 다양한 시도를 통해 모델 성능을 비교하는 과정에서 의도한대로 성능이 올라간 경우도 있었지만 반대로 낮아진 경우도 있었다. 내가 예측하는 기댓값이 무조건 나올거라는 보장이 없다는 것을 몸소 느꼈다.
5. 하이퍼파라미터 튜닝과 모델 검증에 굉장히 많은 시간이 소요되었다. 빅데이터에서 모델 성능을 높이기 위해 투입되는 자원의 양이 엄청나게 많이드는 것을 경험하였다.

🛑 **한계점**

모든 한계점은 시간이 부족하여 수행하지 못한 점이 많았다.

1. 조금 더 다양한 모델을 사용하지 못한점이 아쉬웠다.
2. RandomizedSearch대신 Gridsearch를 사용했다면 더 좋은 성능을 낼 수 있었을 것이다.
3. 데이터 불균형이 존재했는데, 리샘플링 기법을 사용하지 못한점이 아쉬웠다.
4. 특성 공학을 수행할 때 도메인에 대한 이해를 바탕으로 더 다양한 파생 변수를 생성했었다면 더 좋은 성능을 낼 수 있었을 것이다.
