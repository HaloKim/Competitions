# [Fake or Real: AI 생성 이미지 판별 경진대회](https://aiconnect.kr/competition/detail/227/task/295/taskInfo)

# 순위

* 개인 	19/707

# 대회정보 

## 목적

영상 위변조 방지를 위한 가짜 이미지 판별 솔루션

생성 AI가 만들어낸 가짜 (Fake) 이미지와 진짜 (Real) 이미지를 분류하는 문제

## 주최/주관

* 주최 및 주관: AIConnect

## 참가 자격

제한 없음

# 데이터

실제 이미지(0), 생성형 모델로 생성된 이미지(1)

# 시도

이미지 사전 학습 모델 활용 vit_base_patch32_384

# 모델

* Backbone VIT
* Muti Sample Dropout layer 추가 (4)
* BCELoss 사

# 배운점

사전 학습 모델 timm의 강력함.
