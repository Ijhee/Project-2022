## 📊&nbsp;&nbsp;&nbsp;Data augmentation and statistical hypothesis test to predict unbalanced insurance data
> 불균형한 데이터에서의 데이터 증강 기법 적용과 통계적 가설 검정 방법을 주안으로 둔 데어터 분석 프로젝트입니다. 보고서 및 발표 자료는 위에 기재해놨으니 참고해주시면 감사하겠습니다.

---

### 📌&nbsp;&nbsp;1) Purpose of Project
- &nbsp;&nbsp;머신러닝 기법을 활용한 예측의 과정에서 사용되는 데이터의 품질은 최종 예측 성능에 굉장히 많은 영향을 끼치는 것으로 알려져 있다. 하지만 데이터의 수집 과정과 수집 방법에 따른 데이터의 품질이 예측의 성능을 좌우하는 경향성을 불균형 데이터에서는 찾아보기 어렵다. 일례 로 예측의 평가 지표로 가장 많이 사용되는 정확도(Accuracy)는 모델의 학습 양상과 무관하게 불 균형 데이터에서 대부분 높은 수치를 기록한다. 두 범주의 비율이 굉장히 편향되어있기에 복잡한 데이터의 형태를 학습하여 예측하지 않고 단순히 다수의 범주로 통일하여 예측할 경우에도 높은 정확도를 기록할 수 있기 때문이다. 이러한 상황을 Paradox of Accuracy라 일컫기도 한다.</br>
&nbsp;&nbsp;정확도 지표를 통해 예측 성능을 측정하는 대다수의 경우에서는 해당 문제를 간과할 수 있다. 하지만 실생활에서는 다수의 경우를 높은 확률로 예측에 성공하는 것 만큼 소수의 경우를 판별하여 정확하고 예리하게 예측하는 것이 중요한 경우들이 존재한다. 신용카드 사기와 같이 개 인에게 심각한 악영향을 끼치는 예시를 생각해볼 수 있다. 하루에 신용카드를 통한 결제가 이루 어지는 사례는 셀 수 없이 많고 이 중 사기 거래가 이루어지는 경우는 극히 드물 것이라는 것을 알 수 있다. 따라서 어떤 모델이 특정 기간 동안의 신용카드 거래 정보를 수집하여 학습하고 정 상/사기 거래를 예측하는 과정에서 모든 거래가 정상이라 예측하여도 정확도는 99퍼센트 이상을 상회할 것이다. 하지만 높은 정확도의 이면에는 사기 거래의 피해자를 수혜할 수 있는 방안이 사 라지는 단점이 존재하게 되는 것이다.</br>
&nbsp;&nbsp;이를 해결하기 위해서 정확도 뿐만 아니라 정밀도(Precision), 재현율(Recall) 그리고 이 두 지표를 적절히 혼합한 F1 지표를 사용하여 다각화된 분석을 진행하고 있다. 다양한 평가지표를
통해 분석의 완결성을 더하는 것은 분명 불균형 데이터를 통한 예측 문제의 한계점을 해결하는 데에 도움을 줄 수 있으나 다분히 사후적이라는 판단에서 벗어날 수 없다. 따라서 본 분석에서는 [보험 데이터]를 선택하여 여러 데이터 증강 기법을 적용해 예측 문제를 해결하며 결과에 대한 검 정을 통해 실질적인 해결책을 제시하고자 한다.</br>

### 📌&nbsp;&nbsp;2) Data Introducing</br></br>
<p align="center">
<img width="750" alt="image" src="https://user-images.githubusercontent.com/96717686/209924828-dd2a7fe5-b27f-4769-abaa-397e82b103f3.png">
<img width="750" alt="image" src="https://user-images.githubusercontent.com/96717686/209924882-87447de0-6a6e-47e3-a590-c40fbf038b15.png"></p>
- 본 분석에 사용된 데이터는 382,154개의 행과 12개의 열로 이루어져 있다. Gender, Driving License, Region Code, Previously Age, Vehicle Damage, Vehicle Age, Annaul Premium 변수들은 범 주형 변수들이며 그 외 변수들은 연속형 변수이다. 또한 해당 데이터에는 결측치가 존재하지 않는다.</br>
분석에 사용된 데이터는 11개의 설명변수와 Response라는 종속변수로 구성되어 있다. 설 명변수 중 Id, Gender, Age, Region Code 변수들을 통해 고객들의 기본 정보를 알 수 있으며, Driving License, Vehicle Age, Vehicle Damage 변수들을 통해 고객들의 자동차 관련 정보들을 알 수 있다. 또한 고객들이 자사 보험과 1회 이상 접촉한 후에 가입 의향을 조사한 데이터이므로 Policy Sales Channel 변수와 Vintage변수를 통해 자사 보험 접촉 경로 및 접촉 시기 등을 알 수 있다. 추가적으로 접촉했을 당시 책정된 보험료를 Annual Premium 변수에서 확인할 수 있으며 Response는 종속변수로 고객이 자사 보험에 가입하고 싶은지에 대한 여부에 대한 정보를 담고 있다.</br></br>

