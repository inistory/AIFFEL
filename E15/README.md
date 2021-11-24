
# 한국어 데이터로 챗봇 만들기

## 인코더와 디코더 구조
![content img](https://d3s0tskafalll9.cloudfront.net/media/images/Untitled_UcFQAjh.max-800x600.png)

- 인코더 : 입력을 넣는 곳
- 디코더 : 결과를 출력하는 곳
- 훈련데이터셋 예시
	- 번역
		- 입력문장: 저는 학생입니다.
		- 출력문장: I am a student
	- 질문과 답변
		- 입력문장: 오늘의 날씨는 어때?
		- 출력문장: 오늘은 매우 화창한 날씨야
	
## 트랜스포머
- 자연어처리모델(ex RNN) 들은 텍스트 문장을 입력으로 받기 위해 단어를 입베딩벡터로 변환 (벡터화)
- 트랜스포머 모델의 입력데이터 처리에서 RNN과의 차이점? 
	- Positional Encoding
![content img](https://d3s0tskafalll9.cloudfront.net/media/original_images/Untitled_4_fuzN6PD.png)

![content img](https://d3s0tskafalll9.cloudfront.net/media/original_images/Untitled_5_kH52kQN.png)

- Positional Encoding이란?
	- 임베딩벡터 +  어떤 값 => 입력으로 사용
- 트랜스포머만 특별히 positional encoding을 해주는 이유는?
	- 트랜스포머는 입력을 받을 때, 문장에 있는 단어들을 1개씩 순차적으로 받지 X
	- 문장에 있는 모든 단어를 한꺼번에 입력받음 O
	- 어순정보 필요
	- 단어의 임베딩벡터  + 단어의 위치정보를 가진 벡터 (positional encoding)
	- 수식
			![content img](https://d3s0tskafalll9.cloudfront.net/media/original_images/Untitled_6_DyxB6Ax.png)

- 수식 해석	
	- dmodel​ : 임베딩 벡터의 차원
	- pos : 입력 문장에서의 임베딩 벡터의 위치
	- i : 임베딩 벡터 내의 차원의 인덱스 
![content img](https://d3s0tskafalll9.cloudfront.net/media/original_images/Untitled_7_3Rneu0P.png)

	- 임베딩 행렬과 포지셔널 행렬이라는 두 행렬을 더함으로써 각 단어 벡터에 위치 정보를 더해주게 되는 것

## 셀프 어텐션 (Self Attention)
 - 유사도를 구하는 대상이 다른 문장의 단어가 아니라 현재 문장 내의 단어들이 서로 유사도를 구하는 경우
![content img](https://d3s0tskafalll9.cloudfront.net/media/original_images/Untitled_13_hjMyZwL.png)
 - 동물(animal)과 그것(it)이 연관되어 있을 확률이 높다는 것을 self attention을 통해 구하는 것

 - 종류?
![content img](https://d3s0tskafalll9.cloudfront.net/media/original_images/Untitled_11_tFFhFjx.png)
	-   **인코더 셀프 어텐션**  : 인코더의 입력으로 들어간 문장 내 단어들이 서로 유사도를 구한다. 
	-   **디코더 셀프 어텐션**  : 단어를 1개씩 생성하는 디코더가 이미 생성된 앞 단어들과의 유사도를 구한다.
	-   **인코더-디코더 어텐션**  : 디코더가 잘 예측하기 위해서 인코더에 입력된 단어들과 유사도를 구한다.

 - 트랜스포머에서 셀프어텐션 위치
![content img](https://d3s0tskafalll9.cloudfront.net/media/original_images/Untitled_12_SIe2V15.png)

	 -  **인코더 셀프 어텐션**은 인코더에서 
	-  **디코더 셀프 어텐션**은 디코더에서 
	 -  **인코더-디코더 어텐션**  은 디코더에서 이루어짐

## 스케일드 닷 프로덕트 어텐션
- 트랜스포머에서 어텐션 값을 구하는 방법?
	- Q, K, V는 각각 쿼리(Query), 키(Key), 값(Value)
	1.  어텐션 함수는 주어진 '쿼리(Query)'에 대해서 모든 '키(Key)'와의 **유사도**를 각각 구하기
	2.  그리고 구해낸 이 유사도를 키와 맵핑되어있는 각각의 '값(Value)'에 반영 
	3.  그리고 유사도가 반영된 '값(Value)'을 모두 더하면 **어텐션 값(Attention Value)** 

- 수식을 그림으로
	1.  **Q, K, V**는 단어 벡터를 행으로 하는 문장 행렬이다.
	2.  벡터의  **내적(dot product)**  은 벡터의  **유사도**를 의미한다.
	3.  특정 값을 분모로 사용하는 것은 값의 크기를 조절하는 스케일링(Scaling)을 위함이다.

![content img](https://d3s0tskafalll9.cloudfront.net/media/original_images/Untitled_15_pUfIgKn.png)

- 문장 행렬 Q와 문장 행렬 K를 곱하면 각 단어 벡터의 유사도가 모두 기록된 유사도 행렬을 얻음


![content img](https://d3s0tskafalll9.cloudfront.net/media/original_images/Untitled_16_neA52rZ.png)
1. 이 유사도 값을 스케일링 해주기 위해서 행렬 전체를 특정 값으로 나눠주고, 
2. 유사도를 0과 1사이의 값으로 Normalize해주기 위해서 소프트맥스 함수를 사용
	-  	여기까지가 Q와 K의 유사도를 구하는 과정
3. 여기에 문장 행렬 V와 곱하면 **어텐션 값(Attention Value)** 을 얻음

- 결론 : 내적(dot product)을 통해 단어 벡터 간 유사도를 구한 후, 특정 값을 분모로 나눠주는 방식으로 QQ와 KK의 유사도를 구함 
	=>  **스케일드 닷 프로덕트 어텐션(Scaled Dot Product Attention)**
	=> 특정값을 나눠주는 부분이 없다면? **닷 프로덕트 어텐션(dot product attention)**



## 병렬로 어텐션 수행하기
- 트랜스포머 num_heads 변수
	- 병렬적으로 몇 개의 어텐션 연산을 수행할지를 결정하는 하이퍼파라미터
	![content img](https://d3s0tskafalll9.cloudfront.net/media/original_images/Untitled_18_nnOTx9p.png)
	1. 트랜스포머의 초기 입력인 문장 행렬의 크기는
		-  문장의 길이를 행으로
		-  `d_model`을 열로 가짐
	2.  트랜스포머는 이렇게 입력된 문장 행렬을  `num_heads`의 수만큼 쪼개서 어텐션을 수행
	3. 이렇게 얻은  `num_heads`의 개수만큼의 어텐션 값 행렬을 다시 하나로 concatenate
	
		=> 위의 그림은 `num_heads`가 8개인 경우인데, 다시 concatenate하면서 열의 크기가 `d_model`이 됨

- 병렬로 어텐션을 수행(**멀티 헤드 어텐션**)할 때의 장점?
	- 각각 다른 관점에서 어텐션을 수행하므로 한 번의 어텐션만 수행했다면 놓칠 수도 있던 정보를 캐치할 수 있음


## 마스킹
- 특정 값들을 가려서 실제 연산에 방해가 되지 않도록 하는 기법
1. 패딩 마스킹(Padding Masking)
	- 패딩 토큰(Padding token)을 이용한 방법
	- 패딩?
		- 문장의 길이가 서로 다를 때, 모든 문장의 길이를 동일하게 해주는 과정에서 정해준 길이보다 짧은 문장의 경우에는 숫자 0을 채워서 문장의 길이를 맞춰주는 자연어 처리 전처리 방법
	- 이렇게 주어진 숫자 0은 실제 의미가 있는 단어가 아니므로 실제 어텐션 등과 같은 연산에서는 제외할 필요가 있음 
	=>  **패딩 마스킹**은 이를 위해 숫자 0인 위치를 체크
2. 룩 어헤드 마스킹(Look-ahead masking, 다음 단어 가리기)
	- RNN은 **step**이라는 개념이 존재해서 각 **step**마다 단어가 순서대로 입력으로 들어가는 구조
	- 반면 트랜스포머의 경우, 문장 행렬을 만들어 한 번에 행렬 형태로 입력으로 들어간다는 특징 존재
	- 즉, 이전 단어들만으로 다음 단어를 예측하는 훈련을 시키기 위해 자신보다 다음에 나올 단어를 참고하지 않도록 가리는 **마스킹(Masking)** 기법!


## 인코더
![content img](https://d3s0tskafalll9.cloudfront.net/media/images/Untitled_21_Y7Cy8sm.max-800x600.png)

- 하나의 인코더 층은 크게 총 2개의 서브 층(sublayer)으로 나누어짐
- **셀프 어텐션**과 **피드 포워드 신경망**
- 셀프 어텐션은 **멀티 헤드 어텐션**으로 병렬적으로 이루어짐

![content img](https://d3s0tskafalll9.cloudfront.net/media/images/Untitled_22_teJgoCi.max-800x600.png)

- 이렇게 구현한 인코더 층을 **임베딩 층(Embedding layer)** 과 **포지셔널 인코딩(Positional Encoding)** 을 연결하고, 사용자가 원하는 만큼 인코더 층을 쌓음으로써 트랜스포머의 인코더가 완성
- 디코더 내부에서는 각 서브 층 이후에 훈련을 돕는 **Layer Normalization**이라는 테크닉이 사용되었습니다. 위 그림에서는 **Normalize**라고 표시된 부분에 해당

## 디코더
- 인코더는 두 개의 서브 층으로 구성되지만, 디코더는 세 개의 서브 층으로 구성됨
![content img](https://d3s0tskafalll9.cloudfront.net/media/images/Untitled_23_vBHZ3i0.max-800x600.png)

- 첫 번째는 **셀프 어텐션**, 두 번째는 **인코더-디코더 어텐션**, 세 번째는 **피드 포워드 신경망**
- **인코더-디코더 어텐션**은 셀프 어텐션과는 달리, Query가 디코더의 벡터인 반면에 Key와 Value가 인코더의 벡터라는 특징, 이 부분이 인코더가 입력 문장으로부터 정보를 디코더에 전달하는 과정
- 인코더의 **셀프 어텐션**과 마찬가지로 디코더의 **셀프 어텐션**, **인코더-디코더 어텐션** 두 개의 어텐션 모두 **스케일드 닷 프로덕트 어텐션**을 **멀티 헤드 어텐션**으로 병렬적으로 수행
- 이렇게 구현한 디코더의 층은 **임베딩 층(Embedding layer)** 과 **포지셔널 인코딩(Positional Encoding)** 을 연결하고, 사용자가 원하는 만큼 디코더 층을 쌓아 트랜스포머의 디코더가 완성


## References
- 데이터
https://github.com/songys/Chatbot_data/blob/master/ChatbotData.csv