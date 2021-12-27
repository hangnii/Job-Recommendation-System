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
- 6.[REVIEW](#6-REVIEW)

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
KNOW 조사는 다양한 직업에 종사하고 있는 재직자에 대하여 매년 다른 주제의 설문지로 직무 관련 조사를 수행하고 있으며, 최근 3년에는 다음과 같은 내용으로 설문조사가 진행되었다.
</br>
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
설문 조사는 리커트 척도 방식과 주관식 답변 조사로 진행되었으며, 설문지의 내용은 아래의 예와 같다.
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
[2020: 업무수행능력 및 가치관](https://github.com/dss-nklkb-1th/ml-repo-2/blob/main/data/2020%EB%85%84_KNOW_%EC%9E%AC%EC%A7%81%EC%9E%90%EC%A1%B0%EC%82%AC_%EC%84%A4%EB%AC%B8%EC%A7%80.pdf)
</br>
## 3. 데이터 전처리
### 3-1. 데이터셋
2018년도 데이터 설문 파일에는 **총 141개**의 column(문항)
2019년도 데이터 설문 파일에는 **총 153개**의 column(문항)
2020년도 데이터 설문 파일에는 **총 185개**의 column(문항)으로 구성되어 있다.
<p align="center">
	<img src = "https://user-images.githubusercontent.com/68809022/147457779-fed7c81e-0983-4203-9097-e83a2fe04922.png" width="100%" height="100%"/>
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
### Test Accuracy
Classifier<img width=200/>    | Train Score <img width=200/> | Test Score<img width=200/>
------------- | -------------| -------------
Random Forest  | 1.000000 | 0.522756
Decision Tree  | 1.000000 | 0.218078
AdaBoost  | 0.007274 | 0.005689
Logistic Regression  | 0.408918 | 0.248420
LGBM  | 0.228653 | 0.091024

Random Forest Classifier의 Test Accuracy가 5개의 모델 중 가상 뛰어난 성능을 보여주었다.

하지만, 모든 분류기의 test score 가 train score보다 낮은 것으로 보아 과적합이 우려가 되지만, **정답라벨이 500개가 넘는 다는 것과**, **한 라벨 당 학습 데이터가 최대 16개 였던 것을 고려한다면** 나쁘지 않은 학습 결과라고 판단하였다.

## 5. 모델링

## 6.  REVIEW

## 역할