### 📌&nbsp;&nbsp;3) Visualization
> 본 글에서는 데이터 시각화를 통해 인사이트를 얻어낸 경우만 기입하겠습니다.</br>
#### 1. 개별 변수들의 기초통계량 시각화</br>
- Annual Premium</br></br>
 <img width="600" alt="image" src="https://user-images.githubusercontent.com/96717686/209925848-bccc3f16-e83b-464c-b59f-4f4af30ba6f8.png"></br></br>
 &nbsp;&nbsp;Annual Premium의 경우 Histogram을 통해 특정 값의 빈도가 굉장히 높은 것을 파악할 수 있는데 해당 값은 Annual Premium 내의 최소값인 2,630이다. 또한 이는 추가적인 옵션 없이 기본 보험료를 내는 고객의 특성으로 해석할 수 있으므로 기본 보험료를 지불하는 고객과 그렇지 않은 고객들을 다른 범주로 구분하는 변수를 추가했다. </br></br>
- Age</br></br>
<img width="600" alt="image" src="https://user-images.githubusercontent.com/96717686/209926967-19a62b07-1aa3-40a0-a442-51a12c858d63.png"></br></br>
Age 변수는 20, 30대 와 40, 50대에 데이터가 밀집되어 있다. 따라서 데이터 전처리 과정에서 연령대를 grouping 하는 변수를 추가했다. </br></br>
- Policy Sales Channel</br></br>
<img width="350" alt="image" src="https://user-images.githubusercontent.com/96717686/209927323-0759e945-12ae-43df-b31f-90d8ebe5408a.png"></br></br>
 Policy Sales Channel 변수는 고객이 이용한 채널에 대한 정보를 담은 변수이다. 이 변수 를 통해 특정 소수의 채널(152, 26, 124 채널)을 이용하는 고객들이 타 채널을 이용하는 고객들보 다 상대적으로 많이 분포하는 것을 알 수 있다. 따라서 해당 채널들을 주요 채널들로 설정하여 새로운 변수로 추가하였다. </br></br>
