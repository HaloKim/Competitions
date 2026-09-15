# [제4회 2023 연구개발특구 AI SPARK 챌린지 - 공기압축기 이상 판단](https://aifactory.space/competition/detail/2226)

# 순위

* 팀 125/803

# 대회정보 

## 목적

산업용 공기압축기의 이상 유무를 비지도학습 방식을 이용하여 판정

## 주최/주관

* 주최 및 주관: 범천(주) / AIFactory

# 데이터

![image](https://github.com/HaloKim/Competitions/assets/44603549/29d907c8-3a6c-4e46-9868-6bc5540f5f89)

air_inflow: 공기 흡입 유량 (^3/min)

air_end_temp: 공기 말단 온도 (°C)

out_pressure: 토출 압력 (Mpa)

motor_current: 모터 전류 (A)

motor_rpm: 모터 회전수 (rpm)

motor_temp: 모터 온도 (°C)

motor_vibe: 모터 진동 (mm/s)

type: 설비 번호

2. 또한 설비별로 다음의 특성을 갖습니다.

설비 번호 [0, 4, 5, 6, 7]: 30HP(마력)

설비 번호 1: 20HP

설비 번호 2: 10HP

설비 번호 3: 50HP

# 시도

## Preprocess

PCA

TSNE

Scaler

설비 LabelEncoder

Add some Feature

# 모델

AutoEncoder 구조

pyod 라이브러리

# 배운점

Single-Label classification 

이상 데이터가 적은 상태에서 정상 데이터 만을 활용하여 비정상 장비를 찾아내는 방법
