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

데이터를 분석하기 전 도메인에 대한 이해를 위해 사전학습을 실시

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

A~D등급은 2천만원 미만의 대출이 주를 이루었고, E~G등급은 2천만원 이상의 대출이 주를 이루었다.

2천만원이 기준인 이유는 데이터에서 최대 대출금액이 4200만원으로 중간 정도의 2천만원으로 분포를 비교하고자 하였다.

![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/d577c47c-039a-48b0-af27-636cf6718dc6)


























