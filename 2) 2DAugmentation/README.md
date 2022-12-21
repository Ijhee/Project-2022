## ⏺ Data Augmentation in Two-Dimensional Space based on the Predict Proba of the Model
  > 2차원으로 매핑한 데이터를 Model의 Predict Proba에 기반하여 데이터를 증강한다

---

### 📌&nbsp;&nbsp;Purpose of Project</br>
- Train data가 띄는 분포가 test data를 예측하는데 적합하다면, train data의 개수는 많으면 많을 수록 모델이 다양한 데이터를 학습할 수 있기 때문에 좋은 성능을 보이지 않을까? 라는 의문점을 갖게 되어 데이터 증강과 관련된 프로젝트를 진행했다. 데이터 증강 기법은 SMOTE, ROS, CTGAN 과 같이 기존의 다양한 방법론이 있지만 본 프로젝트에서는 predict proba을 이용하여 수리적인 관점에 기반해 데이터를 증강하는 새로운 관점을 제시한다.</br></br>
Model에서 제공하는 predict proba는 개별 데이터가 예측한 클래스로 분류될 확률이다. 이 말은 개별 데이터가 분류된 클래스를 나타내는 대표성이라 여길 수 있으며 따라서 Predict proba가 가장 높은 점들을 원의 중점으로 잡아 해당 점들을 기준으로 원을 그려가며 원 내에 데이터를 증강하도록 한다. 

### 📌&nbsp;&nbsp;Process
- #### 1) DATA
  > Kaggle에 있는 데이터를 이용했으며, 실험데이터는 총 5개로 구성했다. 각 데이터는 train test split 함수를 통해 Train data와 Test data로 분리한다.
- #### 2) PCA
  > ![image](https://user-images.githubusercontent.com/96717686/208847768-52e4d0c5-8af3-44ba-bb7a-87f847ffc38b.png)</br>
  > 
  > 먼저 원을 그리기 위해 분석하고자 하는 데이터(X_train, X_test)를 Scaling한 후, PCA를 통해 2차원으로 축소한다.
- #### 3) Predict Proba
  >  ![image](https://user-images.githubusercontent.com/96717686/208851612-69d7198d-c50d-4dc8-8fb1-f2ca6bc04897.png)</br>
  >  
  >  Logistic Regression Model을 이용하여 Predict Proba를 산출한다. 그 다음 모델의 예측값과 정답이 일치하는 데이터 중 0으로 예측한 Probability가 높은 case와 로 예측한 Probability가 높은 case의 index를 저장한다.
- #### 4) Make Circle & Augmenetation
  >  ![image](https://user-images.githubusercontent.com/96717686/208851612-69d7198d-c50d-4dc8-8fb1-f2ca6bc04897.png)</br>
  >  
  >  Predict Proba가 가장 높은 점을 원의 중심점으로 두고, 초기 반지름은 0.1로 설정한다. 그 다음 초기 반지름에 반지름 값을 0.1씩 더해가며 원을 그린다. 이 떄 주의할 점은 원의 중심과 같은 class를 가진 데이터 포인트가 4개 이상 발견될 경우 원의 반지름을 키우는 과정을 중지한다. </br></br>
  >  이는 원의 중심점이 outlier일 경우 타 데이터와 겹치는 순간까지 원을 그려 안정적인 위치에서 반복문을 중단하도록 하고, 만약 원의 중심점이 해당 class를 잘 대표한다면 반지름을 많이 키우지 않고 중심점 근처에 데이터를 많이 생산시키도록 한 장치이다.</br></br>
  >  위 과정이 모두 진행되면 원이 생성된다. 이제 원의 중심점을 기준으로 np.randon.normal을 통해 정규분포에서 데이터를 생성하여 원 내에 1000개의 데이터가 있을 때까지 반복문을 진행한다.
  >  
- #### 5) Result Analysis
  > [![image](https://user-images.githubusercontent.com/96717686/208855575-db5fd3b4-f37d-4dcd-9c36-43396cd94239.png)
](https://gaesae.com/164)
  >
  >  RandomforestClassifier로 accuracy를 측정했으며, 본 그래프는 데이터 증강한 Accuracy - 데이터 증강하지 않을 시 Accuracy 를 나타냈다. 음수 값일 경우가 더 많기 떄문에 대체적으로 데이터를 증강한 경우보다 데이터를 증강하지 않을 떄의 성능이 더 좋다고 평가할 수 있다. 해당 이유는 원을 그리기 위해 2차원으로 원본 데이터를 PCA 했기 때문에 원본 데이터의 정보가 손실됨에 따라 성능이 낮게 나온 것으로 예측된다. 따라서 성능이 좋지 않기 때문에 성공한 프로젝트라 볼 수 없으나, 기존의 데이터 증강과 다른 컨셉을 제시했다는 점에 의의가 있다.
