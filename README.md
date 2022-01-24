# hello-world
Donghun's private repo

# ADsP
data(mtcars)                      # datasets 패키지의 "mtcars"라는 데이터셋의 마일(mpg), 총마력(hp)의 상관관계 분석을 실시한다
a <- mtcars$mpg                   # a에 mpg칼럼의 값들을 저장
b <- mtcars$hp                    # b에 hp칼럼의 값들을 저장
cor(a,b)                          # correlation(상관계수) 구하기 
cov(a,b)                          # covarience(공분산) 구하기
cor.test(a, b, method="pearson")  # cor.test를 이용하여, mpg와 hp의 상관관계 분석을 실행한 결과

![결과](file:///C:/Users/hanco/OneDrive/%EB%B0%94%ED%83%95%20%ED%99%94%EB%A9%B4/KakaoTalk_20220124_112609904.jpg)

###### 결과의 p-value = 1.788e-07이 유의수준 0.05보다 작다의 의미는 무엇일까?
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
