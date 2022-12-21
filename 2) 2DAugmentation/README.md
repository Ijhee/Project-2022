## Data Augmentation in Two-Dimensional Space based on the Predict Proba of the Model
  > 2차원으로 매핑한 데이터를 Model의 Predict Proba에 기반하여 데이터를 증강한다

---

### 📌&nbsp;&nbsp;Purpose of Project</br>
- Train data가 띄는 분포가 test data를 예측하는데 적합하다면, train data의 개수는 많으면 많을 수록 모델이 다양한 데이터를 학습할 수 있기 때문에 좋은 성능을 보이지 않을까? 라는 의문점을 갖게 되어 데이터 증강과 관련된 프로젝트를 진행했다. 데이터 증강 기법은 SMOTE, ROS, CTGAN 과 같이 기존의 다양한 방법론이 있지만 본 프로젝트에서는 predict proba을 이용하여 수리적인 관점에 기반해 데이터를 증강하는 새로운 관점을 제시한다.</br></br>
Model에서 제공하는 predict proba는 개별 데이터가 예측한 클래스로 분류될 확률이다. 이 말은 개별 데이터가 분류된 클래스를 나타내는 대표성이라 여길 수 있으며 따라서 Predict proba가 가장 높은 점들을 원의 중점으로 잡아 해당 점들을 기준으로 원을 그려가며 원 내에 데이터를 증강하도록 한다. 

### 📌&nbsp;&nbsp;Process
- #### 1) DATA
  > Data는 Kaggle에 있는 데이터를 이용했으며, 실험데이터는 총 5개로 구성했다.
- #### 2) PCA
  > 먼저 원을 그리기 위해 분석하고자 하는 데이터를 2차원으로 축소한다.
