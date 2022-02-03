# ADsP
Studying for getting ADsP certification

# 기초통계분석 Fundamental statistics analysis
data(mtcars)                      # datasets 패키지의 "mtcars"라는 데이터셋의 마일(mpg), 총마력(hp)의 상관관계 분석을 실시한다
a <- mtcars$mpg                   # a에 mpg칼럼의 값들을 저장
b <- mtcars$hp                    # b에 hp칼럼의 값들을 저장
cor(a,b)                          # correlation(상관계수) 구하기 
cov(a,b)                          # covarience(공분산) 구하기
cor.test(a, b, method="pearson")  # cor.test를 이용하여, mpg와 hp의 상관관계 분석을 실행한 결과

<img width="322" alt="피어슨상관분석결과" src="https://user-images.githubusercontent.com/87562188/150898107-9e76343f-a293-49fb-8481-a23b83a68164.png">

## 결과의 p-value = 1.788e-07이 유의수준 0.05보다 작다의 의미는 무엇일까?
인터넷 검색을 통해서 답변을 찾아보았다

For calculation, here's how to Convert 1.778e-07 to Number using the formula above, step by step instructions are given below

Step 1, Here is the separated name of the scientific notation value 1.788e-07.
 Where,
 1.788 = coefficient(계수);
 e = 10 to the power(10의 거듭제곱 이라는 뜻의 영어표현);
 -07 = exponent(지수); # 지수앞에 -가 있으면 10 나누기 지수값, 지수앞에 기호가 없으면 10 곱하기 지수값. EX) 10 -05 이면 10만분의 1임; 0.000 01 

Step 2, To convert, multiply "coefficient" by "10 to the power" of "exponent". Like this (1.788 * 10 ^ -07)
                                        
                                         1.788 * 10 -07

Step 3, After calculate the equation

                                          0.0000001.788

# 회귀분석 Regression Analysis
## 단순회귀분석

가. 회귀분석에서의 검토사항

1)회귀계수들이 유의미한가?
 * 해당 계수의 t 통계량의 p-값이 0.05보다 작으면 해당 회귀계수가 통계적으로 유의하다고 볼수 있다.
2)모형이 얼마나 설명력을 갖는가?
 * 결정계수(R²)를 확인한다. 결정게수는 0~1값을 가지며, 높은 값을 가질수록 추정된 회귀식의 설명력이 높다.
3)모형이 데이터를 잘 적합하고 있는가?
 * 잔차를 그래프로 그리고 회귀진단을 한다.

나. 회귀계수의 추정(최소제곱법, 최소자승법)
예시
 * 10년간 에어컨 예약대수와 판매대수 (단위 : 1,000대)
 예약대수(X) 19 23 26 29 30 38 39 46 49
 판매대수(Y) 33 51 40 49 50 69 70 64 89
 * 에어컨 판매대수에 대한 예약대수의 추정식 : 판매대수 = 6.41+1.53*예약대수

다. 회귀분석의 검정
 1)회귀계수의 검정
  * 회귀계수 β₁이 0이면 입력변수 x와 출력 변수 y사이에는 아무런 인과관계가 없다.
  * 회귀계수 β₁이 0이면 적합된 추정식은 아무 의미가 없게 된다.
    (귀무가설 : β₁=0, 대립가설 β₁≠0)
    
      예제
   * 10년간 에어컨 예약대수와 판매대수 (단위 : 1,000대)
     예약대수(X) 19 23 26 29 30 38 39 46 49
     판매대수(Y) 33 51 40 49 50 69 70 64 89
   * 위의 데이터에 대해 단순회귀분석을 실시하여 검정을 실시한다.
 
R code below

 x <- c(19, 23, 26, 29, 30, 38, 39, 46, 49)
 y <- c(33, 51, 40, 49, 50, 69, 70, 64, 89)
 lm(y~x)
 
 <img width="212" alt="회귀분석결과" src="https://user-images.githubusercontent.com/87562188/150897906-90464202-8746-4fae-883a-fb071c84661a.png">

 summary(lm(y~x))
 
 <img width="319" alt="summary(lm(y~x))" src="https://user-images.githubusercontent.com/87562188/150898422-6ec9ba1e-d886-4ad2-8b22-37557cbcb078.png">

