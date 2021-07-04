

# CNN



![image](https://user-images.githubusercontent.com/55429912/124391221-8bdfd880-dd2a-11eb-96b0-c103acd46f71.png)

(숫자 2 이미지 입력 → 6개의 필터를 Convolution으로 계산 → 6개의 특성 맵 추출 →  Max Pooling을 통해 특성 맵의 크기를 줄임 → 17개의 필터로 Conv. & pooling 과정 반복 → 특성 맵의 출력을 일렬로 이어 붙여 완전연결 신경망으로 최종 클래스를 분류 → 0~ 9 까지의 원-핫 인코딩)

```
원-핫 인코딩은 단어 집합의 크기를 벡터의 차원으로 하고, 표현하고 싶은 단어의 인덱스에 1의 값을 부여하고,
다른 인덱스에는 0을 부여하는 단어의 벡터 표현 방식
```

① 입력 이미지의 feature을 추출

- Convolution

  ![image](https://user-images.githubusercontent.com/55429912/124392311-bd0ed780-dd2f-11eb-878b-7b4de71ac86f.png)

- 정사각형 모양의 필터를 이용하여 feature 추출

- 왼쪽 → 오른쪽으로 `Stride`만큼 이동시키며 포개지는 숫자를 곱해서 모두 더함

  - `Stride`: `Filter`의 이동 간격을 조절하는 파라미터
  - `Stride` 값이 커질수록, 결과 데이터의 사이즈가 작아짐

- **CNN에서 학습하는 것은 필터의 가중치**

- Convolution Layer에서는 Filter와 Stride의 작용으로 인해 Feature map의 크기는 입력데이터 보다 작음

  ![image](https://user-images.githubusercontent.com/55429912/124392929-f85ed580-dd32-11eb-8249-173326f61df2.png)

  - Padding을 통해 이미지의 공간정보를 유지

    

- 구해진 필터를 통해 이미지의 세부 특징을 추출

  ![image](https://user-images.githubusercontent.com/55429912/124392657-eaf51b80-dd31-11eb-84dc-aa6393ee3746.png)

  

② 필터의 개수만큼 나온 특성 맵을 MAX Pooling을 통하여 크기를 줄임

![image](https://user-images.githubusercontent.com/55429912/124392411-5ccc6580-dd30-11eb-8ce8-f5e6aa047d2e.png)

- 가장 큰 값만 추출하여 출력을 작게 만드는 방법
- **적당히 특성 맵의 크기를 줄이고, 특정 feature를 강조**

③ 완전 연결 신경망을 붙여 특성 맵을 사진의 클래스로 최종 분류



**구조**:

**입력**

- `Input`: 이미지 데이터

**특징 추출 단계(Feature Extraction)** 

- `Convolution Layer`: 필터를 통해 이미지의 특징을 추출
- `Pooling Layer`: 특징을 강화시키고 이미지의 크기를 줄임

**이미지 분류 단계(Classfication)**

- `Flatten Layer`: 데이터 타입을 Fully Connected 형태로 변경
- `Softmax Layer`: Classfication 수행

**출력**

- `Output`: 인식결과



**핵심 개념**:

1. CNN은 **이미지의 공간정보를 유지**한 채 학습
2. CNN은 신경망에서 학습을 통해 **자동으로 적합한 필터를 생성**
3. CNN은 Convolution과 Pooling을 반복적으로 사용하면서 불변하는 특징을 찾고, 그 특징을 입력데이터로 Fully-connected 신경망에 보내 Classfication을 수행



## 과대적합(Overfitting)



Overfitting: 모델이 훈련 데이터에 너무 잘 맞지만 일반성이 떨어짐

- 모델의 복잡도가 필요 이상으로 높기 때문에 발생
- 훈련 데이터셋에 잡음이 많거나 데이터가 너무 적을 경우 발생
  - 데이터가 너무 적으면 잡음이 섞인 패턴을 감지하여 학습할 수 있기 때문



해결 방안:

1. 훈련 데이터를 더 많이 모음
2. 정규화
3. 훈련 데이터의 잡음을 줄임(오류 수정 및 이상치 제거)



**규제**: 모델을 단순하게 하고 과대적합의 위험을 감수시키기 위해 모델에 제약을 가하는 것





## 과소적합(underfitting)



underfitting: 모델이 너무 단순해서 데이터의 내재된 구조를 학습하지 못하는 경우



해결 방안:

1. 파라미터가 더 많은 복잡한 모델을 선택
2. 모델의 제약을 줄이기(규제 하이퍼파라미터 값 줄이기)
3. 조기 종료시점(overfitting)까지 충분히 학습



