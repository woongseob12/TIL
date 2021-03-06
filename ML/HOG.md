# HOG(Histogram of Oriented Gradients)



HOG

- 컴퓨터 비전, 및 이미지 처리 시 Object detection의 목적으로 사용되는 특성
- 이미지의 지역적 Gradient를 해당 영상의 특징으로 사용하는 방법

![image](https://user-images.githubusercontent.com/55429912/124394016-5c37cd00-dd38-11eb-9cbe-6ed457ddae1f.png)

`Histogram`: 도수 분포표(구간별 빈도수를 나타낸 그래프)

`Oriented`: 방향

`Gradient`: 변화량

>  Pixel ⊂ Cell ⊂ Block 

```
Step 1
	- Using 8 * 8 pixel cell, compute gradient mag/direction
Step 2
	- Create a histogram of generated 64(8 * 8) gradient vectors
	- Each cell is then split into angular bins, each bin corresponds to a gradient direction(9 bins 0 - 180º) 
	- This reduces 64 vectors to just 9 values
```



① 대상 영역을 일정 크기의 셀로 분할

② Gradient를 이용하여 대한 Local Histogram을 생성

- edge를 검출하기 위해 1D kernel 사용 ⇒ 가로, 세로 각각 양옆의 픽셀 값을 빼주는거

  ![image](https://user-images.githubusercontent.com/55429912/124415672-4c4bd780-dd90-11eb-8a41-3ff0e7a6f028.png)

- 구한 x축 방향, y축 방향 edge를 통해 Orientation을 계산

  ![image](https://user-images.githubusercontent.com/55429912/124416361-ccbf0800-dd91-11eb-9ecc-f7e1ed9c6449.png)

- Gradient value는 0(검) - 255(흰)사이의 값을 가짐

  ![image](https://user-images.githubusercontent.com/55429912/124417069-528f8300-dd93-11eb-95ed-e1d1228e08d7.png)

- `Orientation`을 다 사용할 경우 bin이 int 형태여도 360개나 생성됨

- 적당한 `quantization`을 수행

  ![image](https://user-images.githubusercontent.com/55429912/124423157-8f617700-dd9f-11eb-929e-20c3680c223c.png)

  - 20º 단위의 9개의 bin, 12º 단위의 15개의 bin, 10º 단위의 18개의 bin ...  

    

③  Local Histogram를 이어붙여 일렬로 된 Vector 생성

![image](https://user-images.githubusercontent.com/55429912/124423423-16aeea80-dda0-11eb-950f-e97d3be9bcd3.png)



![image](https://user-images.githubusercontent.com/55429912/124395572-d3249400-dd3f-11eb-97ee-8075c8979156.png)

④ SVM을 통한 검출

![image](https://user-images.githubusercontent.com/55429912/124395629-1979f300-dd40-11eb-8405-8e424ac411c3.png)



참고자료 : 

[1] https://eehoeskrap.tistory.com/98

[2] https://jangjy.tistory.com/163

[3] https://en.wikipedia.org/wiki/Histogram_of_oriented_gradients