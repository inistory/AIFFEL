# E10 뉴스기사 요약해보기

## 텍스트 요약이란?
1) 추출적 요약 (Extractive Summarization)
- 단어 그대로 원문에서 **문장들을 추출**해서 요약하는 방식
2) 추상적 요약 (Abstractive Summarization)
- 원문으로부터 내용이 요약된 **새로운 문장을 생성**해내는 방식



## 1. seq2seq
![content img](https://d3s0tskafalll9.cloudfront.net/media/images/E-21-2.max-800x600.png)
- seq2seq은 두 개의 RNN 아키텍처를 사용하여 입력 시퀀스로부터 출력 시퀀스를 생성해내는 자연어 생성 모델
	1) 원문을 첫 번째 RNN인 인코더로 입력
	2) 인코더는 이를 하나의 고정된 벡터로 변환
	(문맥정보를 가지고 있는 벡터, context vector)
	3) 두 번째 RNN인 디코더s는 컨텍스트 벡터를 전달받아 한 단어씩 다음 등장할 단어를 예측해서 요약 문장을 완성
- 디코더는 시작 토큰 SOS가 입력되면, 각 시점마다 단어를 생성하고 종료 토큰 EOS를 예측하는 순간에 멈춤
- 즉, 훈련 데이터의 예측 대상 시퀀스 앞과 뒤에 시작 토큰과 종료 토큰을 넣어주는 전처리를 하여 멈춰야할 곳을 알려줘야함

## 2. LSTM
- 다음 time step의 셀에 hidden state, cell state가 함께 전달됨
- 인코더가 전달하는 컨텍스트 벡터에 hidden state 와 cell state 가 모두 존재

## 3. Attention Mechanism
- seq2seq는 인코더의 마지막 time step의 hidden state를 컨텍스트 벡터로 사용 (**h5**​)
- Attention Mechanism은 인코더의 모든 step의 hidden state 정보가 컨텍스트 벡터에 전부 반영됨 (**0.2h_1h1​+0.3h_2h2​+0.1h_3h3​+0.15h_4h4​+0.25h_5h5​**)
	- hidden state가 반영되는 비중을 디코더가 현재 time step의 예측에 인코더의 각 step이 얼마나 영향을 미치는지에 따른 가중합으로 계산
	- 컨텍스트 벡터를 구성하기 위한 인코더 hidden state의 가중치 값은  디코더의 현재 스텝이 어디냐에 따라 계속 달라짐
	- 즉, 디코더의 현재 문장 생성 부위가 주어부인지 술어부인지 목적어인지 등에 따라 인코더가 입력 데이터를 해석한 컨텍스트 벡터가 다른 값을 가짐

## 4. 요약
1.  seq2seq를 사용
2.  RNN 계열 중 LSTM을 사용하므로 hidden state뿐만 아니라 cell state도 사용해야 함
3.  디코더의 예측 시퀀스에는 시작 토큰 SOS와 예측 토큰 EOS를 시퀀스의 앞, 뒤로 붙임
4.  seq2seq를 구동시키면 디코더는 시작 토큰을 입력받아 예측을 시작
5.  seq2seq 기본 모델과 달리, 어텐션 메커니즘을 이용해 인코더의 hidden state의 중요도를 취합한 컨텍스트 벡터를 디코더 스텝별로 계산
6.  계산된 컨텍스트 벡터를 이용해서 디코더는 다음 등장할 단어를 예측


	
	- 
- 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcxNjg5NDk1NiwxNDQ5NDgxNTAwLDc4MD
g5NTY0NiwtOTc2MDM0MjkxLDE4MTIzNjczMTYsMTYxOTQzMzYw
MiwxNDcwNTM3ODMxLC0xOTU1MjM5MjI2LC0xNzk1NTUxNTg3LC
03ODk4NjcxMCwxMjIyNjkzNzQsNzMwOTk4MTE2XX0=
-->