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

