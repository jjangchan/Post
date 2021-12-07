# 1) 이산확률분포

## 1. 확률분포란

한 변수가 어떤 실험이나 관찰의 결과로 나타날 수 있는 모든 상황과 각 상황이 나타날 확률을 표시한 것인데, 확률분포의 모양은 확률변수의 종류에 따라 상이하다.



## 2. 이산확률분포란

확률변수가 수량변수중에서 이산변수인 경우에 나타나는 분포를 의미한다.



## 3. 베르누이시행

어떤 실험에 대하여 2가지 결과만을 기대할 수 있는 것, 세가지 조건을 만족시키는 시행

- 한 사건의 두가지 결과 중 하나는 성공(S), 나머지 하나는 실패(F)로 구별
- 성공 확률 : p = P(S), 실패 확률 q = p(F) = 1-p, P(S)+P(F) = 1
- 각 시행은 서로 독립적이다. 즉, 한 시행의 결과는 '다음 시행의 결과에 아무런 영향을 미치지 못한다.'



## 4. 이항분포

### 정의

여러 번 베루누이 시행을 진행 할 떄, 성공의 횟수 혹은 실패의 횟수를 '이항확률변수(binomial random variable)'라고 한다. 'X'로 표시할 수 있다. 이항확률변수의 확률분포를 이항확률분포(binomial probability distribution) 혹은 간략히 이항분포(binomial distribution)라고 한다.

__ex) 동전을 3번 던져 앞면(H) 이 나올 확률__

1. 경우의 수는 $$2^3 = 8$$ 이다
2. 모든 경우의수를 표로 나타내면 아래와 같다.

<img src="C:\Users\momantic03\workspace\post\img\prob.JPG" align="left">



### 확률함수

<img src="C:\Users\momantic03\workspace\post\img\prob2.JPG" align="left">

```python
import operator as op
from functools import reduce

def nCr(n, r):
    if n < 1 or r < 0 or n < r:
        raise ValueError
    r = min(r, n-r)
    numerator = reduce(op.mul, range(n, n-r, -1),1)
    denominator = reduce(op.mul, range(1, r+1), 1)
    return numerator//denominator

# n : 시행횟수, x : 성공횟수, p : 성공확률, 1-p : 실패확률
def BPD(n, x, p):
    bpd = nCr(n,x)*(p**x)*pow(1-p, n-x)
    return bp
```



### 특성(기대값, 분산, 표준편차)

<img src="C:\Users\momantic03\workspace\post\img\prob3.JPG" align="left">

```python
import math

# 기대값
def EV(n, p):
    return n*p

# 분산
def Var(n, p):
    return n*p*(1-p)

# 표준편차
def SD(n, p):
    return math.sqrt(Var(n,p))

```



## 5. 포아송분포

### 정의

정해진 시간, 거리 혹은 장소에서 발생하는 사건(성공)의 횟수를 나타낸 것을 포아송 확률변수(poisson distribution)라고 하며, 포아송확률번수의 확률분포를 포아송분포(poisson distribution)라고 한다. 포아송확률변수는  아래의 조건을 만족해야한다.

- 독립성 : 어떤 구간에서 일어날 성공의 수는 다른 구간에서 일어날 성공의 수와 서로 독립적이다.
- 비례성 : 동일한 길이의 구간에서 일어날 성공의 확률은 같으며, 성공의 수는 구간의 길이에 비례한다.
- 비군집성 : 구간이 아주 작아지면 두 번 이상의 성공이 일어날 확률은 0에 근접한다.



### 확률함수

<img src="C:\Users\momantic03\workspace\post\img\prob4.JPG" align="left">

```python
import math

def PD(u, x):
    numerator = u**x
    denominator = reduce(lambda x, y: x*y, range(1, x+1, 1))
    e = pow(math.exp(1), -u)
    return (numerator/denominator)*e
```



### 특성(기대값,분산, 표준편차)

<img src="C:\Users\momantic03\workspace\post\img\prob5.JPG" align="left">

```python
import math

# 기대값
def EV(n, p):
    return n*p

# 분산
def Var(n, p):
    return n*p

# 표준편차
def SD(n, p):
    return math.sqrt(Var(n,p))
```



# 2) 연속확률분포



## 1. 정의

일정한 범위에 있는 모든 **실수 값**을 취할 수 있는 확률번수를 연속확률변수(continuous random variable) 라고 하며, 이러한 확률변수가 이루는 분포를 연속확률분포(continuous probability distribution) 라고 한다.



## 2. 특징 

연속확률분포에는 다음과 같은 특징들이 있다.

- 연속확률분포에서 특정한 값 'x'가 발생활 확률 거의 '1/∞'이기 때문에 '0'이다, 즉 "P(X=x)=0"
- 연속확률분포에서의 확률은 일정구간(interval) 사이의 값을 취할 확률로 계산된다. 즉, p(a <= X <= b)는 [a,b] 사이의 확률밀도함수 f(x)와 X축 사이의 면적이다,
- 확률밀도함수는 언제나 (+)값을 갖는다. 즉 f(x)>=0 이다.
- 확률밀도함수 아래에 있는 전체의 면적은 언제나 '1'이다. 즉 p(-∞ <= X <= ∞)=1 이다.

<img src="C:\Users\momantic03\workspace\post\img\prob6.JPG" align="left">



## 3. 균일(균등분포)

균일분포(continuous uniform distribution)는 균등분포라고도 하며, 확률변수 X가 취할 수 있는 값이 일정한 범위 내에서 같은 확률로 발생하는 분포를 말한다.

### 확률밀도함수

<img src="C:\Users\momantic03\workspace\post\img\prob7.JPG" align="left">

## 4. 정규분포

정규분포는 정규곡선(normal curve)으로부터 유래한 분포로 가우스가 물리계측의 오차를 계산하는 과정에서 도입된 확률분포로 자연과학 뿐만 아니라 인문사회과학에서도 유용하기 이용되고 있는데, 수리적으로 라플라스(Pierre Laplace)에 의해 정립된 정규함수로부터 유래한 분포이다.

### 확률밀도함수 

<img src="C:\Users\momantic03\workspace\post\img\prob8.JPG">

### 정규분포의 특성

정규분포는 다음과 같은 특성을 가지고 있다.

- 정규분포의 위치와 모양은 분포의 평균과 표준편차로 결정된다.
- 정규분표의 확률밀도함수는 평균(i)을 중심으로 대칭인 종 모양이다.
- 확률변수 X의 범위는 -∞ < X < +∞
- 정규곡선과 x축 사이의 전체면적은 무조건 '1' 이다.
- 분포의 평균은 정규분포의 위치를 나타내며, 표준편차는 분포의 모양을 나타낸다.

<img src="C:\Users\momantic03\workspace\post\img\prob9.JPG" align="left">



# 3) 표준정규분포(Z분포)



## 1. 정의

서로 다른 모든 정규분포의 평균과 표준편차를 표준화 하여 표준적인 정규분포를 만든 것이 표준정규분포(standard normal distribution) 이다.

확률 변수는 `Z`, 평균은 `0`, 분산이 `1` 이 되도록 표준화한 것을 의미하며, "Z~N(0,1)" 로 표현하고, 표준화 Z은 다음과 같이 구한다.

<img src="C:\Users\momantic03\workspace\post\img\prob10.JPG" align="left">

정규분포를 표준정규분포로 전환하기 위한 방법은 아래와 같다.

<img src="C:\Users\momantic03\workspace\post\img\prob11.JPG" align="left">

