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
#### 4. Data Augmentation </br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209930107-73258042-82a9-431c-ba14-d8c9ada5be88.png"></br></br>
- 네번째는 Data Augmentation 이다. 본 분석에서 주안점으로 두고 있는 부분이 Data Augmentation 이며 세가지 방법론과 세가지 비율을 계획하여 총 9 가지 증강 경우의 수를 생성했다. 각각의 방법론은 Random Over Sampling(이하 ROS), Synthetic Minority Over Sampling Technique(이하 SMOTE), Conditional Tabular Generative Adversarial Network(이하 CTGAN)이 해당되며 종속변수의 두 범주를 5:5, 6:4, 7:3의 비율로 총 3가지 경우의 수를 고려했다.</br></br>
#### 5. Final Data Form </br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209930389-4b02b27b-a36e-43ea-880c-19d685b30be5.png"></br></br>
- 최종 모델링 과정에서는 전처리가 완료된 데이터에 변수 선택과 데이터 증강을 순차적으로 적용하여 사전에 선택된 모델의 성능을 기록하게 된다. 또한 실험에 사용되는 데이터는 Model AB-trainN1-N2.csv 의 형태를 띄게 된다. Model 은 앞서 모델 선택에서 선정된 CatBoostClassifier, LGBMClassifier, RandomForestClassifier, Logistic Regression, SGDClassifier 의 다섯개 중 하나가 되며, A 는 변수 추가 여부에 따라 추가되었을 경우 V, 추가되지 않을 경우 O 가 된다. B 는 sub-modeling 여부에 따라 sub-modeling 을 진행했을 경우 bi, 진행하지 않았을 경우 f 가 된다. N1 은 전처리 경우의 수에 따라 1 부터 4 까지 경우의 수가 되며 N2 는 증강 기법에 따라 0 부터 9 의 값 중 하나를 할당받는다. 따라서 실험에 사용될 전체 데이터의 개수는 800 가지이다.</br></br>
### 📌&nbsp;&nbsp;6) Test and interpret results</br></br>
#### 기존 평가지표의 한계점 </br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209930703-c1b814c4-fe42-459c-9c74-6ad0c1e5b61b.png">
- Accuracy는 머신러닝의 분류 평가 지표 중 하나로 대부분의 분석에서 중요한 지표로서 사용된다. 하지만 불균형 데이터를 분류함에 있어 Accuracy는 더이상 좋은 측도가 될 수 없다. 그 이유는 분류기가 데이터 개수가 더 많은 Real Negative 집단에 편향된 학습을 진행하기에 Real Positive 집단은 거의 고려하지 못하기 때문이다. 또다른 성능 지표로서 Precision 및 Recall과 이 둘의 조화평균인 F-measure가 불균형 데 이터를 분류하는데 사용되었다. 하지만 이 세 지표 모두 오로지 True Positive만을 판단하는 기준 이기에 True Negative는 전혀 고려하지 않는다는 단점이 있다. 특히 F-measure은 Precision과 Recall의 가중평균으로 표현되고 이 가중치가 분류기에 따라 달라지기에 성능 지표로서 약점을 지 니고 있다.</br></br>
결국, 기존 평가 지표로서 Accuracy와 F-measure은 불균형 데이터를 다루는데 있어 신뢰 할 수 없는 결과를 낳는다. 하지만 MCC는 Confusion Matrix의 모든 값을 고려하였기에 다른 성능 지표보다 더 많은 정보를 담고 있다. 또한, 불균형 데이터를 분류할 때 가장 신뢰할 만한 평가 지표로 알려져 있다. </br></br>
#### MCC </br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209930818-6a3fc1e9-225f-404b-8976-7912cf2e4314.png"></br></br>
- MCC는 Bookmaker Informedness와 Markedness의 기하 평균으로 나타낼 수 있다. Confusion Matrix을 이용하여 피어슨 카이제곱 검정을 통해 파악된 Bookmaker Informedness 및 Markedness의 추정치를 바탕으로 MCC 추정치 또한 계산이 가능하다. 따라서 P-value를 통하여 해당 추정치가 예상된 범위 내의 값인지 판단할 수 있다. 본 분석에서는 MCC 추정치와 χ2(0.99,1) ≈ 6.63을 기준으로 적합도 검정을 실시하였고 이를 바탕으로 예상과 실제로 발생한 빈도의 차이가 적은 결과들을 선별하였다. 그리고 그 결과 들 중 MCC가 높은 상위 100개를 추출한 후 Accuracy가 높은 모형을 최종 결과물로 선정하였다.</br></br>
### 📌&nbsp;&nbsp;6) Test and interpret results</br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209930914-8e52aeac-010b-4fe4-a4f9-e216bdd948d4.png">
- 본 실험은 총 800개의 데이터에 대해서 진행되었으며 각각은 사용한 모델의 개수 5가지, 전처리 경우의 수 16가지, 데이터 증강 기법 10가지 경우의 수의 모든 조합으로 구성되어 있다. 이 중 앞서 언급한 바와 같이 chi검정을 통과한 결과 중 MCC 상위 100개의 결과를 분석하였다. 분석의 대상인 상위 100 개의 결과들은 Accuracy 의 한계점을 극복했다고 판단했으며 그림 32 와 표 33 에 나타나 있는 바와 같이 해당 결과 중 LGBMClassifier 을 사용하였을 때 Accuracy 91.04% 로 가장 좋은 성능을 거두었음을 알 수 있었다.</br></br>
<img width="850" alt="image" src="https://user-images.githubusercontent.com/96717686/209930990-2d9edb8c-c623-412b-97a7-99e298759325.png"></br></br>
- CatBoostClassifier, LGBMClassifier, RandomForest, LogisticRegression SGDClassifier 의 5 개 모델 중 CatBoostClassifier 은 상위 100 개의 결과물 중 한 개도 포함되지 못했으며 다른 모델은 각각 19개, 24개, 43개, 14개가 포함되었다. 상위 100개에 포함될 기대값인 20개를 기준으로 판단했을 때 LogisticRegression 이 가장 유의한 결과를 기록했음을 알 수 있다. 그림 34 는 모델 별 정확도를 Boxplot 으로 표현하고 있다. 이를 통해 LGBMClassifier 와 RandomForestClasifier 가 여타 모델에 비해 좋은 성능을 거두고 있음을 확인할 수 있다. 또한 모델 별 정확도 지표의 평균 등수를 계산했을 때에는, RandomForest 가 31 등을 기록해 평균적으로 가장 좋은 성능을기록함을 알 수 있었고, LGBMClassifier 가 43 등, LogisticRegression 이 58 등, SGDClassifier 가 62 등을 기록했다. Boxplot 통해 모델 별 정확도의 분포를 파악할 수 있다.</br></br>
- 이후 데이터를 처리한 방법론에 따른 세가지 결과 분석을 진행했다. 첫번째는 변수 추가 여부에 따른 결과 차이 분석이고 두번째는 인코딩/이상치 처리 여부에 따른 결과 차이 분석이며 마지막은 Sub-modeling에 따른 결과 차이 분석이다. 변수 추가 여부에 따른 결과는 새로운 변수 를 추가하지 않은 데이터 44개와 새로운 변수를 추가한 데이터 56개가 최종 상위 100개의 결과 에 포함되었다. 또한 Accuracy Boxplot을 통해 새로운 변수를 추가하는 것은 성능 향상 에 도움이 되었다는 사실을 파악할 수 있었다. 인코딩/이상치는 총 4가지 세부 경우의 수로 분할 되는데 1번 경우의 수는 Label Encoding과 이상치 처리 적용이며 2번 경우의 수는 Label Encoding과 이상치 처리 미적용, 3번 경우의 수는 One-Hot Encoding과 이상치 처리 적용, 4번 경 우의 수는 One-Hot Encoding과 이상치 처리 미적용이 그 각각의 경우이다. 이 경우 1번과 2번 데이터가 각각 53개, 30개 포함되어 기대값인 25개를 넘어서는 경향성을 보였다. 하지만 3번 전처리 결과 (One-Hot Encoding / 이상치 처리 적용)가 평균적으로 성능이 가장 좋은 것을 알 수 있었다. 마지막으로 Sub-modeling여부에 따른 분석에서는 Sub-Modeling을 한 경우가 81개로 압도적인 차이를 보였다. Sub Modeling을 진행했을 경우의 성능이 압도적으로 높게 측정되었음을 확인할 수 있다.</br></br>
- 데이터 증강의 경우에는 사용 방법론 3 가지와 종속변수의 비율 3 가지, 그리고 증강을 적용하지 않은 경우의 수를 포함한 10 가지 데이터가 파생되었다. 데이터를 증강하지 않은 경우는 오직 한 개가 상위 100 개 결과에 포함되었기 때문에 증강을 통해 Imbalance Data 를 효과적으로 처리할 수 있음을 알 수 있었다. 또한 SMOTE 방법론을 적용했을 때의 데이터가 각각 17,16, 13개 포함되어 기대값인 10개를 넘어서는 양상을 보였다. SMOTE 방법론을 적용한 5, 6, 7 번의 평균 성능이 여타 기법보다 우수함을 알 수 있다.</br></br>
### 📌&nbsp;&nbsp;7) Limitation of work & Future work</br></br>
- 분석을 진행하는 과정 속에서 3가지 한계점과 3가지 의의를 찾을 수 있었다. 우선 모든 모델링 과정에서 진행한 하이퍼 파라미터 튜닝 과정이 오로지 국한된 범위 내에서만 진행된 것이 첫번째 한계점이다. 하이퍼 파라미터를 올바르게 튜닝하기 위해서는 모든 범위 내에서 시각화를 병행하며 가장 좋은 성능을 보이는 지점을 찾아야 했으나 범용적으로 사용되는 범위 내에서만 이 과정을 진행하였다. 두번째 한계점은 데이터 증강과 통계적 가설 검정이 보험 데이터가 지니는 특수성 때문에 다른 데이터에도 일반적으로 적용하기 어렵다는 것이다. 마지막 한계점은 변수를 선택하는 과정에서 오직 Permutation Importance 방법론만 적용했다는 것이다. Drop Column Importance, IBS 등 다양한 방법을 적용해서 비교하지 못했기 때문에 다소 편향적인 결과가 도출 되었을 가능성을 배제하기 어렵다.</br></br>
- 반면 데이터를 증강하는 과정에서 종속변수의 두 범주의 비율을 5:5로 통일하지 않고, 6:4의 비율과 7:3의 비율로 경우의 수를 생성한 것이 본 분석의 장점 중 하나라고 생각한다. 또한 통계적 가설 검정을 추가적으로 진행하면서 불균형한 데이터를 평가하는 과정에서 Accuracy를 사용하는 과정에 당위를 부여할 수 있었던 것이 본 분석의 장점이라고 판단했다. 마지막으로는 Sub Modeling을 진행하면서 상이한 분포의 데이터의 학습을 가능케 하여 성능을 향상했다는 점에서 의의를 찾을 수 있었다.
