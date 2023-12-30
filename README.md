# 신용카드 사용자 연체 예측 AI 경진대회

<br/>

## 1. 배경 및 목적

- 신용카드 사용자 데이터를 보고 사용자의 대금 연체 정도를 예측하는 예측 알고리즘
- 3진 분류(0,1,2)
- 평가지표: Log-Loss

<br/>

## 2. 주최 기관 및 참가 인원

- 주최: 2022 D&A Machine Learning Session
- 주관: DACON
- 참가 인원: 40명
  
<br/>

## 3. 프로젝트 기간 

- 2022.10 ~ 2022.11 (2개월)

<br/>

## 4. 프로젝트 설명 
![Untitled1](https://github.com/Ji-eun-Kim/DnA-ML-competition/assets/124686375/51a35b5d-b4bb-4136-8e81-2edf8833c0c6)  
본 대회는 신용카드 사용자들의 개인 신상정보 데이터로 사용자의 신용카드 대금 연체 정도를 예측하는 대회다. 종속변수는 사용자의 신용도를 0, 1, 2의 값으로 표현한 credit 열이었다. 분류모델 중, 높은 성능을 기대할 수 있는 트리 기반의 randomforest, LGBM, CatBoost, XGB 모델을 생성하고 이들을 앙상블 하여 성능을 높이는 전략을 세워 본 대회를 시작하였다.

   전처리의 경우, 데이터의 형태에 따라 전처리를 수행하였다. 수치형 변수의 이상치 처리 부분에서 음수를 지니는 columns(출생일, 신용카드 발급 월)는 양수로 바꾸어 주었으며, 연간 소득의 경우, 표준정규분포로 전환 후, -3 이하 및 3 이상인 값들을 clip 해주었다.  범주형 변수의 경우, 휴대전화 여부 column이 1로 이루어져 있어 열을 삭제하였고, 직업 유형 column에서 적히지 않은 칸은 unemployed로 처리하였다. 

   피처 엔지니어링의 경우, **총 102개의 피처**를 생성했으며, 크게 4**가지 기준(income_total, begin_month, DAYS_EMPLOYED, DAYS_BIRTH)** 으로 피처를 생성하였다. 시각화 및 데이터 분석을 통해 유의미한 피처들을 생성했으며, 이후 추가적인 방식으로 **수치형 변수** 들을 이용한 피처 생성으로는 사분위수로 범주화하는 방법과, 수치형 변수들끼리 곱하는 등의 계산을 통해서 피처를 생성하였고, **범주형 변수**들로는 범주형 변수들끼리 더해 새로운 범주형 변수를 생성하는 방법과, 범주형 피처로 groupby 후 수치형 피처의 평균, 합계, 표준편차를 구해 대입하는 방법을 이용하여 더 많은 피쳐들을 생성하였다. 

   이후 Feature Selection을 통해 모델에 적합한 feature을 선택하였다. Embedded Method를 활용한 Select From Model을 사용하였으며, feature 간 상관관계가 높은 것 중 feature importance가 더 작은 변수를 삭제해주었다. 

   스케일링과 인코딩의 경우, 수치형 변수들 간의 값 범위가 일정치 않아 **MinMaxScaler**  **와 로그변환** 을 함께 사용하여 스케일링을 진행하였고, 범주형 변수의 경우 **Encoding** 을 진행하였다. 이진 변수인 gender, car, reality에 대해서는 0, 1로 **binary encoding** 을, 값들에 순서를 가지고 있던 edu_type은 **ordinal encoding** 을 진행하였고, 나머지 object type의 범주형 변수들은 **label encoding**으로 통일하여 인코딩을 진행하였다. 

   모델링은 분류모델 중, 높은 성능을 기대할 수 있는 트리 기반의 모델들을 사용하였다. 단일 모델로 총 4가지를 사용했으며(Random Forest, LGBM, CatBoost, XGBoost), **Optuna** 를 이용한 하이퍼파라미터 최적화를 진행하고, 선택된 파라미터들로 모델을 학습시켰다. 최종적으로 모델링한 4개의 서로 다른 모델들을 가지고 **가중평균을 활용 앙상블**을 진행하여 성능의 개선을 기대하였으나, 앙상블 한 결과와 비교했을 때, 단일 모델에서 가장 좋은 성능을 보인 XGBoost의 스코어보다 좋은 결과를 내지는 못하여, **단일 모델로 가장 좋은 성능을 보인 XGBoost** 를 최종 모델로 선정하였다.

<br/>

## 5. 팀원 및 담당 역할
**<팀원>**
- 전공생 5명   

  

    
  
**<담당 역할>**

- 데이터 전처리 및 피처 엔지니어링
- 머신러닝, LGBM, CatBoost 모델링 및 하이퍼 파라미터 튜닝
- 가중평균 앙상블
- 코드 정리

<br/>

## 6. 발표 자료 및 추가 자료

- 발표 자료  
https://drive.google.com/file/d/1PKe8akHGVNen8albaZxQNIa2oTAHUGg1/view?usp=drive_link

- 데이터  
https://drive.google.com/drive/folders/1MxeoA6MYSXsL33IYHi8pKF88CJw0Dx4X?usp=drive_link

- 성능
![성능 캡쳐 사진](https://github.com/Ji-eun-Kim/DnA-ML-competition/assets/124686375/c01b70f7-f0df-41ad-aed3-c1bf6b31967c)
