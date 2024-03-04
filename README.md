![image](https://github.com/Sano333/Zerobase_ML_Project/assets/149456385/d6313c1b-547d-4dad-9617-86e8032d14ee)

-----

# Introduction

* 고객 정보 기반 대출 등급 예측 AI 모델 개발

-----

# Contents

* 1.프로젝트 개발 계획
    - 주제 선정배경
    - 사전학습
    - 프로젝트 개요
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




































