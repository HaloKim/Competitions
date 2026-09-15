# [한국어 어문 규범 기반 생성 (RAG)](https://kli.korean.go.kr/benchmark/taskBoardsOrdtm/boardsOrdtm/noticeView.do?recordId=472&boardOrdtmId=)

# 순위

* 팀 은상

# 대회정보 

## 주제

한국어 어문 규범 관련 질문에 대해 국어 지식을 참조하여 외부 지식 없이 주어진 정보만으로 답변을 생성

## 설명

* 선택형: 두 선택지 중 올바른 선택지를 고르고, 그 이유를 생성
* 교정형: 주어진 문장에서 어문 규범에 부합하지 않는 부분을 수정하고, 수정한 이유를 생성

## 주최/주관

* 주최: 국립국어원

# 데이터

* 어문 규범 pdf를 파싱해 규범 제목 기준으로 분리, 규범 단위 json 문서로 전처리

* gold_context가 없어 정답의 근거 문장을 query로 bge-m3 + FAISS 검색해 pseudo labeling 수행

# Retriever

* DPR(dual encoder, in-batch / hard negative) + CLS 기반 Reranker 실험

* 특수 도메인 특성상 의미 기반 검색 성능이 저조하여, 질의 내 선택지({A/B})를 이용한 선택 추출(슬롯 기반) 검색 적용

* 검색 성공 시 규범을 증강한 augmentation prompt, 실패 시 base prompt 사용 (Lost in the Middle 고려해 질의 상단, 문서 하단 배치)

# Train

* HyperCLOVAX-SEED-Think-14B, deepspeed ZeRO-3 학습

* 앙상블 금지 환경에서 seed 앙상블 효과를 위한 Iterative Training (2 epoch -> 8 epoch -> 1 epoch)

* 어문 규범 교정 데이터셋으로 GPTQ 양자화

# 배운점

* 국내 8B 이상 LLM은 사전 지식이 풍부해 적은 데이터 fine-tuning으로도 충분한 생성 성능

* 특수 도메인에서 pseudo labeling 기반 검색기는 정확도가 낮아, 단순한 슬롯 기반 검색이 오히려 성능 향상