## 결과해석

* x의 회귀계수인 t통계량에 대한 p-값이 0.000581로 나타나, 유의수준인 0.05보다 작으므로 회귀계수의 추정치들이 통계적으로 유의하다.
* 결정계수는 0.8341으로 높게 나타나 이 회귀식이 데이터를 적절하게 설명하고 있다고는 할 수 있다.
* 결정계수가 높아 데이터의 설명력이 높고 회귀분석결과에서 회귀식과 회귀계수들이 통계적으로 유의하므로 에어컨 판매대수를 에어컨 예약대수로 추정할 수 있다.
* 회귀분석 결과 "판매대수 = 6.4095+1.5295 * 예약대수"의 회귀식을 구할 수 있다.
   
## 다중회귀분석

1) 분석내용 : MASS 패키지의 "Cars93"라는 데이터셋의 가격(Price)를 종속변수로 선정하고 엔진크기(Engine-Size), RPM, 무게(Weight)를 이용해서 다중회귀분석을 실시한다.

R code below

library(MASS)

head(Cars93)

attach(Cars93)

lm(Price~EngineSize+RPM+Weight, data=Cars93)

<img width="319" alt="결과" src="https://user-images.githubusercontent.com/87562188/150900743-315c43e5-fcd3-4e98-a47c-d93aea9e20d5.png">

summary(lm(Price~EngineSze+RPM+Weight, data=Cars93))

<img width="314" alt="결과" src="https://user-images.githubusercontent.com/87562188/150900883-2a76a77f-5e05-483e-abb3-7a58604c60a3.png">

## 결과해석

* 여기서 F-통계량은 37.98이며 유의확률 p-value 값이 6.746e-16로 유의수준 5%하에서 추정된 회귀모형이 통계적으로 매우 유의함을 알 수 있다.
* 결정계수와 수정된 결정계수는 각각 0.5614, 0.5467로 조금 낮게 나타나 이 회귀식이 데이터를 적절하게 설명하고 있다고는 할 수 없다.
* 회귀계수들의 p-값들이 0.05보다 작으므로 회귀계수의 추정치들이 통게적으로 유의하다.
* 결정계수가 낮아 데이터의 설명력은 낮지만 회귀분석 결과에서 회귀식과 회귀계수들이 통계적으로 유의하여 자동차의 가격을 엔진의 크기와 RPM 그리고 무게로 추정할 수 있다.

## 로지스틱 회귀분석

1) 데이터 설명

림프절이 전립선 암에 대해 양성인지 여부를 예측하는 데이터

양성여부(r) = 전립선암에 대한 양성여부,  aged = 환자의 연령, stage = 질병 단계 : 질병이 얼마나 진행되어 있는지 나타내는 척도, grade = 종양의 등급 : 진행의 정도
xray = X-선 결과, acid = 특정한 부위에 종양이 전이되었을 때 상승되는 혈청의 인산염값

R code below

library(boot)

data(nodal)

a <- c(2,4,6,7)

data <- nodal[,a]

glmModel <- glm(r~., data=data, family="binomial")

summary(glmModel)

<img width="316" alt="결과" src="https://user-images.githubusercontent.com/87562188/150902756-6e8e2f03-6e02-40f9-8605-492bb1195836.png">

## 결과분석

* 2번째 변수인 양성여부를 종속변수로 두고 5개의 변수를 독립변수로 하여 로지스틱 회귀분석을 실시한 결과 age와 grade는 유의수준 5%하에서 유의하지 않아
이를 제외한 3개변수 stage, xray, acid를 활용해서 모형을 개발한다.
* stage, xray와 acid의 추정계수는 유의수준 5% 하에서 유의하게 나타나므로 p(r=1)=1/(1+e-(-3.05+1.65stage+1.91xray+1.64acid))의 선형식이 가능하다.

## 최적회귀방정식

###### 변수 선택법 예제(유의확률 기반)

x1, x2, x3, x4를 독립변수로 가지고 y를 종속변수로 가지는 선형회귀모형을 생성한 뒤, step()함수를 이용하지 않고 직접 후진제거법을 적용하는 R코드를 작성하여 변수제거를 수행해본다.

R code below

