# 변동성 지표(Variability Indicators)



## 평균진정 가격범위(ATR, Average True Range)

> __신뢰도__ ★★★★
>
> __안정성__ ★★★
>
> __민감도__ ★★★
>
> __기간__ 매매 타이밍을 알려주는 지표가 아니다.



__ATR은 변동성을 측정하는 지표이다. 급등 or 급락이 발생하면 ATR이 높게 나타는 경향이 많고 횡보하면 ATR 낮게 나타는 경향이 많다.__

#### 1. 계산법


$$
True\ High = 당일의\ 고점과\ 전일의\ 종가\ 중에서\ 높은\ 것\\
True\ Low = 당일의\ 저점과\ 전일의\ 종가\ 중에서\ 낮은\ 것\\
True\ Range=True\ High-True\ Low\\
ATR=\frac{True\ Range_{-1}\times(n-1)+True\ Range}{n}
$$

