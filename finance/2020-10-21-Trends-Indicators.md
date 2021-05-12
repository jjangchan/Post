# 추세 지표(Trends Indicator) 



## 방향성지수(DMI,Directional Movement Index)

> __신뢰도__ ★★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★★
>
> __기간__ 중,장기 지표



__시장의 방향성과 추세의 강도를 계랑화한 지표이다. ADX와 병행하여 사용하면 더욱 신뢰성을 높이게 된다.__



#### 1. 계산법

* DM(Directional Movement)

$$
\bigtriangleup High=금일의고점-전일의고점 \\
\bigtriangleup Low = 전일의저점-금일의저점 \\
　
\\
\begin{align} 
1.
& \bigtriangleup High \ ,\bigtriangleup Low <0 \ or \ \bigtriangleup High= \bigtriangleup low, \\
& Plus \ DM=0 \\
& minus \ DM=0 \\
2.
& \bigtriangleup High > \bigtriangleup Low, \\
& Plus \ DM = \bigtriangleup High \\
& minus \ DM = 0 \\
3.
& \bigtriangleup High < \bigtriangleup Low, \\
& Plus \ DM=0 \\
& minus \ DM=\bigtriangleup Low
\end{align}
$$

* True Rage

$$
True \ High = 당일자 \ 최고점과 \ 전일 \ 종가 \ 중에서 \ 높은 \ 것 \\
True \ Low = 당일자 \ 최저점과 \ 전일 \ 종가 \ 중에서 \ 낮은 \ 것 \\
TR(True \ Range)=True \ High-True \ Low
$$

* +DI,-DI

$$
+DI = \frac{EMA_{+DM}}{EMA_{TR}}\times100 \\
-DI = \frac{EMA_{-DM}}{EMA_{TR}}\times10
$$

#### 2. 매매 전략

* +DI 가 -DI를 상향 돌파할 때 매매 신호
* +DI 가 -DI를 하향 돌파할 때 매도 신호



#### 3. ERR(Extern Point Rule) 적용 매매 전략

* +DI 선이 -DI 선 상향 돌파+전고점 돌파
* -DI 선이 +DI  선 하향 돌파+전저점 돌파



## 방향성지표(DX,Directional Index)

> __신뢰도__ ★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★
>
> __기간__ 중,장기 지표



__+DI 와 -DI가 교차하는 시점은 상승추세나 하락추세가 정점을 만들고 되돌아서서 어느 정도 방향을 나타낸 이후이다. 따라서 시차 문제가 발생한다.__

__따라서 DX는 전반적인 추세의 강도를 종합적으로 판단하는 지표이므로 시차 문제를 다소 완화할 수 있다. 또한 매매지표가 아니라 방향성지표로 추세가 강한지 약한지 판단할 수 있는 지표이다.__



#### 1. 계산법

$$
DX=\frac{\left |plusDI-minusDI\right |}{\left |plusDI+minusDI\right |}\times100
$$







## 평균방향성지표(ADX,Average Directional Movement Index)

> __신뢰도__ ★★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★
>
> __기간__ 중,장기 지표



__ADX는 __

__1. DX의 이동평균이다. 이동평균을 산출함으로써 DX 움직임의 불규칙성이 안화되었고, 추세의 전환점을 파악하기도 용이해졌다.__

__2. 웰러스 월더는 주가의 방향성의 정도, 다시 말하여 '추세'가 얼마나 강력한지 여부를 지수로 표현하려고 노력하였다.__







#### 1. 계산법

$$
ADX=\frac{(n-1)\times ADX_{-1} \times DX}{n}
$$



#### 2. 매매 전략 

__수렴 과 괴리를 이용__

* 수렴
  * 주가가 최고점 경신하면서 동시에 ADX도 최고점 경신 상승추세 매우 강력 신호
  * 주가가 최저점 경신하면서 동시에 ADX도 최고점 경싱 하락추세 매우 강력 신호
* 괴리
  * 주가는 최고점 경신, ADX는 최고점 경신 못한다면 추세의 강도 저하 신호
  * 주가는 최저점 경신, ADX는 최고점 경신 못한다면 추세의 강도 저하 신호



## 평균방향성지표 순위(ADXR,Average Directional Movement Index Rating)

> __신뢰도__ ★★★★
>
> __안정성__ ★★★★
>
> __민감도__ ★★
>
> __기간__ 중,장기 지표



__당일의 평균방향성지표(ADX)와 n일 전 ADX의 중간값이다. 두개의 ADX에 대한 평균값이다.__

__기준선 20을 넘어선다면 현재의 시장은 추세적 시장, 반대로 아래로 하회한다면 현재의 시장은 횡보하는 비추세적 시장으로 간주한다.__





#### 1. 계산법

$$
ADXR=\frac{ADX_{0}+ADX_{-n}}{2}
$$



#### 2. 매매 전략 

* 20일선을 넘으면 추세적 시장이므로 MACD 등과 같이 추세추종형 기술적지표를 사용하여 매매한다면 매우 효과적이다.







## 이동평균 수렴발산(MACD, Moving Average Convergence Divergence)

> __신뢰도__ ★★★★★
>
> __안정성__ ★★★★
>
> __민감도__ ★★★
>
> __기간__ 장기,단기거래 모두 사용가능



__이동평균은 시차라는 문제점이 있다. 구하는 기간이 길면 길수록 시차 현상은 더 심해진다.__

__이동평균 수렴발산은 단기 이동평균선과 장기 이동평균선의 차이가 최대한으로 벌어진 시점이 바닥에 가까운 시점이라는 사실을 발견하였다.__