1) 데이터 프레임 생성

 x1 <- c(7, 1, 11, 11, 7, 11, 3, 1, 2, 21, 1, 11, 10)
 
 x2 <- c(26, 29, 56, 31, 52, 55, 71, 31, 54, 47, 40, 66, 68)
 
 x3 <- c(6, 15, 8, 8, 6, 9, 17, 22, 18, 4, 23, 9, 8)
 
 x4 <- c(60, 52, 20, 47, 33, 22, 6, 44, 22, 26, 34, 12, 12)
 
 y <- c(78.5, 74.3, 104.3, 87.6, 95.9, 109.2, 102.7, 72.5, 93.1, 115.9, 83.8, 113.3, 109.4)
 
 df <- data.frame(x1, x2, x3, x4, y)
 
 head(df)
 
 <img width="318" alt="결과" src="https://user-images.githubusercontent.com/87562188/150907252-3e36c09e-034b-43a3-8b57-1cf4b2df2cd3.png">

 2) 회귀모형(a) 생성
 
 a <- lm(y~ x1+x2+x3+x4, data=df)
 
 summary(a)
 
<img width="316" alt="결과" src="https://user-images.githubusercontent.com/87562188/150907430-dafb51b2-a3a3-4df5-bd40-fd96730fbefa.png">

 * summary(a)에서 모형의 유의성을 판단하기 위해 F-통계량을 확인한 결과, 111.5로 나타났으며 유의확률이 4.756e-07임으로 통계적으로 유의하게 나타났다. 하지만
 각각의 입력변수들의 통계적 유의성을 검토해 본 결과, t 통계량을 통한 유의확률이 0.05 보다 작은 변수가 하나도 존재하지 않아 모형을 활용할 수 없다고 판단되었다.
 적절한 모형을 선정하기 위해 유의확률이 가장 높은 x3 를 제외하고 다시 회귀모형을 생성해 보았다.
 
 3) 유의확률이 가장 높은 변수를 제거하고 다시 회귀모형(b)을 생성
 
 b <- lm(y~ x1+x2+x4, data=df)
 
 summary(b)
 
<img width="314" alt="결과" src="https://user-images.githubusercontent.com/87562188/150907979-253e751d-d809-404c-89e7-60219f978654.png">

* x3 변수를 제거한 후, 모형의 유의성을 다시 검토한 결과 F 통계량에 대한 유의확률은 통계적으로 유의하게 나타났다. 모든 변수들의 t 통계량에 대한 유의확률이 0.05보다 낮아야 하지만 
 x1을 제외한 2개 변수의 유의확률이 0.05보다 높게 나타나 유의하지 않은 결과를 보였다. 따라서 유의확률이 가장 높은 x4 변수를 제외하고 회귀모형을 다시 생성하였다.
 
 4) 유의확률이 가장 높은 변수를 제거하고 다시 회귀모형(c)을 생성
 
 c <- lm(y~ x1+ x2, data=df)
 
 summary(c)
 
  <img width="318" alt="결과" src="https://user-images.githubusercontent.com/87562188/150908378-fc674ece-5c1e-4146-98e2-a70c1272214b.png">

 * F통계량을 통해 유의수준 0.05하에서 모형이 통계적으로 유의함을 확인할 수 있다.
 * 다변량회귀분석에 선정된 x1, x2 변수에 대한 각각의 유의확률 값이 모두 통계적으로 유의하게 나타났다. 수정된 결정계수는 0.9744로 선정된 다변량회귀식이 전체
  데이터의 97.44%를 설명하고 있는 것을 확인할 수 있었다.
 * 위의 후진제거법을 통해 최종적으로 얻게 된 추정된 회귀식은 y = 52.57735 + 1.46831x1 + 0.6625x2 이다. 
 
###### 변수 선택법 예제(벌점화 전진선택법)

이번에는 step 함수를 사용하여 전진선택법을 적용하는 R코드를 작성하여 변수 제거를 수행해보자.