- Region Code</br></br>
<img width="350" alt="image" src="https://user-images.githubusercontent.com/96717686/209927549-a97ec950-82a1-44f8-8106-d6b14745086e.png"></br></br>
Region Code 변수는 Policy Sales Channel과 마찬가지로 특정 지역의 데이 터 개수가 많은 것을 확인할 수 있다. 전체 데이터 중 지역 코드가 28인 경우가 107199 개로 전체 데이터의 28%를 차지한다. 따라서 인구 밀집 지역에 사는 고객들을 따 로 분리하도록 추후에 변수를 새로 추가하였다.</br></br>
- Response</br></br>
<img width="350" alt="image" src="https://user-images.githubusercontent.com/96717686/209927713-7befc2e6-2ea3-495f-be30-813e76a65999.png"></br></br>
종속변수인 Response의 분포를 살펴보면 Response가 0 인 경우, 즉 고객이 자사 보험 가입 의향이 없는 경우가 의향이 있는 경우보다 많다. 의향이 없는 경우는 전체 데이 터의 83.6%, 의향이 있는 경우는 전체 데이터의 16.4%로 종속 변수의 분포가 imbalance 한 것을 확인할 수 있다.</br></br>
#### 2. 독립변수들 간의 관계 시각화 </br></br>
- Vehicle Age & Vehicle Damage</br></br>
<img width="360" alt="image" src="https://user-images.githubusercontent.com/96717686/209928008-1f278c26-69c3-4f6f-b2f8-25ee7070c986.png"></br></br>
위 그림은 Vehicle Damage변수와 Vehicle Age변수의 관계에 대한 정보를 담고 있다. 본인 소유 자동차 연식이 1년 미만임에도 불구하고 자동차 파손 이력 여부가 있는 고객들 이 41,634명이 있는 것을 확인할 수 있으며 해당 고객들을 고위험군으로 분류할 수 있다. 이에 반해 본인 소유 자동차 연식이 2년 초과일 때 자동차 파손 이력 여부가 없는 고객들이 11명이 있는 것을 볼 수 있고 해당 고객들을 저위험군으로 분류할 수 있다.</br></br>
- Previously Insured & Vehicle Damage</br></br>
<img width="350" alt="image" src="https://user-images.githubusercontent.com/96717686/209928127-3652e13b-1beb-44a9-955c-6c96b5449784.png"></br></br>
위 그림은 Vehicle Damage 변수와 Previously Insured변수의 관계에 대한 정보 를 담고 있다. 타사 보험을 가입한 적이 존재하지 않지만(Previously_Insured : 0) 자동차 파손을 한 경험이 존재하는 (Vehicle_Damage : Yes) 고객들이 총 175,282명이 있음을 확인할 수 있다. 해당 고객들은 보험을 가입하지 않고 자동차 파손을 경험한 적이 있기에 위험군으로 분류할 수 있다.</br></br>
#### 3. 독립변수와 종수변수 간의 관계 시각화 </br></br>
- Vehicle Age & Response</br></br>
<img width="350" alt="image" src="https://user-images.githubusercontent.com/96717686/209928238-06bb3dc8-9cf7-4261-8a11-473f0161b601.png"></br></br>
Vehicle Age 변수와 종속변수인 Response변수의 관계에 대한 정보를 담고 있다. 본인 소유 자동차 연식이 1년 미만일 경우 자사 보험 가입 의향이 없는 비율 (Response=0)이 95%, 본인 소유 자동차 연식이 1년 이상 ~2년 이하일 경우 자사 보험 가입 의향이 없는 비율이 76%, 본인 소유 자동차 연식이 2년 초과일 경우 자사 보험 가입 의향이 없 는 비율이 60%이다. 이 결과 자동차 연식에 따라서 종속변수의 비율이 변한다고 판단할 수 있으 며, 해당 분석 결과를 이용하여 Sub Modeling을 진행했다.</br></br>
- Previously Insured & Response</br></br>
<img width="350" alt="image" src="https://user-images.githubusercontent.com/96717686/209928431-75cf04e3-91b3-41bd-96c7-07a758bf4f4a.png"></br></br>
Previously Insured 변수와 종속변수인 Response 변수의 관계에 대한 정보를 담고 있다. 타사 보험 가입을 하고, 자사 보험 가입 의향이 있는 135명의 고객이 존 재하며 해당 고객의 연령대 분포는 그림 21과 같이 나타난다. 해당 고객들의 연령대가 전체 데이 터의 연령대에 비해 낮은 것을 알 수 있다. 따라서 타사 보험 가입을 하고 자사 보험까지 가입한 고객들은 젊고 자산이 많을 가능성이 있음을 파악했다.</br></br>

