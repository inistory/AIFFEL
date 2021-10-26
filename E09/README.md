# E09 Movielens 영화 추천

## 추천 시스템 (Recommender System)

- 나와 비슷한 다른 사용자들이 좋아하는 것과 비슷한 것을 내게 추천
- 사용자가 선호할 만한 아이템을 추측함으로써 여러 가지 항목 중 사용자에게 적합한 특정 항목을 선택 (information filtering)
### 1) 콘텐츠 기반 필터링 (Contents-based Filtering)
- 콘텐츠 기반 필터링은 항목 자체를 분석하여추천을 구현한다. 
- ex) 음악을 추천하기 위해 음악 자체를 분석하여 유사한 음악을 추천
- 군집분석(Clustering analysis), 인공신경망(Artificial neural network), tf-idf(term frequency-inverse document frequency
### 2) 협업 필터링 (Collaborative Filtering)
- 대규모의 기존 사용자 행동 정보를 분석하여 해당 사용자와 비슷한 성향의사용자들이 기존에 좋아했던 항목을 추천하는 기술
- ex) 이 상품을 구매한 사용자가 구매한 상품들
- 행렬분해(Matrix Factorization), k-최근접 이웃 알고리즘 (k-Nearest Neighbor algorithm;kNN)
- 단점
	-  콜드 스타트(Cold Start)
		- 시스템이 충분한 정보를 모으지 못한 사용자나 아이템에 대한 추론을 할 수 없는 상태
		- 음악 서비스의 경우, 신곡이 발표되면 이를 추천할 수 있는 정보가 쌓일 때까지 추천이 어려워지는 것
	- 계산량이 너무 많아 추천의 효율이 떨어지는 상황		
		- 사용자 수가 많은 경우 효율적으로 추천 불가 
		- 협업 필터링은 계산량이 비교적 많은 알고리즘 (행렬분해, 사용자 수가 커질수록 계산량 증가)
	- 롱테일(Long tail) 문제
		- 롱테일의 꼬리 부분
		- 사용자의 관심이 저조한 항목의 정보가 부족하여 추천에서 배제되는 상황

### 3) 모델 기반 협력 필터링(Model-based Collaborative Filtering algorithm)
- 기존 항목 간 유사성을 단순하게 비교하는 것에서 벗어나 자료 안에 내재한 패턴을 이용하는 기법
- LDA(Latent Dirichlet Allocation), 베이지안 네트워크(Bayesian Network)

### 4) 필터버블(filter bubble)
- 추천 시스템이 고도화될수록 사용자의 입맛에 맞는 정보만 제공되고 나머지 정보는 감추어지는 현상

### 5) Explicit vs Implicit Feedback Datasets
- Explicit Datasets : 유저가 자신의 선호도를 직접(Explicit) 표현
	- ratings
- Implicit Datasets : 유저가 간접적(Implicit)으로 선호, 취향을 나타내는 데이터  
	- 플레이 횟수, 플레이 시간
	- 클릭 수, 구매 여부, 플레이 스킵 여부, 검색 기록, 방문 페이지 이력, 구매 내역, 심지어 마우스 움직임 기록

### 6) Matrix Factorization (MF)
- MF 모델은 2006년 Netflix에서 백만달러의 상금을 걸고 개최한 자사 추천시스템의 성능을 10% 이상 향상시키는 챌린지를 계기로 알려지게 됨
- (m,n) 사이즈의 행렬 R을 (m,k) 사이즈의 행렬 P와 (k,n) 사이즈의 행렬 Q로 분해한다면 R은 P와 Q의 행렬곱으로 표현 가능
- 대체로 k는 m이나 n보다 훨씬 작은 값이기 때문에 계산량 측면으로도 훨씬 유리
- 협업 필터링은 평가행렬을 전제로 함
- m x n : 유저 x 상품


### 7) CSR(Compressed Sparse Row)
- 압축 희소행렬
- 0이 아닌 것을 누적해서 계산
- csr_mat.**indptr** : 행렬의 '0'이 아닌 원소의 행의 시작 위치
- csr_mat.**indices** : 행렬의 '0'이 아닌 원소의 열의 위치
- csr_mat.**data** : 행렬의 '0'이 아닌 원소 값

  
  

### References
- http://www.kocca.kr/insight/vol05/vol05_04.pdf
- https://orill.tistory.com/entry/Explicit-vs-Implicit-Feedback-Datasets?category=1066301
- https://rfriend.tistory.com/551

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjY0Njg1MTI1LC0xNzY4ODkxNDM4LC0xMT
k4NDAwOTkxLC04NjI5MTAyNTYsLTU2MjI0MDgyNywtMTQ1MzE4
MTk2Nyw5NDg2OTMzNjksLTY2Njg5MjY4Niw4MjkyMjUzOTEsLT
YyNzEwMTE2MywtMTUzMzAwMjcyMCw0Mjg2MTcyNSwtMTk0NjQx
NjY5NCwtNDIyNzYwOTUxLDExMDUzNzk4MCwxOTgzNDU5OTEyLD
IxMDE1NDgwOTQsLTU2MTMyMDk4MiwxOTc0NDMzNzIzLC01MzM5
MDE5NjFdfQ==
-->