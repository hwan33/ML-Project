# Kaggle Competition

## Titanic - Machine Learning from Disaster

### Description

- 타이타닉호에 탑승한 인원들에 대한 정보를 학습한 모델으로 Test case의 사람들이 살아남을 수 있는지 예측


- 데이터 (csv file)
  - features
    - passenger id
    - survived
      - label (0 = No, 1 = Yes)
    - Ticket class : 1st, 2nd, 3rd
      - 1st가 가장 좋은 등급
    - Age
      - 실수 값으로 주어짐
    - Sex
      - male, female
    - number of siblings / spouses
    - number of children / parents
    - fare
      - 실수 값으로 주어짐
    - cabin number
    - port of embarkation
      - C = Cherbourg
      - Q = Queenstown
      - S = Southhampton


- 분석 및 전처리
  - 결측값
    - Age, Cabin, Embarked, Fare feature에서 결측값 존재
    - Age feature의 경우 이름에서의 title (Mr, Mrs, etc) 로 그룹화하여 평균값을 대입
    - Embarked feature의 경우 가장 많은 Southhampton 대입
    
  - 데이터 분석
    - 3등급의 사람들이 가장 많이 살아남았으며, 1, 2등급의 사람들은 적게 살아남았다
      - 신중하게 접근해야한다 
      - 오히려 비율로는 1등급 사람들이 가장 많이 생존하였다
    - 살아남은 여성의 비율이 70% 이상으로 남성보다 많이 살아남았다
      - 여성은 보호받을 수 있는 존재였다
    - 나이는 어릴수록 생존 확률이 높아졌다
      - 아이는 보호받을 수 있는 존재였다
    - 2, 3, 4인 가족이 많이 살아남았다
      - 1인 가족은 도움을 받을 수 없었고, 5명 이상의 구성원을 가진 가족은 오히려 생존하는데 어려움이 있었다
    - 요금은 등급과 유사한 feature 이므로 추후 삭제
    - 데이터 상으로는 어디에서 탑승했는 지가 생존에 영향을 미친다
      - Southhampton에서 가장 많이 살아남았다
      - 다만 여기에서 탑승자의 수가 가장 많아서 살아남았는지의 여부 확인 필요
      
  - feature engineering
    - String value들은 numerical value로 변경
    - 생존 확률과 상관 없는 feature라고 판단한 것은 drop
      - Name
      - Age
        - 유의미한 feature이지만 0~100까지 많은 value 가지수를 가지므로 drop
        - 대신 name과 연결하여 title을 categorize 하여 추출
      - Ticket
      - Fare
      - Cabin
      - PassengerId
    - Sibling/spouses & child/parent 는 Family라는 하나의 특성으로 합침
  
- 모델링
  - SGD Classifier
  - Gaussian Naive Bayes
  - Random Forest Classifier
  - Linear SVC
  - K-Nearest Neighbor Classifier