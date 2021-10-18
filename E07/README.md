


> Written with [StackEdit](https://stackedit.io/).
# E07 영화리뷰 텍스트 감성분석하기

### 임베딩이란?
- 임베딩(embedding) : 자연어를 숫자의 나열인 벡터로 바꾼 결과 혹은 그 일련의 과정 전체
- 말뭉치(corpus)의 의미, 문법 정보가 응축되어 있음
- 최근 전이학습 때문에 임베딩이 중요해짐


### 전이학습이란?
- 특정 문제를 풀기 위해 학습한 모델을 다른 문제를 푸는 데 재사용하는 기법
	- 예시 : 대규모 말뭉치를 미리 학습(pretrain)한 임베딩을 문서 분류 모델의 입력값으로 쓰고, 해당 임베딩을 포함한 모델 전체를 문서 분류 과제를 잘할 수 있도록 업데이트(fine-tuning)하는 방식
- 즉, 모델이 학습시 제로 베이스에서 시작하지 않는 것을 의미 
	- 임베딩의 품질이 좋을수록 태스크의 성능이 더 좋다!


### 1) 데이터셋 준비
- 네이버 영화리뷰 데이터
https://github.com/e9t/nsmc


### 2) 데이터로더 구성



### 3) 모델구성을 위한 데이터 분석 및 가공


### 4) 모델구성 및 validation set 구성

### 5) 모델 훈련 개시


### 6) Loss, Accuracy 그래프 시각화


### 7) 학습된 Embedding 레이어 분석


### 8) 한국어 Word2Vec 임베딩 활용하여 성능개선
- https://github.com/Kyubyong/wordvectors

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg2MDcyNTQ2Myw1MzkyOTIxNTcsMTE2OT
I2MDE3NCwyNDc4NDk0NTcsNzk4NjgxNTY1LDczMDk5ODExNl19

-->