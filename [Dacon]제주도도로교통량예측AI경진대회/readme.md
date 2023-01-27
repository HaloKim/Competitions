# [제주도 도로 교통량 예측 AI 경진대회](https://dacon.io/competitions/official/235985/overview/description)

# 순위

* 팀 27/1559

# 대회정보 

## 주제

제주도 도로 교통량 예측 AI 알고리즘 개발

## 설명

제주도의 교통 정보로부터 도로 교통량 회귀 예측

## 주최/주관

* 주최: 제주 테크노파크, 제주특별자치도
* 주관: 데이콘

## 참가 자격

* 일반인, 학생 등 누구나

# 데이터

![image](https://user-images.githubusercontent.com/44603549/213167342-983c0bbe-2801-49aa-9c2f-226a1cd74eb8.png)

# 성능 개선을 위한 시도

* 기존 Feature 활용 파생 변수 생성
* 날씨 변수 추가(데이터기준 작년 동일날짜 10일간의 평균 날씨)
* 좌표 변수 추가(기준 좌표 주변 1Km이내의 버스 정류장 갯수, 어린이보호구역)
* Scailing
* Delete Outlier(IQR)
* 왜도/첨도 수정
* 휘발유/경유 가격 추가
* 제주도 확진자 수
* 시간 주기성 컬럼 생성 COS, SIN
* Target 관련 통계 변수 생성
* Permutaion Importance
* 앙상블
* 5 Folds
* Hyperparameter Tune(Optuna)

# 성능 개선 했던 Feature Engineering

* 기존 Feature 활용 파생 변수 생성
* 날씨 변수 추가(데이터기준 작년 동일날짜 10일간의 평균 날씨)
* 좌표 변수 추가(기준 좌표 주변 1Km이내의 버스 정류장 갯수)
* 시간 주기성 컬럼 생성 COS, SIN
* Permutaion Importance
* 앙상블
* 5 Folds
* Hyperparameter tunuing

날씨 변수 추가로 초반에는 큰 성능 개선을 보였지만 추후 다양한 파생 변수들이 생성되며 다중공선성 문제로 인해 큰 효과를 내지 못해 제거

![image](https://user-images.githubusercontent.com/44603549/213169498-75fb9329-2c41-4d03-b7e2-673e787e1da6.png)

해결을 위해 VIF를 활용했지만 기각

개인적으로 획기적이었던 시간 주기성 컬럼 생성

![image](https://user-images.githubusercontent.com/44603549/213170373-636a23b6-5ce9-4329-be05-80a05a6a563f.png)

```python
def add_column_cyclical_features(df, col, period, start_num):
    values = 2 * np.pi * (df[col]-start_num) / period
    kwargs = {f'sin_{col}': lambda x: np.sin(values),
              f'cos_{col}': lambda x: np.cos(values)}
    return df.assign(**kwargs)
```

# 사용한 모델

* XGB
* CatBoost
* LGBM
* tabnet

최종사용 XGB, Cat, LGBM 평균값으로 적용

