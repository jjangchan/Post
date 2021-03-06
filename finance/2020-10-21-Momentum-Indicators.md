# 모멘텀지표(Momentum Indicators)



## 스토캐스틱(Stochastics)

> __신뢰도__ ★★★★
>
> __안정성__ ★★
>
> __민감도__ ★★★★
>
> __기간__ 단기 장기 거래 사용 가능, 특히 단기거래에 유용



__주가가 상승추세 또는 하략 추세를 보이고 있을 경우 상승 추세 일때는 최고점 부근에 형성되는 경향이 높고, 반대로 하락 추세 일 경우에는 최저점 부근에 형성되는 경향이 높다.__



#### 1. 계산법

$$
\%K = \frac{C-L5}{H5-L5} \times100 \\
\%D =K(MA{_3}) \\
C = 현재종가 \\
H5 = 최근 \ 5일간 \ 최고가 \\
L5 = 최근 \ 5일간 \ 최저가
$$



#### 2. 매매전략

* 오실레이터가  20 ↓ 매수 하고,  80 ↑ 매도 한다
* K선 기준으로 D선 상향 돌파시 매수, 반대로 하향 돌파시 매도
* 디버전스 적용
* 추세둔화(Hinge) 분석. Hinge란 상승 혹은 하락추세로 움직이던 K선이 갑자기 움직임이 둔화될 때가 있는데 이때를 Hinge라 한다. Hinge가 발생하면 스토캐스틱의 추세가 바뀔 가능성이 농후하다. 
* 추세 전환 실패(Failure) 분석. K 값이 85 이상 이거나 25 이하에서 K선과 D선이 교차하며 매매신호를 보인 후 바로 K선과 D선이 또 교차하여 매매신호를 보이는 경우를 Failure라 한다. 이 경우는 기조느이 추세가 더욱 강화된 것으로 판단한다.



## 슬로우 스토캐스틱(Slow Stochastics)

> __신뢰도__ ★★★★★
>
> __안정성__ ★★★★
>
> __민감도__ ★★★
>
> __기간__ 단기 장기 거래 사용 가능



__기본적인 스토캐스틱은 %K 와 %D의 변동폭이 너무 극심하게 나타나는 단점이 있다. 이를 보완 하기 위해 나온 지표이다.__

__안정성과 민감도는 하나를 얻으려면 다른 하나를 포기하여햐 하는 관계, 두 지를 한꺼번에는 충족할 수 없는, 트레이드 오프(trade-off) 관계이다.__



#### 1. 계산법

$$
\%D = Slow \ \%K \\
Slow \%D = \%D(MA_{3})
$$

#### 2. 매매전략 

* 오실레이터가  20 ↓ 매수 하고,  80 ↑ 매도 한다
* Slow K 기준으로 Slow D선 상향 돌파시 매수, 반대로 하향 돌파시 매도
* 디버전스 적용
* 추세둔화(Hinge) 분석. Hinge란 상승 혹은 하락추세로 움직이던 Slow K선이 갑자기 움직임이 둔화될 때가 있는데 이때를 Hinge라 한다. Hinge가 발생하면 스토캐스틱의 추세가 바뀔 가능성이 농후하다. 
* 추세 전환 실패(Failure) 분석. K 값이 85 이상 이거나 25 이하에서 Slow K선과 Slow D선이 교차하며 매매신호를 보인 후 바로 K선과 D선이 또 교차하여 매매신호를 보이는 경우를 Failure라 한다. 이 경우는 기조느이 추세가 더욱 강화된 것으로 판단한다.



## 상대강도지수

> __신뢰도__ ★★★★★
>
> __안정성__ ★★★★
>
> __민감도__ ★★★
>
> __기간__ 단기, 장기거래 모두 사용



__주가의 상승 or 하락 속도, 또는 더 구체적으로 말한다면 현재 시장의 분위기를 객관적으로 나타내주는 지표 중에서는 단연 대표적이다,__



#### 1. 계산법

$$
RSI=\frac{14일간의 \ 상승폭 \ 합계}{14일간의 \ 상승폭 \ 합계 + 14일간의 \ 하락폭 \ 합계} \times100
$$

#### 2. 매매전략

* RSI 값이 30 이하(과매도) 매수 , RSI 값이 70 이상(과매수) 매도
* 역추세 전환의 실패(Failure Swing) : 지지나 저항의 돌파를 확인하는 형태로 RSI 값이 이전의 고점을 돌파하지 못하고 하락하거나 이전 저점 아래로  떨어지지 않고 상승하는 것을 말한다.
* 디버전스
* 지지와 저항