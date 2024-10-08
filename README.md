# 프로젝트 요약
- 배경 : 안구질환의 예방, 조기 진단, 육안 판단을 보조할 수 있는 수단 연구의 필요성 대두
- 목적 : Vision Transformer 모델을 활용해 반려동물의 안구질환 이미지를 분류
- 결과 : 사전 학습된 ViT 모델을 로드하여 전이학습을 통해 반려묘의 안검염과 결막염, 반려견의 궤양성 각막질환과 백내장의 각각 4개 질환에 대한 분류 모델을 학습, 검증하여 평균 91.35%의 테스트 정확도를 도출
- 개발환경 : Google Colab, Python pytorch

# 프로세스
- **문제 정의**
  - 반려동물의 건강관리 방안 모색의 일환으로, 대표적인 반려동물인 반려묘와 반려견의 안구질환 이미지를 Attention Mechanism 기반의 Vision Transformer(ViT) 모델로 분류
  - 반려묘의 안검염과 결막염, 반려견의 궤양성 각막질환과 백내장의 각각 4개 질환에 대한 분류 모델을 학습, 검증
- **데이터 수집 및 전처리**
  - AI-Hub의 반려동물 안구질환 데이터를 활용. 일반카메라로 촬영한 반려묘 질환 2종과 반려견 질환 2종, 안구질환 총 4종을 임의로 선정하였고, 해당 이미지 데이터 57,328장을 사용
  - 반려묘의 데이터가 반려견에 비해 상대적으로 부족하여 데이터 증강(Augmentation) 기법 적용하여 이미지에 다양한 무작위 변형을 적용하였다.
  - Vision Transformer 모델에 맞게 입력 이미지 리사이징
- **데이터 모델링**
  - ViT-Base 모델 적용하여 전이학습 진행
  ![그림3-5](https://github.com/user-attachments/assets/7c8380af-0001-4be9-b089-4223bd70852f)  
    - 드롭아웃 기법으로 과대적합 방지
    - 하이퍼파라미터 최적화를 자동화하는 소프트웨어 프레임워크인 Optuna를 활용하여 파라미터를 최적화
  

  - 모델 학습 과정에서 각 안구질환 이미지 샘플을 Attention Heat Map으로 시각화
    - 모델의 예측과정에 대한 사용자의 해석 가능성을 높이고 모델의 결과를 더 신뢰할 수 있도록 도움
![그림4-5](https://github.com/user-attachments/assets/75a641cc-b9c8-425b-9b17-6bb9f00d3b1c)  

- **결과**
  - 분류 정확도 : 각 모델 성능 편차가 적고, 반려견의 백내장 분류 모델에서 비교적 우수한 성능을 달성
  ![12345](https://github.com/user-attachments/assets/f415cbfc-8f9a-4bf9-9df1-e137ab895c5c)
  - 혼동행렬(Confusion Matrix) 보고서 및 각 질환별 히트맵(Heatmap)
  ![66](https://github.com/user-attachments/assets/390e192f-cc32-4273-baba-fbff373916e7)
    - 클래스별 눈에 띄는 편차는 보이지 않음
    - 네 질환 모두 증상 “무(0)” 클래스를 잘 분류
    - 반려견의 궤양성각막질환은 증상 “하(1)”를 “무(0)”로 분류한 케이스가 약 13% 존재
    - 각 클래스별로 높은 성능을 보이며 모델이 질환의 여러 중증도를 고르게 잘 분류함을 보여줌
  
- **결론**
  - 각 모델 실험의 성능 평가 결과, 평균 91.35%의 테스트 정확도를 도출하였다. 이는 각 질환별로 편차가 크지 않은 고른 성과를 나타낸다.
  - 반려견의 궤양성각막질환 분류에서 ViT와 전통적인 합성곱 신경망 계열 모델과의 비교 분석을 통해, ViT-Base 모델이 반려동물의 안구질환 이미지를 분류하는 데 ResNet50과 EfficientNet-B5 모델에 비해 빠르고 안정적으로 학습을 진행할 수 있으며, 정확도 면에서 효율적이라는 결과를 얻었다.