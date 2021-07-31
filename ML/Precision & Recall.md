# Precision & Recall

Precision(정밀도): 모델이 True라고 분류한 것 중 **실제로 True**인 것의 비율

![image](https://user-images.githubusercontent.com/55429912/127742535-91b0235a-07b6-41ae-808d-568608e79ce6.png)

- PPV(Positive Predictive Value)
- Negative 데이터 예측을 Positive 데이터로 잘못 판단하게 되면 업무상 큰 영향이 발생하는 경우
  - ex. 부정 행위가 아닌 것을 부정 행위로 판별 





Recall(재현율): 실제로 True인 것 중에서 모델이 **True라고 예측**한 것의 비율

![image](https://user-images.githubusercontent.com/55429912/127742576-4ad591d8-d605-4fca-87ad-f7597300bdca.png)

- Sensitivity(민감도), TPR(True Positive Rate)
- Positive 데이터 예측을 Negative 데이터로 잘못 판단하게 되면 업무상 큰 영향이 발생하는 경우
  - ex. 암 진단 모델이 암 환자를 암 환자로 판단하지 못하는 경우 





![image](https://user-images.githubusercontent.com/55429912/127743039-7d7dcacc-e529-4edc-9a2f-8ad6ea265edc.png)



- True Positive(TP) : 실제 True인 정답을 True라고 예측 (**정답**)
- False Positive(FP) : 실제 False인 정답을 True라고 예측 (**오답**)
- False Negative(FN) : 실제 True인 정답을 False라고 예측 (**오답**)
- True Negative(TN) : 실제 False인 정답을 False라고 예측 (**정답**)



## Precision 과 Recall의 Trade-Off

- 분류기는 항상 정밀도와 재현율의 Trade-Off를 갖고 있음

- 사용자는 분류기의 Threshold(임계값)을 통해 분류기의 출력을 조절

  ![image](https://user-images.githubusercontent.com/55429912/127743020-9eb0911e-0793-4123-a224-3568018fab9d.png)

