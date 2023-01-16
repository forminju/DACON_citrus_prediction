# 감귤 착과량 예측 AI 경진대회
![대회소개이미지](https://user-images.githubusercontent.com/92534659/209781272-c4640520-62ce-4965-b9f1-d68d69bea9bc.png)

## 대회 개요
- 주최: 제주 테크노파크
- 주관: [데이콘](https://dacon.io/competitions/official/236038/overview/description)
- 기간: 2022.12.12 ~ 2022.12.14
- 주제: 감귤 착과량 예측 AI 모델 개발

## 목표
감귤나무의 나무 생육 상태, 엽록소 및 새순 정보로부터 감귤 착과량을 회귀 예측

## 결과
- **최종 7위 / 257팀 (상위 3%, 동상)** 
- Public Score 0.07287 | Private Score 0.07286

## DataSet
[출처](https://dacon.io/competitions/official/236038/data)

Input
- ID : 과수나무 고유 ID
- 나무 생육 상태 Features (4개): 수고(m), 수관폭1(min), 수관폭2(max), 수관폭평균(수관폭1과 수관폭2의 평균)
  - 데이터 기입은 cm 단위
- 새순 Features (89개): 2022년 09월 01일 ~ 2022년 11월 28일에 일별 측정된 새순 데이터
- 엽록소 Features (89개): 2022년 09월 01일 ~ 2022년 11월 28일에 일별 측정된 엽록소 데이터

Target
- 착과량(int) : 실제 감귤 착과량 (Target)

Train / Test set
- Train set: 총 2207개 과수나무 케이스 (TRAIN_0000 ~ TRAIN_2206.csv)
- Test set: 총 2208개 과수나무 케이스 (TEST_0000 ~ TEST_2207.csv)

## Model
- `XGBoostRegressor`, `RandomForestRegressor`

## Feature Engineering
엽록소 Feature 삭제 및 파생변수 생성

| 파생변수 종류 | 설명 |
| :----------- | :------------ |
| 9일간 새순 평균 | 새순의 변화가 급격하지 않기 때문에 9일간 평균을 계산함 |
| 새순 최댓값, 최솟값, 범위 | 시간이 지나면서 새순 변수가 점차 감소함을 반영하기 위해 최댓값, 최솟값, 범위를 계산함 |
| 나무 부피 | 수고와 수관폭평균을 곱함 |

## Insight
- EDA 결과 target 값과 큰 연관성이 없는 엽록소 컬럼을 모두 drop한 것이 유의미한 결과를 만든 것으로 보입니다
- 자세한 내용은 [PPT 자료](https://github.com/forminju/DACON_citrus_prediction/blob/main/%EC%B5%9C%EC%A2%85%EB%B3%B8_%ED%91%9C%EC%A7%80%EC%88%98%EC%A0%95.pdf)에서 확인할 수 있습니다

## Team Members
- [노지예](https://github.com/kkumtori), [전민주](https://github.com/forminju), [조성우](https://github.com/jswooo), [임홍주](https://github.com/hihongju)

## Reference
- 제주특별자치도 농업기술원 ebook https://agri.jeju.go.kr/ebook/technology.htm?page=1
- 감귤박물관 https://culture.seogwipo.go.kr/citrus/story/dictionary/cultivation.htm
