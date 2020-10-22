# 가격 지표(Price Indicator) 



## 이동평균선(Moveing Average)

> __신뢰도__ ★★★★★
>
> __안정성__ ★★★★★
>
> __민감도__ ★★★
>
> __기간__ 모두 사용가능



__이동평균선 이란, 평균을 구할 떄 사용되는 기간이 점차 이동한다고하여 이를 이동평균(moving average) 이라는 이름으로 부른다.__

__시장에서는 5일선 '심리선', 20일선을 '추세선', 60일선을 '수급선', 그리고 120일선을 '경기선' 으로 부른다.__



#### 1. 계산법



![{\displaystyle {\begin{aligned}{\overline {p}}_{\text{SM}}&={\frac {p_{M}+p_{M-1}+\cdots +p_{M-(n-1)}}{n}}\\&={\frac {1}{n}}\sum _{i=0}^{n-1}p_{M-i}.\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/61f0e3ed443130803f5e4f57924fed0f8d6a8f37)

Pm = 당일의 시장 가격  , Pm-n = n일 전의 시장 가격

연속적인 값을 계산할 때 새로운 값이 합산되고 가장 오래된 값이 제거되므로 이와 같이 간단한 경우에는 매번 전체 합산이 필요하지 않습니다.

![{\displaystyle {\overline {p}}_{\text{SM}}={\overline {p}}_{{\text{SM}},{\text{prev}}}+{\frac {1}{n}}(p_{M}-p_{M-n}).}](https://wikimedia.org/api/rest_v1/media/math/render/svg/73ee5b23cebd1c156f9e30ec52b0ed41b428895d)



#### 2. 단기 이동평균선과 장기 이동평균선

구하는 기간이 짧으면 최근의 환율 움직임에 예민하게 반응한다. 대신 기간이 길면 장기적인 흐름을 잘 나타내줄 수 있다.



예를 들어

``` 
환율 5,000 원 상승 이면,

5 일이면 5000/5 = +1000원 효과 , 500 일 이면  5,000/500 = +10원 효과
```



#### 3. 골든 크로스와 데드 크로스 

* 골든 크로스 : 단기 이동평균선이 장기 이동평균선을 상향 돌파 할 때,

* 데드 크로스 : 단기 이동평균선이 장기 이동평균선을 하향 돌파 할 때



## 거래량 조정 이동평균(volume-adjusted moving average)

> __신뢰도__ ★★★★★
>
> __안정성__ ★★★★★
>
> __민감도__ ★★★
>
> __기간__ 모두 사용가능



__거래량 조정 이동평균이란, 가격에 당일의 거래량을 곱한 값을 이동평균 한 것 이다.__



#### 1. 계산법

![This is the rendered form of the equation. You can not edit this directly. Right click will give you the option to save the image, and in most browsers you can drag the image onto your desktop or another program.](https://latex.codecogs.com/gif.latex?%5Csum_%7Bi%3D0%7D%5E%7Bn-1%7D%5Cfrac%7BV_%7Bi%7DP_%7Bi%7D%7D%7BV_%7Bi%7D%7D)



__V = 거래량 , P = 시장가격__



## 고저이동평균(High-low Moving Average)

> __신뢰도__ ★★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★★
>
> __기간__ 모두 사용능



__고저이동평균이란, 하루 중이 고가와 저가를 기준으로 이동평균을 산출한다.__



#### 1. 계산법

n일 고점이동평균, H = 최고 가격

![This is the rendered form of the equation. You can not edit this directly. Right click will give you the option to save the image, and in most browsers you can drag the image onto your desktop or another program.](https://latex.codecogs.com/gif.latex?MAHigh%20%3D%20%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D0%7D%5E%7Bn-1%7DH_%7Bi%7D)



n일 저점이동평균, L = 최저가격

![This is the rendered form of the equation. You can not edit this directly. Right click will give you the option to save the image, and in most browsers you can drag the image onto your desktop or another program.](https://latex.codecogs.com/gif.latex?MALow%20%3D%20%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D0%7D%5E%7Bn-1%7DL_%7Bi%7D)



## 이동평균선 그물지표(Moving Average Ribbon)

> __신뢰도__ ★★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★★
>
> __기간__ 장기+중기+단기가 결합된 형태



__일정한 날짜 간격이 있는 다수의 이동평균을 한꺼번에 한 화면에 표시 하는 지표__

* 수렴 할 경우
  * 각 기간의 이동평균이 별 차이가 없다. 변동이성이 낮아져서 횡보면이 전개 되었다는 의미.
  * 강력한 저항선 or 지지선이 된다는 의미.
* 발산 할 경우
  * 기존의 추세가 한창 힘을 받고 진행 되는 것으로 해석.



## 볼린저밴드(Bollinger Bands)

> __신뢰도__ ★★★
>
> __안정성__ ★★★★
>
> __민감도__ ★★★
>
> __기간__ 20일 SMA 주로 사용, 중기적인 분석 유효



__현재의 주가와 이동평균의 간격이 얼마나되는지에 따라 현재의 시장이 정상적인지 비정상적인 상태인지 판단하는 지표__



![img](http://postfiles8.naver.net/MjAxNjEwMzFfMTI0/MDAxNDc3ODkwNDUwNzIz.AmfdYwQpg4VxqT2tAMgbm35W-25GwT-BHxG4u-Bgf90g.a2PanhN4B6C6Fa0bijgQZ6vCw2vUb0kde7baLuhPs18g.JPEG.freewheel3/KakaoTalk_20161031_140613629.jpg?type=w773)

* 위쪽 밴드 : m+2a
* 중간 밴드 : m
* 아래 밴드 : m-2a
* 주가가 위쪽 밴드에 근접 할 때 매도 타이밍 
* 주가가 아래쪽 밴드에 근접 할 때 매수 타이밍
* 밴드의 폭이 좁아 지면 변동성이 낮고 조만간 큰폭의 가격변동이 나타날 것을 예고하는 신호



## 시카고 플로어 트레이더 피봇(CFTPP, Chicago Floor Traders Pivotal Point)

> __신뢰도__ ★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★★
>
> __기간__ 단기거래, 특히 스캘핑이나 데이트레딩



__하루 중의 가격 변동을 이용하여 지지선과 저항선, 그리고 중심적인 피봇을 미리 예측할 수  있는 방법__



#### 1. 계산법

​                               
$$
피봇\ 포인트(PP) = \frac{low+high+close}{\text3}\\
1차\ 저항선(R1) = PP\times2-low_{-1}\ |\ 2차\ 저항선(R2)=PP+(higt_{-1}-low_{-1}\ \\ 
1차\ 지지선(S1) = PP\times2+higt_{-1}\ |\ 2차\ 지지선(S2)=PP-(higt_{-1}-low_{-1})
$$


#### 2. 매매방법

* 1차 지지선 에서 선 매수를 하고 2차 지지선이 대기 하므로 매입 포지션을 늘려 가는데, 2차 지지선이 무너지면 매입 포지션을 손절로 대응 할 수 있다.
* 반대로 주가가 올라가면 1차 저항선 근처에서 일부 청산 해서 수익을 얻고 2차 저항선 근처에서 청산하는 전략을 취할 수 있다.



## 중간값(Median Price)

> __신뢰도__ ★★
>
> __안정성__ ★★★
>
> __민감도__ ★★★
>
> __기간__ 중기,장기 적합



__당일 주가의 최고가와 최저가의 중간값으로 산출된다.__



## 지수이동평균(Exponential Moving Average)

__최근 주가에 가중치를 더 주어 계산한다.__



#### 1. 계산법

$$
EMA =P \times K+EMA_{yest} \times (1-K)\\P=당일주가 \\ K=\frac{2}{N+1} \\ EMA_{yest}=전일 \ EMA
$$



## 이중지수이동평균(Double Exponential Moving Average)

> __신뢰도__ ★★★★
>
> __안정성__ ★★★★
>
> __민감도__ ★★★★
>
> __기간__ 모두 사용가능



__시차, 후행성의 문제점 인 과거의 주가나 현재의 주가나 모두 같은 비중으로 간주되는 문제점을 해결하려는 수단으로 고안되었다__.



#### 1. 계산법 

$$
DEMA=2 \times EMA-EMA(EMA) 
$$

#### 2. 매매전략

- 골든크로스 발생시 매수 신호
- 데드크로스 발생시 매도 신호
- SMA 보다 더 빠르게 반응한다. 대략 3일정도?



### 3. code

```c++
int EMA_function(float alpha, int latest, int stored){
  return round(alpha*latest) + round((1-alpha)*stored);
}
 
int ema_a = 0.06;
int ema_ema = 0;
int ema = 0;

void loop(){
  sensor_value = analogRead(sensor_Pin);
  ema = EMA_function(ema_a, sensor_value, ema);
  ema_ema = EMA_function(ema_a, ema, ema_ema);
    
  int DEMA = 2*ema - ema_ema;
}
```



## 엔빌로프(ENVELOPE)

> __신뢰도__ ★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★★
>
> __기간__ 중기 , 장기거래에 적합



__볼린저밴드 접근방식과 같으면 다른점은 중간 밴드를 중심으로 미리 정해진 '일정한 폭' 으로 범위가 정한다. 통상 범위는 0.1%~10% 정도가 된다.__



#### 1, 계산법

$$
Middle \ Band = SMV_{n} \\
Upper \ Band = Middle \ Band+(Middle \ Band \times a\%) \\
Lower \ Band = Middle \ Band-(Middle \ Band \times a\%) \\
$$



#### 2. 매매전략

* 주가가 Upper Band 에 근접하면 매도
* 주가가 Lower Band 에 근접하면 매수



## 파라볼릭(Parabolic Stop AND Reversal)

> __신뢰도__ ★★★★
>
> __안정성__ ★★★★
>
> __민감도__ ★★★
>
> __기간__ 장기 or 단기거래 모두 사용된다.



__SAR이란 '청산 및 반대 방향으로의 거래'를 의미한다. 기존의 포지션을 청산하고 반대 방향으로 거래하라는 뜻__



#### 1. 계산법

$$
PSAR_{t} =PSAR_{t-1}+AF \times(EP-PSAR_{t-1}) \\
단, AF=Acceleration \ Factor \ | \ EP=Extreame \ Point
$$

* AF = 0.02 부터 시작해서 매일 0.02 추가된다, MAX= 0.20

* EP = 극단점은 추세가 바뀌는 가격수준으로 정해진다.
* 추세가 상승세에서 하락세로 바뀔 떄라면 EP는 직전 최고가격
* 추세가 하락세에서 상승세로 바뀔 때라면 EP는 직전 최저가격 

* 추세가 막 바뀌는 첫 번째 날의 PSAR은 EP와 같은 값으로 설정된다.



#### 2. 매매전략

* 주가가 아래쪽에서 포물선을 그리면서 상승하고 있는 PSAR 건드리면 하락추세 전환 으로 간주하고 매도
* 주가가 위쪽에서 포물선을 그리면서 하락하고 있는 PSAR 건드리면 상승추세 전환으로 간주하고 매수 





