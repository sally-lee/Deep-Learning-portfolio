
## 1. Vectorization의 사용 예제

<br>

신경망이나 로지스틱 회귀를 프로그래밍할때 기억해야할것은 <br>
가능한 for문을 사용하지않는 것이다. <br>
for문을 쓰지않는게 항상 가능한 건 아니지만 <br>
필요한 값을 계산할때 내장함수나 다른 방법을 쓸수있다면 for문을 쓰는것보단 빠를것이다. <br><br>

### ex1)

$u = Av$

행렬 $A$와 벡터 $v$의 도트연산인 벡터 $u$를 계산할때 일반적인 정의는 아래와 같다.<br>

$u_i = \sum A_{ij} v_j $

<br>
이것은 아래와같이 코딩할수있다. <br>

```
u = np.zeros((n,1)) # u를 0인 벡터로 초기화
for i ...
     for j ...
          u[i] += A[i][j]*v[j] # 원소들을 각각 도트연산 후 더해준다
```

두개의 for문을 사용한다.<br>
하지만 Vectorization을 사용하면 loop없이 아래와 같이 간단하게 작성할수있다.<br>

```
 u = np.dot(A,v)
```
<br>

### ex2)


<img src="/Neural Networks and Deep Neural Networks/Logistic regression/image/003.png"><img src="/Neural Networks and Deep Neural Networks/Logistic regression/image/004.png"> <br>

벡터 v가 있고 벡터 v의 모든 원소에 exponential operation을 하고싶을때 아래와같이 코딩할수있다. <br>

```
import math 
u = np.zeros((n,1)) # u를 0인 벡터로 초기화  
for i in range(n): 
     u[i] = math.exp(v[i]) # for문을 통해 원소를 각각 계산 
```

파이썬 NumPy에는 벡터를 한번에 병렬계산할수있는 내장함수가 많다. <br>
아래와같이 for문을 제거하여 코딩할수있다.

```
import numpy as np
u = np.exp(v) # 벡터 v를 입력해 출력벡터 u를 한줄로 계산한다
```

vectorization 연산은 단순히 코드만 줄어드는것이아니라 <br>
딥러닝과 같이 데이터가 많아지는 상황에서 엄청난 시간을 단축할수있을것이다. <br><br>




| np.log(v) | 원소의 로그값을 구함  |
|:-----------|:---------------------|
| **np.abs(v)** | **절대값을 구함**  |
| **np.max(v,0)** | **v의 원소와 0중에서 큰값 반환**  |
| __v ** 2__ | **모든 원소 제곱한 벡터 반환** |

> NumPy 라이브러리엔 다양한 벡터함수들이 있다.
 
<br><br>

## 2. 로지스틱 회귀에서의 Vectorization

<br>
<img src="/Neural Networks and Deep Neural Networks/Logistic regression/image/011.png"> <br>



원래라면 로지스틱 회귀에서 m개의 트레이닝세트를 학습하는데에 첫번째 for문 1개, <br>
두개 이상(이미지같은경우 수십 수백개)의 피쳐를 계산하는데에 두번째 for문이 사용된다. <br>
두번째 for 문을 없애기 위해서는 먼저 $dw_1 , dw_2$등을 0으로 초기화하는 대신 하나의 $dw$ 벡터로 만든다. <br>
<br>

<img src="/Neural Networks and Deep Neural Networks/Logistic regression/image/008.png"> <br>

$dw$를 np.zeros((n_x,1))로 지정하여 n_x차원의 벡터로 만든다. <br>
그러면 아래 for문을 쓰는 대신 vectorization연산인 $dw$ += $x^{i}dz^{i}$로 바꿀수있다. <br><br>

<img src="/Neural Networks and Deep Neural Networks/Logistic regression/image/010.png"> <br>

그리고 이 부분 또한 $dw$ /= $m$ ( $dw$ 전체 Gradient 벡터를 $m$ (트레이닝세트)으로 나눈 평균)을 쓸 수있다. <br>


경사하강법의 for문 하나를 제거하는것만으로 코드는 빠르게 실행될수있다. <br>
하지만 **가장 좋은방법은** 위의 첫번째 for문도 Vectorization하여 최종적으로는 <br>
로지스틱 회귀에서 **for문을 하나도 쓰지않고 훈련세트 전체를 동시에 처리하는것**이라고할수있다. <br>

<br>


참조
---
https://youtu.be/pYWASRauTzs