>**참고** 
>
> step(lm(출력변수~입력변수, 데이터세트), scope=list(lower=~1, upper=~입력변수), direction="변수선택방법")
>
> scope - 변수선택 과정에서 설정할 수 있는 가장 큰 모형 혹은 가장 작은 모형을 설정. scope가 없을 경우 전진선택법에서는 현재 선택한 모형을
> 가장 큰 모형으로, 후진제거법에서는 상수항만 있는 모형을 가장 작은 모형으로 설정한다.
>
> direction - 변수선택법(forward: 전진선택법, backward: 후진제거법, stepwise: 단계적선택법)
>
> k - 모형선택 기준에서 AIC, BIC와 같은 옵션을 사용 -k=2이면 AIC, k=log(자료의 수) 이면 BIC 

R code below

1) step함수를 이용한 전진선택법의 적용
 
 step(lm(y~1, data=df), scope=list(lower=~1, upper=~x1+x2+x3+x4), direction="forward")
 
<img width="327" alt="결과" src="https://user-images.githubusercontent.com/87562188/150909534-984ebfcc-6b28-4c73-8d37-329ead2ae71a.png">

 * 벌점화 방식을 적용한 전진선택법을 실시한 결과, 가장 먼저 선택된 변수는 AIC값이 58.852으로 가장 낮은 x4 였다. x4에 x1을 추가하였을 때 AIC 값이 28.742로 낮아지게 되었고,
  x2 를 추가하였을 때 AIC 값이 24.974으로 최소화되어 더 이상 AIC를 낮출 수 없어 변수 선택을 종료하게 되었다.
 * 최종적으로 선택된 추정 회귀식은 y = 71.6483 -0.2365x4 + 1.4519x1 + 0.4161x2 이다.
 
###### 변수 선택법 예제(벌점화 후진제거법)

가. 활용데이터
 * 전립선암 자료(8개의 입력번수와 1개의 출력 변수로 구성)
 * 마지막 열에 있는 변수는 학습자료인지 예측자료인지를 나타내는 변수로 이번 분석에서는 사용하지 않는다.

lcavol = 종양 부피의 로그, lweight = 전립선 무게의 로그, age = 환자의 연령, lbph = 양성 전립선 증식량의 로그, svi = 암이 정낭을 침범할 확률,
lcp = capsular penetration의 로그값, gleason = Gleason 점수, pgg45 = Gleason 점수가 4 또는 5인 비율, lpsa = 전립선 수치의 로그

R code below

library(ElemStatLearn)

Data = prostate

data.use = Data[,-ncol(Data)]

lm.full.Model = lm(lpsa~., data=data.use)

나. 후진제거법에서 AIC를 이용한 변수선택

R code below

backward.aic = step(lm.full.Model, lpsa~1, direction="backward")

>R프로그램 내부의 문제로 ElemStatLearn패키지 다운로드 불가능 -> 이후에 문제해결 후 결과물과 분석 추가

# 시계열 분석

시간의 흐름에 따라 관찰된 데이터를 시계열 데이터 또는 시계열 자료라고 한다. 이러한 시계열 자료에는 주식가격 데이터, 실업률, 기후데이터 등 우리 주위에서 많이 찾아볼 수 있다.
시계열 자료는 대부분 비정상정을 띄는데 이를 정상성 시계열 자료로 변환하여 분석을 실시 한다. 정상성이란 평균이 일정할 때, 분산이 일정할 때, 공분산도 단지 시차에만 의존하고
실제 특정 시점 t, s에는 의존하지 않을 때 만족한다. 시계열 자료를 분석하 때에는 회귀분석(계량경제)방법, Box-Jenkins 방법, 지수평활법, 시계열 분해법 등이 있으며, 시계열 모형에는 
자기회귀 모형(AR, Autoregressive model), 이동평균 모형(MA, Moving Average model), 자기회귀누적이동평균 모형(ARIMA, autoregressive integrated moving average model)이 있다.

## R을 이용한 시계열분석

 영국 왕들의 사망 시 나이 데이터를 이용한 시계열분석

* 영국 왕 42명의 사망 시 나이 예제는 비계절성을 띄는 시계열 자료
* 비계절성을 띄는 시계열 자료는 트렌드 요소, 불규칙 요소로 구성
* 20번째 왕까지는 38세에 55까지 수명을 유지하고, 그 이후부터는 수명이 늘어서 40번째 왕은 73세까지 생존

R code below

1. 분해 시계열

가) 자료 읽기 및 그래프 그리기

library(tseries)

library(forecast)

library(TTR)

king <- scan("http://robjhyndman.com/tsdldata/misc/king.dat", skip=3)

