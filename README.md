# ADsP
Donghun's private repo

# Fundamental statistics analysis 기초 통계 분석
data(mtcars)                      # datasets 패키지의 "mtcars"라는 데이터셋의 마일(mpg), 총마력(hp)의 상관관계 분석을 실시한다
a <- mtcars$mpg                   # a에 mpg칼럼의 값들을 저장
b <- mtcars$hp                    # b에 hp칼럼의 값들을 저장
cor(a,b)                          # correlation(상관계수) 구하기 
cov(a,b)                          # covarience(공분산) 구하기
cor.test(a, b, method="pearson")  # cor.test를 이용하여, mpg와 hp의 상관관계 분석을 실행한 결과

![결과](file:///C:/Users/hanco/OneDrive/%EB%B0%94%ED%83%95%20%ED%99%94%EB%A9%B4/KakaoTalk_20220124_112609904.jpg)
