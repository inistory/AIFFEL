

# E08 인물사진을 만들어 보자

## Cv2
- 좌표가 왼쪽 상단부터 시작
- x, y 좌표가 반대
- HWC(Height, Width, Channel)


## 이미지 세그멘테이션(image segmentation)
- 이미지에서 픽셀 단위로 관심 객체를 추출하는 방법
- 하나의 이미지에서 배경과 사람 분리 가능
- 분리 된 배경을 블러처리하고 다시 사람이미지와 합치면 아웃포커싱 효과
- 이미지 세그멘테이션은 모든 픽셀에 라벨(label)을 할당하고 같은 라벨은 "공통적인 특징"을 가진다고 가정

### 1) 시멘틱 세그멘테이션(semantic segmentation)이란?
- 우리가 인식하는 세계처럼 물리적 의미 단위로 인식하는 세그멘테이션
- 이미지에서 픽셀을 사람, 자동차, 비행기 등의 물리적 단위로 분류(classification)하는 방법

![content img](https://d3s0tskafalll9.cloudfront.net/media/images/E-14-5.max-800x600_YNvIU7P.png)


### 2) 인스턴스 세그멘테이션(Instance segmentation)이란?
- 시멘틱 세그멘테이션은 '사람'이라는 추상적인 정보를 이미지에서 추출해내는 방법 : 사람이 누구인지 관계없이 같은 라벨로 표현
- 인스턴스 세그멘테이션은 사람 개개인별로 다른 라벨 가짐: 사람 개개인별로 다른 라벨로 표현

### 3) DeepLab 알고리즘(DeepLab v3+)
- 세그멘테이션 모델 중에서도 성능이 매우 좋아 최근까지도 많이 사용
- https://blog.lunit.io/2018/07/02/deeplab-v3-encoder-decoder-with-atrous-separable-convolution-for-semantic-image-segmentation/
- receptive field를 넓게 사용하기 위해 atrous convolution을 사용
- Depthwise separable convolution은 Xception 에서 처음 제안, 3x3 conv layer 의 receptive field를 1/9 수준의 파라미터로 구현할 수 있기 때문에 효율적
	-[DeepLab Demo](https://arxiv.org/abs/1610.02357)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYyNDU2MzEzMywzNDE4NDQwMjQsLTMxMT
Q5NzYzOSwxMjQ2MTMyMDU4LC0xNjA3MzU5NjY0LDE0ODU5OTA4
NzYsNzMwOTk4MTE2XX0=
-->