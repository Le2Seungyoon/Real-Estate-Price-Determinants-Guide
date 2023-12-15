## 금융 소프트웨어 개발 프로젝트 : 부동산 가격 결정요인 가이드

### 배경
부동산 매매시 고려할 다양한 요소들이 존재하며,  
이런 요소들에 대한 정보들은 범람하나 대체로 거시적이고, 일반론적인 경향이 강함  
따라서 지역적, 시간적 특성을 반영한 구체적인 정보를 제시할 필요성 존재  

### 주요 기능  
특정 지역을 선정하여 해당 지역에서 어떤 요인이 가격 결정력이 높은지 제시  
이를 바탕으로 이용자는 부동산 매물을 선정함에 있어 주요 요인을 고려하여 
가치가 높은 부동산을 선택할 수 있는 가이드를 제시  

### 결과물  
<img src="https://github.com/Le2Seungyoon/Real-Estate-Price-Determinants-Guide/assets/118061818/250f98fa-6e99-4343-80d2-a9c143ebe005/web_sample.png" width="512" height="256"/>

### 데이터  
|Feature|Description|
|---|---|
|법정동|지역 관련 변수|
|지하철역 개수|지역 접근성 관련 변수|
|노령화지수|지역 거주인구 관련 변수|
|건폐율|재건축 관련 변수|
|용적률|재건축 관련 변수|
|건축년도|재건축, 건물 노후도 관련 변수|
|층 위치|건물 유형 관련 변수|
|전세가율|거시경제 관련 변수|
|소비자 물가지수|거시경제 관련 변수|
|회사채|거시경제 관련 변수|
|면적당 가격|가치를 나타내는 종속변수|

데이터 출처: 

### 프로세스  
1) Model Define:  
   지역별로 vanilla LGBM 모델을 생성 
2) Hyperparameter Tuning:  
   GridsearchCV를 통해 넓은 구간에서의 최적 파라미터 조합 탐색 후,
   Optuna를 통해 좁은 구간에서 최적 파라미터 값 도출  
3) Permutation Feature Importance:  
   Greedy 알고리즘인 Tree 모델의 Feature Importance가 가지는 단점을 보안하기 위해,    
   반복 시행을 통해 변수 중요도를 반환하는 Permutation Feature Importance를 사용  
   이를 통해 구해진 중요도를 웹에 전달하여 시각화

### 실행  
1) 모델링을 위해서는 modeling.ipynb 실행  
2) 이후 생긴 --을 이용하여 visualize.ipynb 실행  
3) 최신화를 위해서는 데이터셋 출처에서 최신 데이터를 다운받은 후 전처리하여 dataset.csv와 같은 양식의 데이터 구축  