king.ts <- ts(king)

plot.ts(king.ts)

<img width="340" alt="결과" src="https://user-images.githubusercontent.com/87562188/151259408-fa566a23-f743-43dd-9d29-765c160f3623.png">

나) 3년마다 평균을 내서 그래프를 부드럽게 표현

king.sma3 <- SMA(king.ts, n=3)

plot.ts(king.sma3)

<img width="338" alt="결과" src="https://user-images.githubusercontent.com/87562188/151259958-8354e446-8d09-42ce-936b-29cb1d2f2ce9.png">

다) 8년마다 평균을 내서 그래프를 부드럽게 표현

king.sma8 <- SMA(king.ts, n=3)

plot.ts(king.sma8)

<img width="342" alt="결과" src="https://user-images.githubusercontent.com/87562188/151260131-cdf89dfa-ebf0-43b0-8a32-6fd3e502a306.png">

2. ARIMA 모델

가) 개요

* ARIMA 모델은 정상성 시계열에 한해 사용한다.
* 비정상 시계열 자료는 차분해 정상성으로 만족하는 조건의 시계열로 바꿔준다.
* 이전 그래프에서 평균이 시간에 따라 일정치 않은 모습을 보이므로 비정상시계열이다. 따라서 차분을 진행한다.
* 1차 차분 결과에서 평균과 분산이 시간에 따라 의존하지 않음을 확인한다.
* ARIMA(p,1,q)모델이며 차분을 1번 해야 정상성을 만족한다.
 
R code below

king.ff1 <- diff(king.ts, differences=1)

plot.ts(king.ff1)

<img width="341" alt="결과" src="https://user-images.githubusercontent.com/87562188/151260758-bbca0831-caed-418a-81a2-cceca03d1d01.png">

나) ACF와 PACF를 통한 적합한 ARIMA 모델 결정

 ① ACF
  * lag는 0부터 값을 갖는데, 너무 많은 구간을 설정하면 그래프를 보고 판단하기 어렵다.
  * ACF값이 lag 1인 지점 빼고는 모두 점선 구간 안에 있고, 나머지는 구간 안에 있다.

R code below

acf(king.ff1, lag.max=20)

<img width="339" alt="결과" src="https://user-images.githubusercontent.com/87562188/151261581-4d77135b-c704-4c3e-8cfd-3e44f5fc3c4e.png">

acf(king.ff1, lag.max=20, plot=FALSE)

<img width="318" alt="결과" src="https://user-images.githubusercontent.com/87562188/151261649-f786da7f-15c1-4518-9c2e-a14701c8d0fd.png">

 ② PACF - PACF 값이 lag 1,2,3에서 점선 구간을 초과하고 음의 값을 가지며 절단점이 lag 4이다.
 
R code below

pacf(king.ff1, lag.max=20)

<img width="340" alt="결과" src="https://user-images.githubusercontent.com/87562188/151262048-02aee39b-f06d-4ed0-84da-e45e5da1a159.png">

pacf(king.ff1, lag.max=20, plot=FALSE)

<img width="314" alt="결과" src="https://user-images.githubusercontent.com/87562188/151262145-a33878d4-b665-4489-afdc-66f63b7fd468.png">

다) 종합

* ARMA 후보들이 생성

① ARMA(3,0) 모델 : PACF 값이 lag4에서 절단점을 가짐. AR(3) 모형

② ARMA(0,10 모델 : ACF 값이 lag2에서 절단점을 가짐. MA(1) 모형

③ ARMA(p,q) 모델 : 그래서 AR모형과 MA모형을 혼합

라) 적절한 ARIMA 모형 찾기
 * forecast package에 내장된 auto.arima() 함수 이용
 * 영국 왕의 사망 나이 데이터의 적절한 ARIMA모형은 ARIMA(0,1,1)이다.
 
R code below

auto.arima(king)

<img width="317" alt="결과" src="https://user-images.githubusercontent.com/87562188/151262619-21afbe04-3e0c-4961-a5e0-0e3270ed1d13.png">

마) 예측
* 42명의 영국왕 중에서 마지막 왕의 사망시 나이는 56세
* 43번재에서 52번째 왕까지 10명의 왕의 사망시 나이를 예측한 결과 67.75살로 추정된다.
* 5명 정도만 예측하고 싶다면, 옵션에 h=5를 입력한다.
* 신뢰 구간은 80%~95% 사이

