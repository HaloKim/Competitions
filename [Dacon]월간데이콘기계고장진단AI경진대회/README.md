# [월간 데이콘 기계 고장 진단 AI 경진대회](https://dacon.io/competitions/official/236036/overview/description)

# 순위

* 개인 19/582

# 대회정보 

## 주제

음향 데이터 기반 기계 고장 진단 AI 모델 개발

## 설명

정상의 데이터들로부터 비지도 학습을 통해 팬(FAN)의 고장 여부를 판단(Unsupervised Anomaly Detection)하세요.

## 주최/주관

* 데이콘

## 참가 자격

* 데이커라면 누구나 참가 가능

# 데이터

![image](https://user-images.githubusercontent.com/44603549/213172392-3e78fdce-3819-4ad7-aea9-8d3db1f5138d.png)

wav 10초 가량의 음성 파일

비지도 학습, Train은 모든 데이터가 0 인 정상 범주의 기계 음성이며, 모델을 통해 Test에만 들어있는 비정상 음성을 예측해야하는 비지도학습 대회

음성을 통해 비정상을 진단한다는 점이 흥미로웠음

# 성능 개선을 위한 시도

* melspectrogram 128 Feature 생성
* mfcc 128 Feature 생성
* KLDLoss 적용
* 5 Folds

# 적용한 모델

* AutoEncoder
* ConvAutoEncoder
* GAN
* Unet
* ResUnet
* ResUnet++(attention)

접근법은 비지도 학습 및 Pytorch 학습을 위해 신경망으로 접근(최종 모델 ResUnet)

1. 정상인 Train 데이터를 학습시켜서 128+128개의 Feature 값을 생성하는 모델을 개발
2. 추론 진행 후 COS Similarity를 활용하여 특정 임계값(>= 0.999)을 넘지 못하면 비정상 데이터로 판별

# 효과적이었던 접근

모델에 Residual을 적용한 이후로 성능이 폭발적으로 향상
