## 기술적 지표(Technical Indicator)





## 가격지표



### 이동평균선(Moveing Average)

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



### 거래량 조정 이동평균(volume-adjusted moving average)

__거래량 조정 이동평균이란, 가격에 당일의 거래량을 곱한 값을 이동평균 한 것 이다.__



#### 1. 계산법

![This is the rendered form of the equation. You can not edit this directly. Right click will give you the option to save the image, and in most browsers you can drag the image onto your desktop or another program.](https://latex.codecogs.com/gif.latex?%5Csum_%7Bi%3D0%7D%5E%7Bn-1%7D%5Cfrac%7BV_%7Bi%7DP_%7Bi%7D%7D%7BV_%7Bi%7D%7D)



__V = 거래량 , P = 시장가격__





### 고저이동평균(High-low Moving Average)

__고저이동평균이란, 하루 중이 고가와 저가를 기준으로 이동평균을 산출한다.__



#### 1. 계산법

n일 고점이동평균, H = 최고 가격

![This is the rendered form of the equation. You can not edit this directly. Right click will give you the option to save the image, and in most browsers you can drag the image onto your desktop or another program.](https://latex.codecogs.com/gif.latex?MAHigh%20%3D%20%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D0%7D%5E%7Bn-1%7DH_%7Bi%7D)



n일 저점이동평균, L = 최저가격

![This is the rendered form of the equation. You can not edit this directly. Right click will give you the option to save the image, and in most browsers you can drag the image onto your desktop or another program.](https://latex.codecogs.com/gif.latex?MALow%20%3D%20%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D0%7D%5E%7Bn-1%7DL_%7Bi%7D)



### 일목균형표

__시장의 '균형' 을 '일목요연' 하게 나타내는 '표' 라는 뜻이다.  더 깊숙히 들어가면 가격론, 시간론, 파동론, 형보론 등의 세부적인 이론들로 구성되어 있다.__

* 가격론 : 가격의 목표치를 구하는 방법.
* 시간론 : 사건과 가격과의 관계를 밝히는 이론.
* 파동론 : 주가의 움직임을 일정한 파동으로 세분하는 방법.
* 형보론 : 특정한 모양이 반복되는 것을 살펴 가격 움직임을 예측. 즉 패턴 분석



#### 1. 계산법

* 전환선 = 최근 9일간 최고가격 + 최근 9일간 최저가격 / 2

* 기준선 = 최근 26일간 최고가격 + 최근 26일간 최저가격/2

* 선행스팬 1 = 당일의 기준선값 + 당일의 전환선값/2 의 수치를 26일 후에 기입
* 선행스팬 2 = 최근 52일간 최고가격 + 최근 52일간 최저가격/2 의 수치를 26일 후에 기입
* 후행스팬 = 현재 종가의 가격을 26일 뒤쪽 표시

﻿

#### 2. 매매방법

* 전환선의 방향에 때라 매입 또는 매도를 결정하는 방법
  * 하락하다가 상승세로 전환하면 매입 타이밍 간주
  * 상승하다가 하락세로 전환하면 매도 타이밍 간주
  * 빠르게 대응 할 수 있다.
  * 횡보 구간에서 수익 내기 어렵다.
* 기준선과 전환선의 교차를 이용하는 방법
  * 전환선이 기준선을 상향돌파 할 때 매입 타이밍 간주
  * 전환선이 기준선을 하향돌파 할 때 매도 타이밍 간주
* 구름을 이용하는 것
  * 가장 최적의 매입 타이밍은 주가가 구름 아래에 있다가 상승하여 막 구름 위로 올라섰을 때
  * 가장 최적의 매도 타이밍은 구름 위에 위치하던 주가가 하락하여 구름 아래로 내려섰을 때

﻿