R code below

king.arima <- arima(king, order=c(0, 1, 1))

king.forecasts <- forecast(king.arima)

king.forecasts

<img width="322" alt="결과" src="https://user-images.githubusercontent.com/87562188/151263063-59fdbc27-2416-46fc-907f-e0c4daa6df88.png">

# 다차원척도법

객체간 근접성(proximity)을 시각화하는 통계기법이다. 군집분석과 같이 객체들을 대상으로 변수들을 측정한 후에 개체들 사이의 유사성/비유사성을 측정하여 개체들을 2차원 또는 3차원
공간상에 점으로 표현하여 개체들 사이의 집단화를 시각적으로 표현하는 분석방법이다.

## 다차원척도법 종류

###### 계량적 MDS(Multi Dimensional Scailing)
* 데이터가 구간척도나 비율척도인 경우 활용한다.(전통적인 다차원 척도법) N개의 케이스에 대해서 p개의 특성변수가 있는 경우, 각 개체들간의 유클리드 거리행렬을 계산하고 개체들간의 
비유사성S(거리제곱 행렬의 선형함수)를 공간상에 표현한다.

cmdscale 사례

* MASS package의 eurodist 자료를 이용한다.
* 유럽의 21개 도시들 사이의 거리를 측정한다.
* cmdscale을 이용하여 2차원으로 21개 도시들을 매핑한다.
* 종축은 북쪽 도시를 상단에 표시하기 위해 부호를 바꾼다.

R code below

library(MASS)

loc <- cmdscale(eurodist)

x <- loc[, 1]

y <- -loc[, 2]

plot(x, y, type="n", asp=1, main="Metrics MDS")

<img width="417" alt="결과" src="https://user-images.githubusercontent.com/87562188/151594239-8306d0a8-4a46-46d3-9db2-14aa34de71b6.png">

text(x, y, rownames(loc), cex=0.7)

 <img width="416" alt="결과" src="https://user-images.githubusercontent.com/87562188/151594483-6c30da29-63be-4816-ba7f-fe5560750c34.png">

abline(v=0, h=0, lty=2, lwd=0.5)

<img width="419" alt="결과" src="https://user-images.githubusercontent.com/87562188/151594630-06e50bd0-9b96-4e51-9a58-7ce4982cbc43.png">

###### 비계량적 MDS(nonmetric MDS)
* 데이터가 순서척도인 경우 활용한다. 개체들간의 거리가 순서로 주어진 경우에는 순서척도를 거리의 속성과 같도록 변환(monotone transformation)하여 거리를 생성한 후 적용한다.

isoMDS사례

* MASS package의 Swiss 자료를 이용하여 2차원으로 도시들을 매핑한다.
* 1888년경의 스위스연방 중 47개의 불어권 주의 토양의 비옥도 지수와 여러 사회경제적 지표를 측정한 자료이다.

R code below

library(MASS)

data(swiss)

swiss.x <- as.matrix(swiss[, -1])

swiss.dist <- dist(swiss.x)

swiss.mds <- isoMDS(swiss.dist)

plot(swiss.mds$points, type="n")

<img width="422" alt="결과" src="https://user-images.githubusercontent.com/87562188/151596112-e577d353-12ca-4594-b119-ca077c328c42.png">

text(swiss.mds$points, labels=as.character(1:nrow(swiss.x)))

<img width="413" alt="결과" src="https://user-images.githubusercontent.com/87562188/151596274-65bf59a4-72e7-439f-a97f-34db40bf0c8e.png">

abline(v=0, h=0, lty=2, lwd=0.5)

<img width="415" alt="결과" src="https://user-images.githubusercontent.com/87562188/151596382-f18843dd-55c8-4688-8e32-1491c335ee70.png">

# 주성분 분석

여러 변수들의 변량을 '주성분(principal Component)'이라는 서로 상관성이 높은 변수들의 선형결합으로 만들어 기존의 상관성이 높은 변수들을 요약, 축소하는 기법이다.
첫 번째 주성분으로 전체 변동을 가장 많이 설명할 수 있도록 하고, 두 번째 주성분으로는 첫 번째 주성분과는 상관성이 없어서(낮아서) 첫 번쨰 주성분이 설명하지 못하는 나머지
변동을 정보의 손실 없이 가장 많이 설명할 수 있도록 변수들의 선형조합을 만든다.

