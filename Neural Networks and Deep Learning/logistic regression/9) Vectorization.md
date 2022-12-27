# Vectorization 


<br><br>

## 1. Vectorization의 정의
<br>

Vectorization(벡터화)란 데이터를 행렬화하여 계산하는것이다. <br>
프로그래밍에서는 CPU 및 GPU에서 활용가능한 병렬 명령어인 <br>
SIMD(Single Instruction Multiple Data)명령어를 사용하는 기술이다. <br>
for문과 같은 loop를 제거하고 데이터를 transpose하여 병렬계산해 연산속도를 높일수있다. <br><br>

예를들어 로지스틱 회귀에서는 $z = w^Tx+b$를 계산해야한다. <br>
$w$는 열벡터이고 $x$도 마찬가지이다. 피쳐가 많다면 매우 큰 벡터가 될것이다. <br>
$w$와 $x$는 모두 트레이닝 데이터세트에 따른 n_x차원을 가진 벡터이다. <br>
만약 Vectorization을 사용하지않고 계산한다면 아래와 같은 코드를 작성해야한다. <br>

```
z = 0
for i in range(n_x) # for문으로 데이터를 일일히 계산해준다
    uz += w[i]**x[i]
z += b
```

하지만 Vectorization을 사용하면 $w^Tx$를 직접 한번에 계산한다.

```
z = np.dot(w^T,x)+b #파이썬 명령어 np.dot(w,x)를 사용한다
```

아래의 예제에서 이 방법이 훨씬 빠르다는것을 알수있다. <br><br>




## 2. Vectorization을 사용하는 이유

<br>

<img src="/Neural Networks and Deep Neural Networks/Logistic regression/image/005.png"><br>
figure1) for문을 사용한 계산

<img src="/Neural Networks and Deep Neural Networks/Logistic regression/image/006.png"> <br>
figure2) 벡터화를 사용한 계산 <br><br>


```
import time # 계산에 걸리는 시간을 측정하기 위해 time 모듈을 불러온다
a = np.random.rand(1000000) # 100만차원의 난수로 배열 a를 만든다
tic,toc # 계산전 시간을 tic, 계산후 시간을 toc에 지정해 1000을 곱하여 밀리초 단위로 표현해준다
```

파이썬에서 위와 같이 100만의 배열을 만들어 서로 도트연산해줄때 <br>
벡터화를 사용한 계산과 그렇지 않은 계산은 약 300배정도의 속도차이를 보인다. <br>
5시간걸릴 코드를 1분만에 처리할수있는 속도차이를 보인다는것이다. <br>
<br>
딥러닝 이전 시대에서 벡터화는 그저 사용하면 좋고 사용하지않아도 그만이였지만 <br>
많은 데이터를 학습시킬수록 빛을 발하는 딥러닝 알고리즘에서는 <br>
트레이닝할 데이터세트가 수천, 수만개가 되었다. 따라서 벡터화는, <br>
학습시키는 시간을 대폭 절약할수있는 딥러닝 시대의 매우 중요한 기술이 되었다. <br>

<br>

참조
---
https://youtu.be/qsIrQi0fzbY


