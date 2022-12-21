## 📝&nbsp;&nbsp;&nbsp;Reference Point of Permutation Importance : Index Based Selection (On going Paper)
> Index를 기반으로 Permutation Importance의 Reference Poin를 제공
---

### 📌&nbsp;&nbsp;Purpose of Project
- 데이터 과학의 발전으로 과거에 비해 대용량의 데이터가 수집되고 있으며 최적의 분석 결과를 위한 변수 선택 알고리즘이 성공적인 분석 결과를 도출하기 위한 주안점으로 여겨지고 있다. 데이터 분석의 주제나 모형 종류 등 상황에 따라 적절한 변수 조합이 달라지게 되고 이에 따라 전진선택법, 후진선택법, 단계적선택법과 같은 합리적인 변수 선택 알고리즘 방법들이 대표적으로 사용되고 있다.</br></br> 
하지만 이러한 방법들은 시간이 다소 오래 소요될 뿐 아니라 비선형적 모델을 다룰 때에 적합하지 않다는 한계점이 명확하다. 개별 변수마다 데이터를 Shuffle한 후 모델의 예측값을 구하여 변수의 중요도를 파악하는 Permutation Feature Importance는 보다 직관적으로 이러한 문제를 해결해준다. 하지만 해당 방법을 적용했을 때에도 어떤 변수를 선택하고, 제거해야하는 지에 대한 기준은 모호하며 이를 해결하기 위해 Index를 활용한 새로운 방법론을 제시하고자 한다.
