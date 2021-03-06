# Parking_Demand_Prediction_AI [20210701 ~ 20210720]
## 문제
주어진 columns과 외부 데이터를 이용하여 등록차량수를 예측하는 주차수요 예측 문제이다. 회귀 분석을 이용하였다.

## 주어진 DATA
1. train.csv <br>
column : 단지코드, 총세대수, 임대건물구분, 지역, 공급유형, 전용면적, 전용면적별세대수, 공가수, 신분, 임대료보증금, 임대료, 도보 1-분거리 내 지하철역 수(환승노선 수 반영), 도보 10분거리 내 버스정류장 수, 단지내주차면수, 등록차량수
2. test.csv<br>
column : train.csv랑 동일, 등록차량수 예측
3. age_gender_info.csv : 지역 임대주택 나이별, 성별 인구 분포<br>
4. sample_submission.csv : 제출 양식<br>



## 1) First(1주차) : 데이터 전처리 과정
- columns명 변경<br>
도보 10분거리 내 지하철역 수(환승노선 수 반영) -> 지하철<br>
도보 10분거리 내 버스정류장 수 -> 버스<br>

- 임대보증금, 임대료에 있는 문자열 변경<br>
: 임대보증금, 임대료에 - 문자열 0으로 변경<br>

- 전용면적 평수로 변환<br>
전용면적*0.3025<br>

- float형 -> int형 변환<br>
단지 내 주차면수, 등록 차량수, 공가수, 전용면적열에 적용<br>

- 버스열 null 처리<br>
: 양산으로 추정되어 버스 2개, 지하철 0개로 채워줌<br>
- 지하철 null 처리<br>
: 광역시끼리 지하철 역 평균 0.xx로 나와서 전부 0으로 채워줌<br>

## 2) Second(2주차) : 데이터 전처리 과정
- train 데이터의 지역별 빈간 결측치 확인 및 결측치 제외 평균 살펴보기<br>
- 대전광역시 임대보증금, 임대료 결측치<br>
: 행 평균으로 채워주기<br>
- 상가임대료 결측치<br>
: 제주,경남,대전,강원,충청,부산에 대하여 임대료 평균으로 채워주기<br>
- 남은 임대보증금 결측치<br>
: 임대건물구분이 상가일때 전부 결측치가 생겨 0으로 채워주기로 함<br>
- 데이콘에서 주어진 데이터 오류 수정<br>

## 3) Third(3주차) : 데이터 전처리 & 회귀 분석 모델링
- 데이터 처리<br>
: 총세대수, 전용면적, 전용면적별세대수, 공가수, 지하철, 버스, 단지내주차면수, 등록차량수에 대해 standardscaler() 해줌<br>
: 단지코드,임대건물구분,지역,공급유형,자격유형에 대해 get_dummies() 해줌 <br>
columns 수가 464개가 되었다.<br>

- Ridge regression <br>
첫 제출 mae : 491.85<br>
높은 제출 mae : 169.95[code](https://github.com/jihyeheo/Parking_Demand_Prediction_AI/blob/main/3rd_Week/Dataprocessingfinal_ridge.ipynb)<br>

## TRY 모델<br>
OLS, Ridge regression, xgb, lgb<br>


## 결과
![image](https://user-images.githubusercontent.com/64202709/137959025-5be7a7f4-aecf-4fc7-bf6c-0d982f5c4426.png)
~~~~
model : LGMRegressor
가장 높은 mae : 111.448
~~~~~


## 내가 생각한 문제점
1) 데이터 파악을 잘 못해 결과가 이상하게 나옴<br>
2) 선형,비선형을 먼저 파악하고 모델링을 해야할 것 같음<br>
3) 데이콘이 끝난 후 분석을 해보지 않음<br>
4) 데이콘 베스트 분석을 분석해보자!<br>


## Study
1) [Code_1](https://github.com/jihyeheo/Parking_Demand_Prediction_AI/blob/main/Study/Code_1.ipynb)<br>
   : Private 1위 장어님 코드 공부 [[Link]](https://dacon.io/competitions/official/235745/codeshare/3015?page=1&dtype=recent)


## Reference
```
[1] 데이콘_주차수요 예측 ai 경진대회 : https://dacon.io/competitions/official/235745/mysubmission
```
