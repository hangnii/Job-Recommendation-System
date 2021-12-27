# ML Job Recommendation (머신러닝 기반 직업 추천 알고리즘)
<p align="center">
	<img src="https://user-images.githubusercontent.com/68809022/147449868-01bfe8e0-c4b9-46ff-9c02-467a784d7d22.png" width="70%" height="50%">
</p>

## Introduction
	- 개인의 성격, 역량, 능력을 설문지로 조사하여 직업을 추천해주는 모델입니다.

----
## Contents
- 1.[프로젝트 소개](#1-프로젝트-소개)
- 2.[데이터 개요](#2-데이터-개요)
- 3.[데이터 전처리](#3-데이터-전처리)
- 4.[시각화 및 분석](#4-시각화-및-분석)
- 5.[모델링](#5-모델링)
- 6.[추천시스템](#6-추천시스템)
- 7.[REIVEW](#7-REVIEW)

----
## 1. 프로젝트 소개
	1) KNOW(한국직업정보) 설문 데이터셋을 활용한 직업 추천 알고리즘 개발

	2) 직업과 연관이 높은 설문지 문항 분석 및 영향변수 발굴
</br>

## 2. 데이터 개요
### 2-1. 데이터 출처 : 한국직업정보(Korea Network for Occupations and Workers; KNOW)시스템
KNOW(한국직업정보) 재직자 조사는 한국고용정보원이 **청소년과 성인의 진로 및 경력 설계, 진로 상담, 구인, 구직** 등의 도움을 주기 위해 2001년부터 개발, 운영하고 있는 조사이다.
</br>
</br>
KNOW 조사는 다양한 직업에 종사하고 있는 재직자에 대하여 매년 다른 주제로 직무 관련 조사를 수행하고 있으며, 최근 3년에는 다음과 같은 내용으로 설문조사가 진행되었다.
</br>

#### 연도별 직무 관련 설문지 조사: 
[2018: 업무환경 및 흥미](https://github.com/dss-nklkb-1th/ml-repo-2/blob/main/data/2018%EB%85%84_KNOW_%EC%9E%AC%EC%A7%81%EC%9E%90%EC%A1%B0%EC%82%AC_%EC%84%A4%EB%AC%B8%EC%A7%80.pdf)
</br>

[2019: 지식 및 성격](https://github.com/dss-nklkb-1th/ml-repo-2/blob/main/data/2019%EB%85%84_KNOW_%EC%9E%AC%EC%A7%81%EC%9E%90%EC%A1%B0%EC%82%AC_%EC%84%A4%EB%AC%B8%EC%A7%80.pdf)
</br>

[2020: 업무수행능력 및 가치관](https://github.com/dss-nklkb-1th/ml-repo-2/blob/main/data/2020%EB%85%84_KNOW_%EC%9E%AC%EC%A7%81%EC%9E%90%EC%A1%B0%EC%82%AC_%EC%84%A4%EB%AC%B8%EC%A7%80.pdf)
</br>

***

### 2-2 설문지 내용(2018년, 2019년, 2020년)
#### 설문지 조사 방식
설문 조사는 리커트 척도 방식과 주관식 답변 조사로 진행되었으며, 설문지의 내용은 아래의 예시와 같다.
</br>
#### - 리커트 척도 조사 방식
<p align="center">
	<img src="https://user-images.githubusercontent.com/68809022/147454014-e5395674-796a-4e1a-889c-327aded94fb9.png" width="60%" height="60%"/>
</p>

#### - 주관식 답변 조사 방식
<p align="center">
	  <img src="https://user-images.githubusercontent.com/68809022/147454079-e13678e7-7a35-4457-92fd-89804ad67739.png" width="60%" height="60%"/>
</p>

***

#### - 설문지 문항
[2018: 업무환경 및 흥미](https://github.com/dss-nklkb-1th/ml-repo-2/blob/main/data/2018%EB%85%84_KNOW_%EC%9E%AC%EC%A7%81%EC%9E%90%EC%A1%B0%EC%82%AC_%EC%84%A4%EB%AC%B8%EC%A7%80.pdf)
</br>
[2019: 지식 및 성격](https://github.com/dss-nklkb-1th/ml-repo-2/blob/main/data/2019%EB%85%84_KNOW_%EC%9E%AC%EC%A7%81%EC%9E%90%EC%A1%B0%EC%82%AC_%EC%84%A4%EB%AC%B8%EC%A7%80.pdf)
</br>
[2020: 업무수행능력 및 가치관](https://github.com/dss-nklkb-1th/ml-repo-idx column을 포함한 2/blob/main/data/2020%EB%85%84_KNOW_%EC%9E%AC%EC%A7%81%EC%9E%90%EC%A1%B0%EC%82%AC_%EC%84%A4%EB%AC%B8%EC%A7%80.pdf)
</br>
## 3. 데이터 전처리
### 3-1. 데이터셋
제공된 파일들에선,

2018년도 데이터 설문 파일에는 idx column을 포함한 **총 141개**의 column(문항)

2019년도 데이터 설문 파일에는 idx column을 포함한 **총 153개**의 column(문항)

2020년도 데이터 설문 파일에는 idx column을 포함한 **총 185개**의 column(문항)으로 구성되어 있다.

<p align="center">
	<img src = "https://user-images.githubusercontent.com/68809022/147472919-2abff91f-1e34-4fbf-a5ee-de4c055d3e0c.png" width = "100%" height "100%">
</p>

### 3-2. 주요 컬럼 선택
모든 컬럼(141 + 153 + 185)개를 다 사용하기엔 그 수가 많으므로 선택적으로 취할 필요가 있었다.
	- 기준 1) 같은 직업을 가진 재직자들 간 응답이 유사했던 문항 위주로 선택
	- 기준 2) 프로젝트 목적에 적합한 문항 위주로 선택
	


### 3-3. 데이터셋
### 3-4. 데이터셋
### 3-5. 데이터셋
### 3-7. 데이터셋
### 3-8. 데이터셋
### 3-9. 데이터셋
### 3-10. 데이터셋

## 4. 시각화 및 분석


## 5. 모델링
***

### 5-1. Test Accuracy from 5 Classifiers
Classifier<img width=200/>    | Train Score <img width=200/> | Test Score<img width=200/>
------------- | -------------| -------------
Random Forest  | 1.000000 | 0.522756
Decision Tree  | 1.000000 | 0.218078
AdaBoost  | 0.007274 | 0.005689
Logistic Regression  | 0.408918 | 0.248420
LGBM  | 0.228653 | 0.091024

Random Forest Classifier의 Test Accuracy가 5개의 모델 중 가상 뛰어난 성능을 보여주었다.

하지만, 모든 분류기의 test score가 train score보다 낮은 것으로 보아 과적합이 우려가 되지만, **정답라벨이 500개가 넘는다는 것과**, **한 라벨 당 학습 데이터가 최대 16개였던 것을 고려한다면** 나쁘지 않은 학습 결과라고 판단하였다.

***

### 5-2. 교차 검증(Stratified 5-fold Cross Validation)
<p align = "center">
	<img src = "https://user-images.githubusercontent.com/68809022/147464637-5ce0cdf3-c0ec-4eb9-9c97-641135cb8f78.png" width="80%" height="80%">
</p>

수행 결과 대부분 모델에서 **정확도의 표준편차가 0.01 이하** 인 것으로 보아 **과적합이 아닌 것으로 판단**하였다.

<p align = "center">
	<img src = "https://user-images.githubusercontent.com/68809022/147464357-930d56a3-c766-49f3-80a1-91749c41290b.png" width = "80%" height = "80%">
</p>

***

### 5-3. Random Forest Classifier 성능 개선 작업
1. Optimum **max_depth** value: **34**

	Grid Search Cross Validation 방법을 이용하여 max_depth 범위를 [25, 40]으로 한 결과, **max_depth가 34일 때, test accuracy 값이 0.5054406347180608**로 가장 좋은 결과 값이 나왔다.

2. Optimum **n_estimator** value: **900**

	max_depth를 34로 설정한 후, n_estimator 값을 100씩 변경하며 테스트해본 결과, **900**일 때 가장 좋은 결과 값이 나왔다.

<p align ="center">
	<img src = "https://user-images.githubusercontent.com/68809022/147472334-a9a31982-5919-427f-b2af-420573e41862.png" width = "100%" height = "100%">
</p>

***

### 5-4. 최종 모델 with Hyper Paramter: Random Forest Classifier(max_depth = 34, n_estimators = 900)
<p align="center">
	<img src = "https://user-images.githubusercontent.com/68809022/147465288-eb622aed-c2a1-44a1-b3a4-a174d782260d.png"  width = "60%" height="60%">
</p>

#### 최종 모델 Accuracy : 0.6194690265486725

***

### 5-5. 직업 추천 모델 :
하나의 직업에 국한되어 있지 않고, 설문 조사에서 취합한 개개인의 역량에 적합한 직업의 다양한 가능성을 보여주기 위해

최종모델에서 추천된 모델에서 상위 3개, 5개, 10개 데이터별로 묶어서 label 값이 포함되어 있는지 확인해보았다.
<p align ="center">
	<img src = "https://user-images.githubusercontent.com/68809022/147474941-f4721bf8-f539-42a5-a06c-50e6c07f6af8.png" width = "100%" height="100%">
</p>						

최종모델에서 추천된 직업이 **상위 3개에 포함되어 있을 확률은 75%**, **상위 5개에 포함되어 있을 확률은 81%**, **상위 10개에 포함되어 있을 확률은 88%** 로 확인되었다.

## 6.  추천시스템
설문 조사들을 통하여 응시자의 개인 성격, 능력, 역량에 적합한 **직업 상위 10개를 추천**해준 후,

현직자가 평가한 업무 만족도와 직업 전망, 사회적 평판을 고려할 때, 추천된 **상위 10개의 직업에서 Best3**를 선정하여 알려주는 **서비스를 구현** 하였다.

***

### 6-1. 데이터 수집

총 123개의 문항으로 구성된 설문지를 직접 만들었으며, 아래의 설문지에는 총 9가지의 섹션으로 "업무 환경", "물리적 환경", "업무 특성", "업무에 대한 흥미", "본인의 성격", "지식 역량", "업무 수행 능력", "본인의 가치관", "종합(근무하고 싶은 업종, 학력, 직업 선택에 있어서 중요한 요소, 등)"에 관련된 질문들로 구성되어 있다.

[설문 조사 응시](https://docs.google.com/forms/d/1YA3iA2KJQQtdmrN7iGbOecF6bMXA4eYk75ls2teH5BA/edit?usp=drive_web)

<p align="center">
	<img src = "https://user-images.githubusercontent.com/68809022/147476727-5f4ddb0c-9cd5-40e7-98fe-bbc28ebe06fc.png" width = "100%" height="100%">
</p>

***

### 6-2. Radar Chart를 통한 시각화
추천된 직업 리스트 중 현직자가 추천하는 best3에 대하여 평가한 업무 만족도(satisfaction), 직업 전망(prospects), 사회적 평판(reputation), 수입(income), 직업의 안정성(stability)를 Radar Chart를 통하여 결과물을 표현하였다.
<p align = "center">
	<img src = "https://user-images.githubusercontent.com/68809022/147476563-8497b9de-07ff-4a74-aefd-71f12547a7f5.png" width = "60%" height = "60%">
</p>

## 8. REVIEW


## 역할

