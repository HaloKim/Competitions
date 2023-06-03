# [Kaggle Playground-S3E15](https://www.kaggle.com/competitions/playground-series-s3e15/overview)

# 순위

* 개인 11/693

# 대회정보 

## 목적

머신러닝을 이용한 임계 열유속 예측

## 주최/주관

* 주최 및 주관: Kaggle

# 데이터

![image](https://github.com/HaloKim/Competitions/assets/44603549/fddd51a7-04cc-4d07-ba69-ce8cdf440ed6)

# 시도

## EDA

1) Relationship between "author" and "geometry"

2) Relationship between D_e [mm] and D_h [mm]

## Preprocess
Apply discovered patterns

fillna('Unknown')

fillna Mode()

fillna Mean()

Label Encoding

# 모델

AutoML mljar 활용

# 배운점

결측값을 EDA를 통해 Feature간의 패턴을 찾아 적용하고, 평균값이나 최빈값을 통해 잘 채워 Train data로써 잘 채우는 방법