### 📌&nbsp;&nbsp;4) Data Processing</br></br>
#### 1. 이상치 처리 </br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209929303-b079399b-47dd-4b4d-905d-75c095b9553a.png"> </br></br>
- 본 분석에서는 총 3가지 데이터 전처리 기법을 적용했다. 처음 과정은 이상치 처리 과정 이다. Boxplot을 확인했을 때는 Annual_Premium 변수 외에는 IQR 기준의 이상치를 확인할 수 없었다. 또한 Annual Premium 변수는 최소값인 2,630이 전체 데이터 의 16%를 차지하고 있을 뿐만 아니라 다수의 값들이 상대적으로 작은 값을 가진다. 따라서 값들 의 분포가 몰려 있으며 이에 따라 이상치의 개수가 굉장히 많은 것을 확인할 수 있다. 하지만 해 당 이상치들을 다 제거하게 될 경우 변수의 고유한 분포를 왜곡시키는 상이한 분포를 형성할 수 있기 때문에 IQR 기준의 이상치 값들을 제거하지 않았다. IQR 기준 이상치를 삭제하지 않은 반면 개별 데이터 자체의 논리가 성립하지 않는 경우를 탐색하여 데이터 수집 과정에서 생긴 오류라고 판단한 후 해당 케이스를 제거했다. 운전면허를 소지하지 않았는데 본인 소유 자동차가 파손된 고객들의 경우가 그 예시이며 이는 논리적으로 성립할 수 없다고 판단하여 해당 데이터를 의미론 적 이상치로 판단한 후 제거했다.</br></br>
#### 2. 인코딩 </br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209929355-721dd45d-8a4e-415c-b4cd-275856a6bedd.png"> </br></br>
- 인코딩 과정에서는 Label Encoding과 One-hot Encoding 총 2가지 방법론을 채택하였다. Label Encoding은 각 범주들을 알파벳 순서대로 숫자를 할당하여 변환하는 방법론이다. 이에 달
리 One-hot Encoding은 해당 변수의 각 범주들에 따라 Dummy Variable을 추가하는 방법이다.</br></br>
#### 3. 변수추가 </br></br>
- 총 10개의 변수를 추가했으며, 자세한 내용은 보고서에 기입되어 있으니 확인해주시면 감사하겠습니다.</br></br>
### 📌&nbsp;&nbsp;5) Modeling</br></br>
#### 1. Model Selection </br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209929590-6a76377d-be0e-4045-b934-6f36bb208777.png"></br></br>
<img width="825" alt="image" src="https://user-images.githubusercontent.com/96717686/209929520-c5201c98-119c-4ada-8139-e8badfa82dff.png"></br></br>
- 분석에서 사용할 모델을 선택하는 과정에서 임의성을 최대한 배제하기 위해 Model Selection의 과정을 거치게 되었다. 특정 모델을 분석에 사용하기 위해서는 모델과 데이터의 적합성을 평가해야 한다. 이를 위해 전체 데이터의 10%에 해당하는 부분집합부터 개수를 늘려가 전체 데이터의 100%에 해당하는 부분집합까지 총 10개의 부분집합을 생성한 후 데이터의 개수가 증가함에 따라 모델의 성능이 상승하는 관계성을 검토한다. 데이터의 개수와 모델의 성능이 양의 상관관계를 지니고 있음이 파악되면 해당 데이터 는 이 모델로 평가하기에 적합하다는 결론을 내릴 수 있게 되는 것이다. 본 분석에서는 위 그림의 결과를 바탕으로 CatBoostClassifier, LGBMClassifier, RandomForestClassifier, LogisticRegression, SGDClassifier의 5개 모델을 선정하였다.</br></br>
#### 2. Variable Selection </br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209929822-b48759db-b7d8-4cb0-867c-3917510b23cd.png"></br></br>
- 두번째는 Permutation Importance Method를 통한 변수 선택이다. Permutation Method는 Filter Method의 일례로서 개별 변수들의 중요도를 내림차순으로 정렬해 특정 임계점을 넘는 변 수만을 선택하여 최종 모형에 사용하는 방식으로 동작한다. 개별 변수의 중요도는 해당 변수가 포함되었을 때의 모델 성능에서, 배제되었을 때의 모델 성능을 빼는 과정을 통해 도출할 수 있다. 해당 변수를 제거하여 성능을 도출하기 위해서는 적합(fit)하는 과정을 변수 별로 두번씩 진행해야 하기 때문에 Permutation Importance는 해당 변수를 Shuffle하여 제거와 동일한 효과를 유도한다. 이 과정에서 중요도가 음수가 나오게 될 경우 해당 변수가 존재하지 않는 것이 모델의 성능을 향 상한다고 판단할 수 있기 때문에 임계점은 ‘0’ 으로 설정하는 것이 타당하다.</br></br>
#### 3. Variable Selection </br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209929929-07108c14-03c0-4ae1-9a6f-7b9eab555d30.png"></br></br>
- 세번째는 Sub-Modeling이다. Sub-Modeling은 전처리가 완료된 데이터를 두 부분집합으 로 분할하여 각각 다른 모델을 통해 병렬적으로 학습한 후 최종 결과를 종합하여 평가하는 방식 을 일컫는 용어이다. 앞서 언급한 바와 같이 “Vehicle Age”를 기준으로 데이터를 분할했을 때 특 정 부분집합에서 종속 변수가 균형적인 분포를 보이고 있음을 알 수 있었다. Sub-Modeling은 종 속변수의 상이한 분포를 각기 다른 모델을 통해 학습하여 불균형한 데이터가 지니는 문제점을 해 결할 수 있을 것이라는 기대효과가 존재한다.</br></br>