#### 1. MACD 히스토그램(Histogram) 

* 기울기는 인접한 두 막대의 관계에 의해 정의된다.
* 당일의 막대가 전일의 막대보다 더 높으면 MACD 히스토그램의 기울기는 양(+) 이고, 더 낮으면 기울기는 음(-) 이다.
* 기울기가 가격과 같은 방향으로 움직일 경우에 주가의추세에 확신을 가져도 된다. 반대방향으로 움직이면 의문점을 가질 필요가 있다.



#### 2. 계산법

$$
MACD = EMA_{12}-EMA_{26}\\
Signal = EMA(MACD_{9})\\
EMA = Exponctial\ Move\ Average\ 지수이동평균
$$

  

#### 3. 매매 전략

* MACD 곡선이 시그널 곡선을 상향 돌파 할 때 매수 시기
* MACD 곡선이 시그널 곡선을 하향 돌파 할 때 매도 시기
* MACD 값이 (-) 에서 양(+) 으로 전환 되면 상승추세  반대는 하락추세



## 큐스틱(Qstick)

> __신뢰도__ ★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★★★
>
> __기간__ 장기거래에 효과적



__개장가와 종가와의 관계를 과학적으로 측정하여 시장에서의 세력균형을 파악하기 위하여 개발된 지표.__



#### 1. 계산법

$$
Qstick = Moveing \ Average(ClosePrice-OpenPrice,8) \\
Qstick \ MA = Moveing \ Average(Qstic,8)
$$



#### 3. 매매 전략

* Qstick 이 하락세 이면 매도 포지션 or 반대로 상승세 이면 매수 포지션
* Qstick 이 Qstick Average 를 상향 돌파하면 매수 포지션 or 반대로 하향 돌파하면 매도 포지션



## 소나

> __신뢰도__ ★★★
>
> __안정성__ ★★★★
>
> __민감도__ ★★★
>
> __기간__ 장기,단기 사용 가능, 장기가 더욱 효과적



__노무라 증권 조사부에서 개발한것으로 오늘자 지수이동평균을 n일자 이전의 지수이동평균석을 차감하는 방식이다.__

__추세가 상승세이면 상세의 강도가 강화된다면 주가는 점점 상승폭을 늘릴 것이면 덩달아 이동평균의 값도 증가한다. 그러므로 현재의 이동평균의 값과 n일자 이전의 이동평균을 서로 비교한다면 그차이는 점점 벌어질 것이다.__



#### 1. 계산법

$$
SONAR = EMA_{0}-EMA{-n} \\
Signal = EMA(SONAR_{n})
$$



#### 2. 매매 전략

* SONAR 가 Signal 을 상향 돌파하면 매입 타이밍
* SONAR 가 Signal 을 하향 돌파하면 매도 타이밍



## 상대강도 스토캐스틱(StochRSI)

> __신뢰도__ ★★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★★
>
> __기간__ 모두 사용 가능



__RSI의 장점인 안정성 과 스토캐스틱에 장점인 민감성을 살려서 만든 하이브리드 지표__



#### 1. 계산법

$$
StochRSI = \frac{RSI-RSI_{L}}{RSI_{H}-RSI_{L}} \times 100 \\
단, RSI=당일의 \ RSI \\
RSI_{h}
$$



#### 2. 매매전략

* StockRSI 가 80 위로 올라가서 80 밑으로 하향 돌파하면 매도 기회
* StockRSI 가 20 밑으로 내려가다 20 위로 상향 돌파하면 매수 기회



## 추세채널지수(CCI,Commodity Channel Index)

> __신뢰도__ ★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★★
>
> __기간__ 장,단기 사용 가능



__현재의 주가가 이동평균과 많이 떨어져 있으면 조만간 주가가 방향을 돌려 이동평균 부근으로 가까워질 것이고, 결국 현재의 추세는 조만간 끝이 날 것이라고 예상할 수 있다.__



#### 1. 계산법

$$
CCI = \frac{M-m}{d} \times 0.15 \\
M = \frac{당일의 고가+당일의저가+종가}{3} \\
m = M의 \ n일자 \ 이동평균 \\
d = 평균오차
$$



#### 2. 매매전략

* 과매수(+100), 과매도(-100)을 활용한 매매 전략
* 0 선 기준 상향돌파시 매수, 하향 돌파시 매도 전략
* 디버전스 이용
* +100을 상향 돌파하고 100을 다시 하향 돌파시 매도 , 반대로 -100을 하향돌파하고 -100을 다시 상향 돌파하면 매수 전략



## 알리게이터(Aligator) 악어



__Alligator's Jaw : "악어의 턱", 일반적으로 기간은 13, 간격은 8로 설정한 Smoothed Moving Average이다.__

__Alligator's Teeth : "악어의 이빨", 일반적으로 기간 8, 간격은 5로 설정한 Smoothed Moving Average이다.__

__Alligator's Lips : "악어의 입술", 일반적으로 기간 5, 간격은 3로 설정한 Smoothed Moving Average이다.__

__간격은 봉 앞의 미래를 예상하듯이 앞으로 뻣어 있다.__



#### 1. 계산법

$$
Median \ Price= \frac{(High+Low)}{2} \\
Allgators \ Jaw = SMMA(MedianPrice,13,8) \\
Allgators \ Teeth=SMMA(MedianPrice, 8, 5) \\
Allgators \ Lips=SMMA(MedianPrice, 5, 3) \\
$$





