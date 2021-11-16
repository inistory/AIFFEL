
# E13 CIFAR-10 이미지 생성하기
-   **판별 모델**  : 입력된 데이터셋을 특정 기준에 따라 분류하거나, 특정 값을 맞추는 모델
-   **생성 모델**  : 학습한 데이터셋과 비슷하면서도 기존에는 없던 새로운 데이터셋을 생성하는 모델로 정리할 수 있습니다.

## Pix2Pix
- Pix2Pix는 간단한 이미지를 입력할 경우 실제 사진처럼 보이도록 바꿔줄 때 많이 사용되는 모델
- **이미지(Input Image)** 와 **실제 이미지(Ground Truth)** 가 쌍을 이루는 데이터셋으로 학습을 진행
- Input Image를 입력받으면, 내부 연산을 통해 실제 사진 같은 형상으로 변환된 Predicted Image를 출력
- 계속해서 Ground Truth와 얼마나 비슷한지를 평가하며 점차 실제 같은 결과물을 만들어 내게 됩니다.
- 한 이미지를 다른 이미지로 픽셀 단위로 변환한다는 뜻
![content img](https://d3s0tskafalll9.cloudfront.net/media/images/pix2pix.max-800x600.png)

##  CycleGAN
- Pix2Pix 이후 발전된 모델
- 그림을 사진으로 바꾸는 Pix2Pix와 비슷해 보이지만, 한 방향으로의 변환만 가능한 Pix2Pix와 달리 CycleGAN은 양방향으로의 이미지 변환이 가능
- 실사 이미지를 그림으로 바꾸는 것과 그림을 실사 이미지로 바꾸는 것 두 가지가 모두 가능한 것
![content img](https://d3s0tskafalll9.cloudfront.net/media/images/CycleGAN2.max-800x600.jpg)

## Neural Style Transfer
- 전체 이미지의 구성을 유지하고 싶은 Base Image와 입히고 싶은 스타일이 담긴 Style Image 두 장을 활용해 새로운 이미지를 만들어 내는 것
![content img](https://d3s0tskafalll9.cloudfront.net/media/images/StyleTransfer.max-800x600.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA0MTQ3MTQ0LC05MzY2MzE4MTYsLTE5OD
YzNTI0NiwxOTY5MDkyNDMxLDE3MzA4MTk0NjUsNzMwOTk4MTE2
XX0=
-->