## 주성분 분석 사례

USArrests 자료

* 1973년 미국 50개주의 100,000명의 인구 당 체포된 세 가지 강력범죄수(assault,murder, rape)와 각 주마다 도시에 거주하는 인구의 비율(%)로 구성되어 있다.
* 변수들 간의 척도의 차이가 상당히 크기 떄문에 상관행렬을 사용하여 분석한다.
* 특이치 분해를 사용하는 경우 자료 행렬의 각 변수의 평균과 제곱의 합이 1로 표준화되었다고 가정할 수 있다.

R code below

1. 4개의 변수들 간의 산점도

library(datasets)

data(USArrests)

pairs(USArrests, panel = panel.smooth, main = "USArrests data")

<img width="415" alt="결과" src="https://user-images.githubusercontent.com/87562188/151598381-d7a67952-c560-4097-963c-460b852ac2b4.png">

* Murder와 UrbanPop 비율간의 관련성이 작아 보인다.

2. summary
* 제1주성분과 제2주성분까지의 누적 분산비율은 대략 86.8%로 2개의 주성분 변수를 활용하여 전체 데이터의 86.8%를 설명할 수 있다.
* 주성분들에 의해 설명되는 변동의 비율은 Screeplot을 통해 확인 가능하다.

US.prin <- princomp(USArrests, cor = TRUE)

summary(US.prin)

<img width="476" alt="결과" src="https://user-images.githubusercontent.com/87562188/151598909-23810b3a-5352-4a21-8a95-c8a7b76a14db.png">

screeplot(US.prin, npcs=4, type="lines")

<img width="419" alt="결과" src="https://user-images.githubusercontent.com/87562188/151598967-2c280219-52e3-4728-af23-e2c8b04d32d8.png">

3. Loading
* 네 개의 변수가 각 주성분 Comp.1-Comp.4까지 기여하는 가중치가 제시된다.
* 제1주성분에는 네 개의 변수가 평균적으로 기여한다.
* 제2주성분에서는(Murder,Assault)와(UrbanPop, Rape)의 계수의 부호가 서로 다르다.

loadings(US.prin)

<img width="473" alt="결과" src="https://user-images.githubusercontent.com/87562188/151599578-a708bdd0-da38-44dd-a0a3-1079c3ae1980.png">

4. Scores
* 각 주성분 Comp.1-Comp.4의 선형식을 통해 각 지역(record)별로 얻은 결과를 계산한다.

US.prin$scores

<img width="471" alt="결과" src="https://user-images.githubusercontent.com/87562188/151600039-a729f07c-a2ea-468b-bc8e-fd71eae02414.png">

5. 제 1-2주성분에 의한 행렬도
* 조지아,메릴랜드,뉴 멕시코 등은 폭행과 살인의 비율이 상대적으로 높은 지역이다.
* 미시간, 텍사스 등은 강간의 비율이 높은 지역이다.
* 콜로라도, 캘리포니아, 뉴저지 등은 도시에 거주하는 인구의 비율이 높은 지역이다.
* 아이다호, 뉴 햄프셔, 아이오와 등의 도시들은 도시에 거주하는 인구의 비율이 상대적으로 낮으면서 3대 강력범죄도 낮다.

arrests.pca <- prcomp(USArrests,center = TRUE,scale. = TRUE)

biplot(arrests.pca,scale=0)

<img width="417" alt="결과" src="https://user-images.githubusercontent.com/87562188/151600964-65850c22-ace3-4087-8f6a-55efdf315b26.png">

# 5장. 정형 데이터 마이닝
 데이터 마이닝은 대용량 데이터에서 의미있는 패턴을 파악하거나 예측하여 의사결정에 활용하는 방법이다.
 
## ROCR 패키지로 성과분석

