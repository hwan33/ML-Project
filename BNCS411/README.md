# ML-Project

Brain and Machine Learning/ 2020-2 / Professor Seok Heung il, Korea University

---

## Project A

### Description

- 여기에서는 인지 장애의 정도를 크게 3가지로 분류하였다
  - AD (Alzheimer's Disease) : 중증 치매
  - MCI (Mild Cognitive Impairment) : 경도 인지 장애
  - CN (Cognitive Normal) : 인지 정상


- 데이터 (csv 형식)
  - class of disease
  - cortical volume of a hippocampus
  - cortical volume of an entorhinal cortex


- Tensorflow나 scikit-learn에 있는 라이브러리를 사용하지 않고, pandas, numpy 등을 활용하여 데이터 분석


- 해마와 내측후각 피질 각각의 부피에 따른 3가지 그룹에 대한 분석 (Univariate Gaussian Distribution)


- 해마와 내측후각 피질 두가지 변수에 의한 3가지 그룹에 대한 분석 (Bivariate Gaussian Distribution)


### 사용 라이브러리

- numpy : 다차원 배열 처리
- pandas : 데이터 분석에 활용
- matplotlib : matlab과 유사하게 그래프를 그리는데 활용

---

## Project B

### Description

- 약 140개의 feature와 1600개에 달하는 instance를 분석하여 모델링을 하고, 이를 통해 적절한 인지 장애의 진단이 가능한지 테스트


- 데이터 (csv 형식)
  - feature
    - ['ST102CV':'ST99TA'] : 해마 및 내측후각 피질의 특정 부위
    - ['DX_bl'] : 진단 결과
    - ['ADAS11':'MMSE'] : 각종 검사 및 평가
  - instance : 1600명의 사람


- 데이터 분석 및 전처리
  - Pandas를 통해 데이터 분석 진행
  - 결측값 확인 후, ['ST123CV','ST64CV','ST123TA','ST64TA'] 네 가지 feature drop
    - 데이터가 너무 많이 손실되어 drop
  - StratifiedShuffleSplit을 사용하여 train set과 test set으로 데이터 나누기
  - StandardScaler를 사용해 정규화
  - SMOTE를 사용해 over-sampling
    - Imbalanced data에 의한 bias를 해결


- 모델링
  - 사용 모델
    - RandomForestClassifier
    - LogisticRegression
    - Keras를 활용한 Neural network
      - early stopping을 통해 over-fitting 방지

  - GridSearchCV를 활용해 적절한 parameter 설정
  - Accuracy와 Confusion matrix를 통한 모델 평가

### 사용 라이브러리

- numpy
- pandas
- matplotlib
- missingno : 결측치 시각화 툴
- scikit-learn : classifiers 사용
- Tensorflow : Keras를 통한 NN 사용
- imblearn : SMOTE 사용

---

## Project C

### Description

- 데이터가 이미지 파일로 주어져서 CNN 모델이 성능이 높았다


- 데이터 (npy 형식)
  - trn_dat.npy
    - shape : (2800, 32, 32, 16)
  - trn_lbl.npy
    - shape : (2800,)
  - sample_evaluation_data.npy
    - shape : (10, 32, 32, 16)


- 데이터 전처리
  - Reshape
    - 3d-array를 1d-array로 변경
    - Dimensionality reduction은 모델의 성능을 향상시킴
  - Normalize
    - 배열을 1000.0으로 나눔 (모든 값이 1000이하)
    - 모든 값을 0 ~ 1으로 정규화함으로써 data deduplication


- 모델링
  - Keras를 이용한 multi-layer perceptron
  - CNN
    - binary classifying model을 원하므로 다음의 설정 사용
      - sigmoid activation
      - binary crossentropy
      - adam
  - deep CNN
    - binary classifying model을 원하므로 다음의 설정 사용
      - sigmoid activation
      - binary crossentropy
      - adam
    - dropout layer를 통해 과적합 방지
> 차원 축소는 multi-layer perceptron 모델의 데이터에만 적용했다 
<br>CNN 및 deep CNN은 normalization만 처리해주었다

- modelcheckpoint를 사용해 훈련하는 동안의 가중치 저장


- early-stopping을 통한 과적합 방지


- matplotlib을 통해 모델에 대한 loss, val_loss, acc, val_acc값을 도식화하고 이를 고려하여 모델 성능을 높임

### 사용 라이브러리

- numpy
- tensorflow
- keras
