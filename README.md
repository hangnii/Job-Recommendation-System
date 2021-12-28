# ML Job Recommendation (머신러닝 기반 직업 추천 알고리즘)
<p align="center">
	<img src="https://user-images.githubusercontent.com/68809022/147449868-01bfe8e0-c4b9-46ff-9c02-467a784d7d22.png" width="70%" height="50%">
</p>

## Introduction
### 머신러닝 기반 직업 추천 시스템
최근 3년치 KNOW 재직자 조사 데이터를 통합・변형하여 구직자 대상 설문지를 개발하고 응답에 따른 추천 직업을 시각화하여 제시하는 서비스 구현

## Contents
- 1.[프로젝트 소개](#1-프로젝트-소개)
- 2.[데이터 개요](#2-데이터-개요)
- 3.[데이터 전처리](#3-시각화-및-분석)
- 4.[시각화 및 분석](#4-데이터-전처리)
- 5.[모델링](#5-모델링)
- 6.[추천시스템](#6-추천시스템)
- 7.[REIVEW](#7-REVIEW)

----

## 1. 프로젝트 소개

코로나19로 심각해진 취업난 속 직업 선택에 대한 새로운 시각 제공 필요성 절감

참고 기사: ["취준생 86만명 사상최대…세명 중 한명은 공무원 준비"](https://www.mk.co.kr/news/society/view/2021/07/698992/) (작성: 2021.07.20)

☞ KNOW 재직자 조사 데이터를 분석・활용하여 직업과 연관이 높은 설문지 문항 및 영향변수를 발굴하고, 이에 기반한 직업 추천 알고리즘을 개발하고자 함


## 2. 데이터 개요
### 🗃 2-1. 데이터 출처 : 한국직업정보(Korea Network for Occupations and Workers; KNOW)시스템
KNOW(한국직업정보) 재직자 조사는 한국고용정보원이 **청소년과 성인의 진로 및 경력 설계, 진로 상담, 구인, 구직** 등의 도움을 주기 위해 2001년부터 개발, 운영하고 있는 조사이다.
</br>
</br>
KNOW 조사는 다양한 직업에 종사하고 있는 재직자에 대하여 매년 다른 주제로 직무 관련 조사를 수행하고 있으며, 최근 3년에는 다음과 같은 내용으로 설문조사가 진행되었다.
</br>

#### 연도별 직무 관련 설문지 조사: 
[2018: 업무환경(cq) 및 흥미(iq)](https://github.com/dss-nklkb-1th/ml-repo-2/blob/main/data/2018%EB%85%84_KNOW_%EC%9E%AC%EC%A7%81%EC%9E%90%EC%A1%B0%EC%82%AC_%EC%84%A4%EB%AC%B8%EC%A7%80.pdf)
</br>
[2019: 지식(kq) 및 성격(sq)](https://github.com/dss-nklkb-1th/ml-repo-2/blob/main/data/2019%EB%85%84_KNOW_%EC%9E%AC%EC%A7%81%EC%9E%90%EC%A1%B0%EC%82%AC_%EC%84%A4%EB%AC%B8%EC%A7%80.pdf)
</br>
[2020: 업무수행능력(saq) 및 가치관(vq)](https://github.com/dss-nklkb-1th/ml-repo-2/blob/main/data/2020%EB%85%84_KNOW_%EC%9E%AC%EC%A7%81%EC%9E%90%EC%A1%B0%EC%82%AC_%EC%84%A4%EB%AC%B8%EC%A7%80.pdf)
</br>

***

### 🗃 2-2 설문지 내용(2018년, 2019년, 2020년)
#### 설문지 조사 방식
설문 조사는 리커트 척도 방식과 주관식 답변 조사로 진행되었으며, 설문지의 내용은 아래의 예시와 같다.
#### - 리커트 척도 조사 방식
<p align="center">
	<img src="https://user-images.githubusercontent.com/68809022/147454014-e5395674-796a-4e1a-889c-327aded94fb9.png" width="60%" height="60%"/>
</p>

#### - 주관식 답변 조사 방식
<p align="center">
	  <img src="https://user-images.githubusercontent.com/68809022/147454079-e13678e7-7a35-4457-92fd-89804ad67739.png" width="60%" height="60%"/>
</p>

### 🗃 2-3 설문 대상자
DACON측에서 직업 라벨을 포함하여 제공한 25,000여 명의 설문지 조사 데이터를 사용하였다.

## 3. 시각화 및 분석

### 🛰️ 3-1. 연도별 응답자 직군
![image](https://user-images.githubusercontent.com/68809022/147485971-ab898241-175f-450c-84be-4a3df7675db4.png)

- 아래 분석은 2018 ~ 2020년도에 공통적으로 조사된 직업(528)개를 대상으로 한다.
- 2018 ~ 2020년도 모두 "경영·사무·금융·보험직", "연구직 및 공학 기술직", "설치·정비·생산직"에 관련된 직군들의 직업이 많이 포진되어 있으며, "농림어업직" 및 "건설·채굴직" 관련 직군들의 직업은 적게 조사된 것 확인할 수 있다.

### 🛰️ 3-2. 직업 대분류별 임금근로자 연봉
![image](https://user-images.githubusercontent.com/68809022/147486627-33f6a082-ff65-4b0f-99b5-6a93d895e3d4.png)

### 🛰️ 3-2. 직업 대분류별 임금근로자 연봉 (한계값 연봉 1.5억 설정)
![image](https://user-images.githubusercontent.com/68809022/147486889-8471c6a8-22c0-4ca0-a912-73699a24d60f.png)

- 2018~2020년 모두 "경영·사무·금융·보험직"에 포함되는 97개의 직업들이 다른 직군들에 비해 연봉이 다소 높은 것을 확인 할 수 있다. 
- "보건·의료직"에는 의사뿐만 아니라, 간호사, 간호조무사, 약사 등 다양한 의료직군에서 종사하는 재직자들이 포함되어 있기 때문에 연봉의 분포도가 넓게 퍼져 있는 것을 볼 수 있다.
- 2020년도의 경우, "영업·판매·운전·운송직"의 연봉이 다른 년도에 비해서 크게 증가한 것을 확인 할 수 있다. Covid19로 인해 택배와 배달 수요가 늘어나면서 이 직군에 종사하는 재직자들의 최저 임금 또한 상승한 것으로 보인다.

### 🛰️ 3-3. 연도별 응답자 중, 고소득 직업
![image](https://user-images.githubusercontent.com/68809022/147487627-53f80599-2c88-4914-b19a-2129b212012a.png)

- 4-2의 boxplot그래프에서 outlier에 포함된 대상자를 위주로 고소득 직업을 조사하였다.
- 2018년도 설문조사에 참여한 응딥자 중, 제품 생산관련 관리자가 6억으로 가장 높은 연봉을 받고 있었으며, 일부 개그맨 및 코미디언과 스포츠 감독 및 코치 또한 많은 연봉을 받고 있는 것으로 확인되었다.
- 2019년도 설문조사에 참여한 응답자 중, 기업 고위임원들이 4~5억으로 가장 높은 연봉을 받은 것으로 확인되었으며, 그 외에 운동 선수, 의사, 항공기 조종사 순으로 포함된 것으로 확인되었다.
- 2020년도 설문조사에 참여한 응답자 중, 의사들이 가장 높은 연봉을 받은 것으로 확인되었으며, 의사외의 직업으로는 기업 고위임원이 포함되었다.

### 🛰️ 3-4. Reputation (수정중)
### 🛰️ 3-5. Income (수정중)
### 🛰️ 3-6. Stability (수정중)
### 🛰️ 3-7. Satisfaction (수정중)
### 🛰️ 3-8. Prospects (수정중)

## 4. 데이터 전처리
총 400 여개의 column과 25,752명의 재직자 설문 조사 데이터를 분석하여 최종, **123개의 column으로 이뤄진 7,906명의 재직자 설문조사로 재구성하여** 사용했습니다.

### 4-1. 설문조사 답안 밀림 현상
- 데이터를 불러오기 이전에 csv파일들을 Excel에서 열어 확인해보니 주관식으로 작성되었어야 할 항목에 일부 숫자가 포함된 것 발견 (2018, 2019년 파일)
- csv 파일의 식별자 인식 문제로 일부 행에 대하여 밀려서 표기된 부분이 있는 것으로 파악되었으며, 해당 부분을 수동으로 바로잡아 별도의 파일로 저장하여 사용

### 4-2. 설문조사 '공백' 답안 대체
- **객관식 문항**에서 공백으로 표기된 응답은 해당 능력 혹은 지식 등이 직무에서 중요하지 않아 특별한 수준이 요구되지 않음을 의미
- **주관식 문항**에서 공백으로 표기된 응답은 학력이 중졸 이하라서 전공 작성란을 비워둬야 했음을 의미

- 설문조사의 특정 목적에 의해 공백으로 표시된 답안들을 모두 0으로 대체함

### 4-3. 설문조사 문항 선별
2018년도 데이터 설문 파일에는 idx column을 포함한 **총 141개**의 column(문항)

2019년도 데이터 설문 파일에는 idx column을 포함한 **총 153개**의 column(문항)

2020년도 데이터 설문 파일에는 idx column을 포함한 **총 185개**의 column(문항)

<p align="center">
	<img src = "https://user-images.githubusercontent.com/68809022/147472919-2abff91f-1e34-4fbf-a5ee-de4c055d3e0c.png" width = "100%" height "100%">
</p>
	

통합 설문 개발 시 3년치 조사의 모든 문항을 다 사용하기엔 중복 문항을 제외해도 400여 개로 그 수가 너무 많으므로 아래의 두가지 분석 방법에 기반하여 문항 수를 줄였다.

- i. 통계 분석 기반
	<p align ="center">
		<img src = "https://user-images.githubusercontent.com/68809022/147523739-da75b6a9-a838-4ab7-83f5-d516c7fd6464.png" width = "90%" height = "90%">
	</p>
	
	- 같은 직업을 가진 재직자들 간 응답이 유사했던 문항 위주로 선택 시도
	- 각 문항에 대하여 직업별 표준편차를 살펴보고 그 평균이 1.5를 넘는 객관식 문항은 모두 제외
	  (단, bq1은 업종에 대한 문항으로 21개 보기 중 택한 것이라 편차가 크게 나올 수밖에 없음을 참작하여 예외적으로 포함시킴)
	- 문항 분류별 균형을 고려하여 기준을 1.3 또는 1.0으로 적용한 경우도 있음

- ii. 내용 분석 기반
	- 프로젝트 목적에 적합한 문항 위주로 선택
		- ex) 근로소득 관련 문항: 직업에 따라 소득 수준이 상이하여 직업을 추천받고자 하는 사람이 희망 연봉을 특정하여 답하기는 어려울 것으로 판단되므로 제외
	- 특정 능력이나 지식 등에 대하여 중요도를 묻는 문항과 요구되는 수준을 묻는 문항이 연결되어 나타나는 경우, 수준을 중심으로 문항 통합

- ☞ 최종적으로 122개 문항을 선정, 사용할 컬럼은 knowcode 포함 123개로 정리
	<p align="center">
		<img src = "https://user-images.githubusercontent.com/68809022/147523838-2dd6abd5-9cd6-41ce-a346-15a69de30c20.png" width = "100%" height = "100">
	</p>


### 4-4. knowcode(직업코드)별 응답자 수 정리 및 DataFrame 병합
- KNOW 재직자 조사는 매년 동일인이 응답하는 게 아닌데다 응답자 수도 상이하여, 통합 설문 형태에 맞춰 3년치 DataFrame을 병합하고자 할 때 기준이 될 키값이 존재하지 않음
- 이를 해결하기 위해 3개년의 직업별 응답자 수를 통일하여 동일인의 응답인 것처럼 임의로 매치하여 이어붙이기로 결정

	<p align = "center">
		<img src = "https://user-images.githubusercontent.com/68809022/147524042-9001159f-6df2-47d0-95f8-feb6b4eeaa3b.png" width="30%" height="30%">
	</p>

- 예를 들어 특정 직업이 2018년에 18명, 2019년에 15명, 2020년에 15명 조사됐다면, 15명까지 데이터를 차례로 이어붙이고 이후에 남는 2018년의 3명 분 데이터는 사용하지 않음

### 4-5. 전공 컬럼 가공 및 라벨 인코딩
- '경영', '경영학', '경영과', '경영학과' 등 동일 전공을 조금씩 다르게 표기한 경우가 많음
- 라벨 인코더 적용 시 이러한 답안이 모두 서로 다른 전공으로 취급되는 일을 줄이고자 단어 마지막에 쓰인 '학', '과', '학과'를 제거
(코사인 유사도를 이용한 자연어처리를 시도할 시 '의예', '의류'가 같은 전공으로 묶이는 등의 문제가 우려됨 - 추후 다른 보완 방법 고안 필요)

- 이후 라벨 인코더 적용

## 5. 모델링


***

### 🔩 5-1. Test Accuracy from 5 Classifiers
Classifier<img width=200/>    | Train Score <img width=200/> | Test Score<img width=200/>
------------- | -------------| -------------
Random Forest  | 1.000000 | 0.522756
Decision Tree  | 1.000000 | 0.218078
AdaBoost  | 0.007274 | 0.005689
Logistic Regression  | 0.408918 | 0.248420
LGBM  | 0.228653 | 0.091024

Random Forest Classifier의 Test Accuracy가 5개의 모델 중 가장 뛰어난 성능을 보여주었다.

하지만 모든 분류기의 test score가 train score보다 낮은 것으로 보아 과적합이 우려 되지만, **정답 라벨이 530개가 넘는다는 것과**, **한 라벨 당 학습 데이터가 최대 16개였던 것을 고려한다면** 나쁘지 않은 학습 결과라고 판단하였다.

***

### 🔩 5-2. 교차 검증(Stratified 5-fold Cross Validation)
<p align = "center">
	<img src = "https://user-images.githubusercontent.com/68809022/147464637-5ce0cdf3-c0ec-4eb9-9c97-641135cb8f78.png" width="80%" height="80%">
</p>

수행 결과 대부분 모델에서 **정확도의 표준편차가 0.01 이하** 인 것으로 보아 **과적합이 아닌 것으로 판단**하였다.

<p align = "center">
	<img src = "https://user-images.githubusercontent.com/68809022/147464357-930d56a3-c766-49f3-80a1-91749c41290b.png" width = "80%" height = "80%">
</p>

그래프에서 알 수 있듯이 Random Forest Classifer의 값이 다른 분류 모델들에 비해서 좋은 것을 확인 할 수 있다.
***

### 🔩 5-3. Random Forest Classifier 성능 개선
1. ⚙**max_depth** value: **34**

	Grid Search Cross Validation 방법을 이용한 결과, 
	
	**max_depth가 34일 때, test accuracy 값이 0.505440634**로 가장 좋은 결과 값이 나왔다.

2. ⚙**n_estimator** value: **900**

	max_depth를 34로 설정한 후, n_estimator 값을 100씩 변경하며 테스트한 결과, 
	
	**900**일 때 가장 좋은 결과 값이 나왔다.

	<p align ="center">
		<img src = "https://user-images.githubusercontent.com/68809022/147472334-a9a31982-5919-427f-b2af-420573e41862.png" width = "100%" height = "100%">
	</p>
	
	max_depth를 34로 설정한 후, n_estimators 값을 100씩 증가시키며 stratified 5-fold cross validation 결과(accuracy)를 비교해 보았다. 평균값은 900에서 최대로 나타났고, 표준편차는 300에서 가장 낮게 나타나긴 했지만 900에서 0.01456이라는 양호한 수치를 보이며 다시 극소를 이룬다. 따라서 n_estimators는 900일 때 가장 좋은 것으로 판단했다.
	

***

### 🔩 5-4. 최종 모델 with Hyper Paramter: Random Forest Classifier(max_depth = 34, n_estimators = 900)
<p align="center">
	<img src = "https://user-images.githubusercontent.com/68809022/147465288-eb622aed-c2a1-44a1-b3a4-a174d782260d.png"  width = "60%" height="60%">
</p>

#### 최종 모델 Accuracy : 0.6194690265486725

<p align = "center">
	<img src = "https://user-images.githubusercontent.com/68809022/147526937-8bf0fbfe-2341-4b66-b391-5dbb7f8c74c0.png" width = "70%" height="70%">
</p>

설문조사를 바탕으로 학습한 최종모델에서는 아래의 feature들이 직업을 추천하는데 큰 영향을 끼친다는 것을 알 수 있다.
	1. 전공
	2. 산업 유형(업종)
	3. 업무를 수행하는데 요구되는 교육수준
	4. 청력 능력
	5. 시력 능력
	6. 글쓰기 능력
	7. 업무와 관련된 문서를 읽고 이해하는 능력
	8. 장비 유지 보수 능력
	9. 주말 및 공휴일 근무 여부
	10. 영어 회화, 독해 능력 여부
	11. 법률, 규정에 관한 지식
	12. 실외 근무 여부
	13. 소통 능력
	14. 기계와 도구를 사용하고 수리/유지하는 지식
	15. 판단과 의사결정 능력
	16. 집중력
	17. 기억력
	18. 시간 관리 능력
	19. 외부 고객 대응 여부
	20. 상대방의 말을 듣고 요점을 이해하는 
***

### 🔩 5-5. 직업 추천 모델 :
응답자의 특성에 적합한 직업을 한가지로 국한시키지 않고, 다양한 가능성을 보여주기 위해 최종모델에서 산출된 결과를 상위 3개, 5개, 10개 단위로 출력해보았다.

각각의 경우에서 산출된 결과에 실제 직업 라벨(정답 라벨)이 포함된 경우는 **상위 3개에 포함되어 있을 확률: 75%**, **상위 5개에 포함되어 있을 확률: 81%**, **상위 10개에 포함되어 있을 확률: 88%** 로 확인되었다.

<p align ="center">
	<img src = "https://user-images.githubusercontent.com/68809022/147474941-f4721bf8-f539-42a5-a06c-50e6c07f6af8.png" width = "100%" height="100%">
</p>						

추천된 다양한 직업을 보여주기 위해 상위 10개를 출력해주는 모델을 선택하여 추천시스템을 구현하였다.

## 6.  추천시스템
설문 조사 결과를 통하여 응시자의 성격, 능력, 역량에 적합한 **직업 상위 10개를 추천**해준 후,

해당 리스트에서 현직자가 업무 만족도, 직업 전망, 사회적 평판 등을 고려했을 때 **가장 좋은 Best3 직업**을 알려주는 서비스를 구현하였다.

***

### 📜 6-1. 데이터 수집

직접 제작한 설문지(123문항)는 아래의 카테고리에 해당하는 문제들로 구성되어 있다. [설문 조사 응시](https://docs.google.com/forms/d/1YA3iA2KJQQtdmrN7iGbOecF6bMXA4eYk75ls2teH5BA/edit?usp=drive_web)

	- "업무 환경"
	- "물리적 환경"
	- "업무 특성"
	- "업무에 대한 흥미"
	- "본인의 성격"
	- "지식 역량"
	- "업무 수행 능력"
	- "본인의 가치관"
	- "종합 질문(근무하고 싶은 업종, 학력, 직업 선택에 있어서 중요한 요소, 등)"
	


<p align="center">
	<img src = "https://user-images.githubusercontent.com/68809022/147476727-5f4ddb0c-9cd5-40e7-98fe-bbc28ebe06fc.png" width = "100%" height="100%">
</p>

***

### 📜 6-2. Radar Chart를 통한 시각화
추천된 상위 10개의 직업에서 현직자가 아래의 요소들을 고려했을때 가장 좋은 직업 Best3를 Radar Chart를 활용하여 표현하엿다.

	- 업무 만족도(satisfaction)
	- 직업 전망(prospects)
	- 사회적 평판(reputation)
	- 수입(income)
	- 직업의 안정성(stability)


</br>

왼쪽: 추천된 상위 10개의 직업, 오른쪽: 현직자가 뽑은 Best3

<p align = "center">
	<img src = "https://user-images.githubusercontent.com/68809022/147483604-e5ad200f-395e-4e87-8e21-a04242f1644b.png" width = "90%" height = "90%">
</p>

## 7. REVIEW
### 한계점
	- 주관식으로 답한 문항에서의 부족한 자연어 처리
	
	- 설문 답변들이 재직자 기반으로 조사한 결과이기 때문에, 구직자 입장에서의 답변과 완벽히 매칭되지 않는다는 한계

## Team
- 강승완
- 이유나
- 정하은