1. ROC Curve(Receiver Operating Characteristic Curve)
 * ROC Curve란 가로축을 FPR(False Positive Rate=1-특이도)값으로 두고, 세로축을 TPR(True Positive Rate, 민감도)값으로 두어 시각화한 그래프이다.
 * 2진 분류(binary classfication)에서 모형의 성능을 평가하기 위해 많이 사용되는 척도이다.
 * 그래프가 왼쪽 상단에 가깝게 그려질수록 올바르게 예측한 비율은 높고, 잘못 예측한 비율은 낮음을 의미한다. 따라서 **ROC곡선 아래의 면적을 의미하는 AUROC(Area Under ROC)**
   값이 크면 클수록(1에 가까울수록) 모형의 성능이 좋다고 평가한다.
   
2. R 실습 코드
* ROCR패키지는 binary classfication만 지원가능

R code below

library(rpart)

library(party)

libarary(ROCR)

x <- kyphosis[sample(1:nrow(kyphosis), nrow(kyphosis), replace=F),]

x.train <- kyphosis[1:floor(nrow(x)*0.75),]

x.evaluate <- kyphosis[floor(nrow(x)*0.75):nrow(x),]

x.model <- cforest(Kyphosis~Age+Number+Start, data=x.train)

x.evaluate$prediction <- predict(x.model, newdata=x.evaluate)

x.evaluate$correct <- x.evaluate$prediction == x.evaluate$Kyphosis

print(paste("% of predicted classfication correct", mean(x.evaluate$correct)))

x.evaluate$probabilities <- 1- unlist(treeresponse(x.model, newdata=x.evaluate), use.names=F)[seq(1,nrow(x.evaluate)*2.2)]

* 그래프1

pred <- prediction(x.evaluate$probabilities, x.evaluate$Kyphosis)

perf <- performance(pred, "tpr", "fpr")

plot(perf, main="ROC curve", colorize=T)

<img width="341" alt="결과" src="https://user-images.githubusercontent.com/87562188/152264415-b47a6968-ac71-4f54-811d-14cbcf946685.png">

* 그래프2

perf <- performance(pred, "lift", "rpp")

plot(perf, main="lift curve", colorize=T)

<img width="342" alt="결과" src="https://user-images.githubusercontent.com/87562188/152264655-db43c3e0-f9b9-4059-8276-c31420689d93.png">

## 이익도표(Lift chart)

1. 이익도표의 개념
* 이익도표는 분류모형의 성능을 평가하기 위한 척도로, 분류된 관측치에 대해 얼마나 예측이 잘 이루어졌는지를 나타내기 위해 임의로 나눈 각 등급별로 반응검출율, 반응률, 리프트
 등의 정보를 산출하여 나타내는 도표이다.
* 2000명의 전체고객 중 381명이 상품을 구매한 경우에 대해 이익도표를 만드는 과정을 예로 들어보면, 먼저 데이터셋의 각 관측치에 대한 예측활용을 내림차순으로 정렬한다. 이후 
 데이터를 10개의 구간으로 나눈 다음 각 구간의 반응율(% response)을 산출한다. 또한 기본 향상도(baseline lift)에 비해 반응률이 몇 배나 높은지를 계산하는데 이것을 향상도(lift)라고 한다.
* 이익도표의 각 등급은 예측확률에 따라 매겨진 순위이기 때문에, 상위 등급에서는 더 높은 반응률을 보이는 것이 좋은 모형이라고 평가할 수 있다.

2. 이익도표의 활용 예시

![결과](https://user-images.githubusercontent.com/87562188/152265244-027d60b7-7deb-46cb-83ec-d9c52e2215e1.jpg)

* 전체 2000명 중 381명이 구매
* Frequency of "buy" : 2000명 중 실제로 구매한 사람
* % Captured Response : 반응검출율 = 해당 등급의 실제 구매자 / 전체 구매자
* % response : 반응률 = 해당 등급의 실제 구매자 / 200명
* Lift : 향상도 = 반응률 / 기본 향상도
  좋은 모델이라면 Lift가 빠른 속도로 감소해야 한다.
 
 ![결과](https://user-images.githubusercontent.com/87562188/152265523-737427cb-f965-410f-9d50-a26d8eab4ec7.jpg)

* 등급별로 향상도가 급격하게 변동할수록 좋은 모형이라고 할 수 있고, 각 등급별로 향상도가 들쭉날쭉하면 좋은 모형이라고 볼 수 없다.

# 분류분석



 


