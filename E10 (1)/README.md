# E10 뉴스기사 요약해보기

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
- 다음 time step의 셀에 hidden state, cell state가 함께 전달됨s
- 인코더가 전달하는 컨텍스트 벡터에 hidden state 와 cell state 가 모두 존재

## 3. Attention Mechanism
- seq2seq는 인코더의 마지막 time step의 hidden state를 컨텍스트 벡터로 사용 (**h5**​)
- Attention Mechanism은 인코더의 모든 step의 hidden state 정보가 컨텍스트 벡터에 전부 반영됨 (**0.2h_1h1​+0.3h_2h2​+0.1h_3h3​+0.15h_4h4​+0.25h_5h5​**)
	- hidden state가 반영되는 비중을 디코더가 현재 time step의 예측에 인코더의 각 step이 얼마나 영향을 미치는지에 따른 가중합으로 계산
	- 컨텍스트 벡터를 구성하기 위한 인코더 hidden state의 가중치 값은  디코더의 현재 스텝이 어디냐에 따라 계속 달라진다
	- 즉, 디코더의 현재 문장 생성 부위가 주어부인지 술어부인지 목적어인지 등에 따라 인코더가 입력 데이터를 해석한 컨텍스트 벡터가 다른 값을 가짐

	
	- 
- 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgxMjM2NzMxNiwxNjE5NDMzNjAyLDE0Nz
A1Mzc4MzEsLTE5NTUyMzkyMjYsLTE3OTU1NTE1ODcsLTc4OTg2
NzEwLDEyMjI2OTM3NCw3MzA5OTgxMTZdfQ==
-->