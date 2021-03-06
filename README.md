![image](https://user-images.githubusercontent.com/53938323/170057007-8a928a4e-5589-4ed3-b927-bacc82e478b7.png)


# 리그오브레전드 사전 승패예측

픽창에서 승패를 알 수 있다. 

## 문제

#### 1. Pick & Ban 단계에서 전적 검색만으로 승패를 객관적으로 예측할 수 없음.
#### 2. Pick & Ban 단계에서 상대의 정보를 수집할 수 없음.
#### 3. 사전 승패예측을 할 수 있는 모델에 대한 연구가 없음

## 선행연구


#### 1. 양방향 순환신경망 임베딩을 이용한 리그오브레전드 승패 예측 : LSTM / 58.07% 
    낮은 정확도, random 50% 와 단 8% 차이.
#### 2. 딥 러닝을 이용한 리그 오브 레전드 승패 예측 예비 연구 : DNN / 99.29%
    이론상 정확도는 높으나, 현실적으로 불가능한 모델.
    사후 데이터를 바탕으로 승패를 예측하고 있음.
    예측모델을 적용하려면 게임 시작 전에 예측을 해야하는데, 이에 대한 설명 및 대안이 없음.
#### 3. 기계학습을 활용한 E-Sports 승·패 예측에 관한 연구 : Decision Tree, NaiveBayes, Logistic Analysis / 92%
    2번 논문과 마찬가지로 실전에 적용할 수 있는 모델이 아닌, "학습을 위한 예측 모델"임.
#### 4. DNN을 활용한 ‘League of Legends’ 승부 예측 : DNN / 93.75%
    상기 논문들과 마찬가지로 실전 적용 불가. 학습 데이터셋은 26000개, 테스트 데이터 셋은 단 16개에서 나온 정확도이므로 신뢰할 수 없음.

## 해결 방안
#### 1. 대과거 데이터를 학습해서 과거 결과를 예측하도록 학습
    대과거 데이터를 학습해서 과거 결과를 예측하도록 설계해야,
    현실에서 과거 데이터를 기반으로 현재 진행하려는 게임의 결과를 예측할 수 있다.

![image](https://user-images.githubusercontent.com/53938323/169698830-a465e57b-4785-4bf6-a9c6-f0f23023a5f5.png)

#### 2. 상대의 정보를 수집할 수 는 없어도, 각 선수별 상대 전적을 포함하여 학습에 참여시키도록 함.
    당장의 경기에서는 상대가 누군지 알 수 없기에 명확한 상대 지표를 계산할 수 없지만, 
    이전 5개의 경기에서 각 아군의 맞라인(상대)상대로 평균적으로 어느정도 실적을 내는지를 계산하여 모델 학습에 포함한다면 
    해당 경기에서도 이 평균값 정도를 기대할 수 있으므로 정보 부족 보완.


## 서론
#### 1. 원시 데이터
    Riot Developer 에서 제공하는 API
    
#### 2. 데이터 수집 & 구조 & 전처리
    수집 방법은 다음과 같다.
    구조는 다음과 같다.
    전처리 과정은 다음과 같다.
    
#### 3. 모델 설계 & 구현
    모델은 서포트 벡터 머신을 이용하였다.
    kernel 종류 , C 와 gamma 값
    
#### 4. 검증
    테스트와 별개로, 실제 그랜드마스터 이상 유저에게 적용해보고 그 정확도를 받아온다.
    
#### 5. 시각화

## 연구 결과

#### 1. SVM 
    80.3%
                        precision    recall  f1-score   support

                   0       0.80      0.81      0.80      2298
                   1       0.80      0.79      0.80      2274

        accuracy                               0.80      4572
        macro avg          0.80      0.80      0.80      4572
        weighted avg       0.80      0.80      0.80      4572

#### 2. 앙상블
    Voting 분류기 정확도 0.8072
    RandomForestClassifier 정확도: 0.7934
    BaggingClassifier 정확도: 0.7917
    ExtraTreesClassifier 정확도: 0.7847
    GradientBoostingClassifier 정확도: 0.7396
    SVC 정확도: 0.8212  ( gamma : 450 , C : 300 )
    XGBClassifier 정확도: 0.7795

#### 6. 기대효과
    챌린저 티어에서 80%의 정확도를 보여주고 있다. 비슷한 실력대인 프로경기에서 적용을 할 수 있을 것으로 기대된다.
    e스포츠 시장은 약 14조, 가장 많은 시청자가 모이는 LCK, MSI, 롤드컵에서 많은 팬덤들이 누가 우승할 지 궁금해 한다. 
    이를 AI 로 예측할 수 있다면 AI 의 e스포츠 시장 진출이 확대될 것이라 생각한다. (이미 DeepLOL, Blitz, OP.GG 에서 비슷한 시도를 하고 있다.)
    
