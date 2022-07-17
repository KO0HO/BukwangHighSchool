# -
실습파일
부광고등학교 실습파일입니다.
rm(list = ls())

# 패키지 설치

install.packages("dplyr") 
install.packages("ggplot2")
install.packages("lubridate")
install.packages("gridExtra")

# 패키지 이용하기

library(dplyr)
library(ggplot2)
library(lubridate)
library(gridExtra)

# 간단하게 따라하기 -------- ppt page 39 ~ 

x <-3 ; x # 숫자형 데이터
as.character(x) # 문자형 데이터로 바꾸기 
# 다른점은?! ""(따음표 표시안에 들어있음)

# 변수를 할당 할 때 x <- 3과 x = 3은 같은 의미입니다.

y = statistics # 에러가 뜬다
y = "statistics"; y # 문자형은 따음표 안 넣고 변수에 지정한다.

# 사칙 연산 
3+5; 3*5 ; 3-5 ; 3/5
cat(3+5, 3-5, 3*5)

A = 10000
sqrt(10000)
sqrt(A); A/10
V1 = c(1,2,3,10,-5); V2 = c(-1, -2, 0.8, 1/2, 1000)
V1 + 3
sqrt(V2) # 음수에 루트를 씌우면 NaN :(잘못된 입력으로 인해 계산을 할 수 없음을 나타내는 기호이다.)
V2[3] # V2의 세번째 값
V1[c(3,4)] # V1의 세번째 4번째 값

# 직접 데이터 입력

dat1 = data.frame(label = c("Sam", "Tom", "Mia"),
                  height = c(179, 182, 160),
                  sex = c("M","M","F"))
# 데이터 확인하기
View(dat1)
head(dat1)

# $을 이용하여 변수다루기

A = dat1$label ; B = dat1$height

mean(B) # mean(평균)
summary(dat1$sex) 

# 수치 자료 

B

# 범주형 자료
dat1$sex # 성별

# 내장 데이터를 이용하여 실습하기
# Mtcars : 1974 Motor Trend US Megazine 에 수록된 차량과 차량에 관련된 수치들이 기록된 자료이다.

mtcars

head(mtcars) # 앞에서 6개 자료 확인
tail(mtcars) # 뒤에서 6개 자료 확인

# 원형그래프
pie(table(mtcars$cyl),col = rainbow(3, s = 0.2), labels = c("4개","8개","6개"))
pie(table(mtcars$gear), labels = c("3개","5개","6개"))

# 다른 방법으로 원형그래프 만들기
# 1. 표 만들기
table(mtcars$gear) # 범주형 자료를 수치화 시킴

gear = c(15/ (15+12+5), 12/(15+12+5), 5/ (15+12+5) )
names(gear) = c("gear = 3", "gear = 4", "gear = 5")
gear

# 2. 원형그래프 만들기
pie(gear, radius = 1) # radius = 원의 크기

# 부가적으로! 만약 연속형 자료를 table()로 한다면?
table(mtcars$mpg) # 잘 적합이 되지 않는다.

# 만약 R 함수(명령)을 잘 모르겠다? help 함수 사용!
# example

help(pie)



# 막대그래프 만들기
barplot(dat1$height, ylim = c(0,200))
barplot(dat1$height, ylab = "height" , names.arg = dat1$label, col = rainbow(3, s = 0.2), ylim = c(0,200))

# mtcars 데이터를 이용해 배기량 막대그래프 그리기
barplot(mtcars$disp[1:10], xlab = "차량종류", ylab = "배기량", col = rainbow(length(mtcars), s= 0.2),
        legend.text = rownames(mtcars)[1:10] ) # disp = 배기량

# 산점도 만들기
plot(x = mtcars$wt, y = mtcars$mpg, xlab = "wt" , ylab = "mpg", 	main = "wt vs mpg (산점도)", 
     cex = 1.5, col = "blue", pch = 8) 
# cex : 점의 크기, pch = 점의 모양


hist(mtcars$mpg, breaks = 10)
hist(mtcars$mpg) # 연비가 어떤 분포를 가지는지 알 수 있다.

# 부록 연습하기
death <- c(2, 1, 2, 4, 2, 5, 3, 3, 5, 6, 3, 8, 3, 3, 6, 3, 6, 5, 3, 5, 2, 6, 2, 3, 4, 3, 2, 9, 2, 2, 3, 2, 7, 3, 2,
           10, 6, 2, 3, 1, 2, 3, 3, 4, 3, 2, 6, 2, 2, 3, 2, 3, 4, 3, 2, 3, 5, 2, 5, 5, 3, 4, 3, 6, 2, 1, 2, 3, 2, 6,
           3, 3, 6, 3, 2, 3, 6, 4, 6, 5, 3, 5, 6, 2, 6, 3, 2, 3, 2, 6, 2, 6, 3, 3, 2, 6, 9, 6, 3, 6, 6, 2, 3, 2, 3,
           5, 3, 5, 2, 3, 2, 3, 3, 1, 3, 3, 2, 3, 3, 4, 3, 6, 6, 3, 3, 3, 2, 3, 3, 6)
table(death)
freq.table = table(death) # 도수분포표

# 막대그래프
barplot(height = freq.table)
barplot(height = freq.table, col = 4, main = "사망원인에 대한 막대그래프",
        ylab = "빈도수", xlab = "사망원인")

cause <- c("감염성 질환", "각종 암", "순환기 질환", "호흡기 질환", "소화기 질환",
         "각종 사고사", "비뇨기 질환", "정신병", "노환", "신경계 질환")
barplot(height = freq.table, col = rainbow(10, s = 0.2), main = "사망원인에 대한 막대그래프",  
        ylab = "빈도수", xlab = "사망원인", 
        legend.text = cause,
          args.legend = list(x = "topright"))

pie(freq.table, label = cause, main = "사망원인에 대한 원형그래프", cex = 0.7)

# 실습 ------------------------
# 데이터 불러오기 --------------------

# 복사된 작업 공간: C:\Users\pc\Desktop\stat_practice

# setwd() 작업공간 설정하는 함수
# setwd("작업공간") # 이때 작업공간 복사 붙여넣기 시, \ -> \\ 로 바꾸거나, \ -> / 로 바꾸기

getwd()

setwd("C:\\Users\\pc\\Desktop\\stat_practice") # 작업공간 설정하기 


getwd() # 작업 공간 확인하기

dir() # 작업 할 수 있는 데이터 확인하기

data = read.csv(file = "한국환경공단_도로 재비산먼지 측정 정보_20220630.csv") # 데이터 지정하기

head(data) # 데이터 확인 하기

tail(data)

View(head(data)) # 데이터 확인 2  
# dust <- read.csv('C:/Users/INHA/Desktop/bugwang/data.csv')

dust = data



c('매우좋음'='#ff6600',
  '좋음'='#002955',
  '보통'='#074ca1',
  '나쁨'='#7c0022',
  '매우나쁨'='#131230') -> palette

# pie chart
total <- dust %>% group_by(오염범례) %>% summarise(count=n()) %>% mutate(pct=count/sum(count))
total <- total[c(3,5,4,1,2),]

incheon <- dust %>% filter(지역 == "인천" ) %>% group_by(오염범례) %>% summarise(count=n()) %>% mutate(pct=count/sum(count))
incheon <- incheon[c(3,5,4,1,2),]
seoul <- dust %>% filter(지역 == "서울" ) %>% group_by(오염범례) %>% summarise(count=n()) %>% mutate(pct=count/sum(count))
seoul <- seoul[c(2,4,3,1),]

a <- ggplot(total, aes(x="", y=pct, fill=오염범례)) +
  geom_bar(stat="identity", width=1) +
  coord_polar("y", start=0) +
  ggtitle('전국')+
  scale_fill_manual(values=palette) 


b <- ggplot(seoul, aes(x="", y=pct, fill=오염범례)) +
  geom_bar(stat="identity", width=1) +
  coord_polar("y", start=0) +
  ggtitle('서울')+
  scale_fill_manual(values=palette) 


c <- ggplot(incheon, aes(x="", y=pct, fill=오염범례)) +
  geom_bar(stat="identity", width=1) +
  coord_polar("y", start=0) +
  ggtitle('인천')+
  scale_fill_manual(values=palette) 

grid.arrange(a,b,c, nrow=1, ncol=3)

# flip

dust %>%  group_by(지역) %>% summarise(n=n()) # 서울 경기, 인천 지역 데이터 충분함

# 지역별 오염범례 비교
region_dust <- dust %>% 
  filter(지역 %in% c('경기','서울','인천')) %>% 
  group_by(지역, 오염범례) %>% 
  summarise(n=n()) %>% 
  mutate(top_groub=sum(n)) %>% 
  mutate(pct=round(n/top_groub*100,2))

# 전국 오염 범례
total_dust <- dust %>% 
  group_by(오염범례) %>% 
  summarise(n=n()) %>% 
  mutate(top_groub=sum(n)) %>% 
  mutate(pct=round(n/top_groub*100,2))

# 데이터 연결
total_dust ['지역']='전국'
dust_tabel <- rbind(total_dust, region_dust)

dust_tabel$오염범례 <- factor(dust_tabel$오염범례, level = c('매우좋음', '좋음','보통','나쁨','매우나쁨'))

ggplot(data=dust_tabel, aes(x = 지역, y = pct, fill = 오염범례)) +
  geom_col() +
  coord_flip()

# 소주제 2 기온과 습도는 미세먼지 농도에 영향을 줄까 -----------------------------

sample$지역 %>% table()

data1 = data %>% filter(지역 %in% c("경기","인천","서울"))
data2 = data1 %>% select(기온,습도,재비산먼지.평균농도,오염범례)

# 데이터 확인하기
head(data2)

par(mfrow = c(1,1)) 
# Eda
plot(data2$기온, data2$습도, cex = 1,
     xlab = "기온", ylab = "습도", main = "기온 vs 습도")

plot(data2$습도, data2$재비산먼지.평균농도, cex = 1,
     xlab = "습도", ylab = "평균 농도", main = "습도 vs 평균 농도")

# 두개의 산점도에서 전부 관계성이 모호함

# 관계성이 있다는 것은 이러한 유형의 자료입니다.
x = mtcars$hp
y = mtcars$qsec
plot(x, y,xlab = "hp", ylab = "qsec")
abline(lm(y~x), col = "blue", lwd = 2)



dev.off()


# 시각화 1
# x 기온, y 농도, 점의 색 = 습도로 표시
ggplot(data = data2 , aes(x = 기온, y = 재비산먼지.평균농도, col = 습도 )) + # 축 설정하기 
  labs(title = "온도와 농도 비교하기", x = "기온", y = "미세먼지 농도") +
  theme(plot.title = element_text(hjust = 0.5),
        axis.text.x = element_text(size = 15), # x 축 변수 크기 
        axis.title.x = element_text(size = 20), # x 축 제목 크기
        axis.text.y = element_text(size = 15),  # y 축 변수 크기
        axis.title.y = element_text(size = 20))+ # y 축 제목 크기
  geom_point() + # 산점도로 그리기
   ylim(0,500)

# 시각화 2
ggplot(data = data2 , aes(x = 습도, y = 재비산먼지.평균농도, col = 기온 )) +
  labs(title = "습도와 농도 비교하기", x = "습도", y = "미세먼지 농도") +
  theme(plot.title = element_text(hjust = 0.5),
        axis.text.x = element_text(size = 15), # x 축 변수 크기 
        axis.title.x = element_text(size = 20), # x 축 제목 크기
        axis.text.y = element_text(size = 15),  # y 축 변수 크기
        axis.title.y = element_text(size = 20))+ # y 축 제목 크기
  geom_point() + # 산점도로 그리기
  ylim(0,500)
# 시각화1, 시각화2에서 모두 관계성이 크게 들어나보이지는 않는다.

# 결론 연속적인 데이터로 보았을때는 어떠한 관계가 있어보이지는 않는다.

# 그럼 좀 더 세분화 되게 확인해보자!

# 오염범례와 비교하기
ggplot(data = data2 , aes(x = 기온, y = 습도, col = 오염범례))+
  labs(title = "기온 습도 비교하기", x = "기온", y = "습도") +
  theme(plot.title = element_text(hjust = 0.5),
        axis.text.x = element_text(size = 15), # x 축 변수 크기 
        axis.title.x = element_text(size = 20), # x 축 제목 크기
        axis.text.y = element_text(size = 15),  # y 축 변수 크기
        axis.title.y = element_text(size = 20))+ # y 축 제목 크기
  geom_point()



tab = table(data2$오염범례)
tab = tab[c(3,5,4,1,2)]
tab
# 매우좋음이 너무나도 많아 알아 보기가 힘들다.

# 따라서 순차적으로 어떠한 분포를 보이는지 알고자 한다!
data2 %>% filter(오염범례 != "매우좋음")

plot1 = ggplot(data = data2 %>% filter(오염범례 != "매우좋음") , aes(x = 기온, y = 습도, col = 오염범례))+
  labs(title = " ", x = "기온", y = "습도") +
  theme(plot.title = element_text(hjust = 0.5),
        axis.text.x = element_text(size = 15), # x 축 변수 크기 
        axis.title.x = element_text(size = 20), # x 축 제목 크기
        axis.text.y = element_text(size = 15),  # y 축 변수 크기
        axis.title.y = element_text(size = 20))+ # y 축 제목 크기
  geom_point() + 
  xlim(20,35) +
  ylim(30,100)

plot1 # 확인하기

plot2 =ggplot(data = data2 %>% filter(오염범례 == "좋음") , aes(x = 기온, y = 습도, col = 오염범례))+
  labs(title = "좋음", x = "기온", y = "습도") +
  theme(plot.title = element_text(hjust = 0.5),
        axis.text.x = element_text(size = 15), # x 축 변수 크기 
        axis.title.x = element_text(size = 20), # x 축 제목 크기
        axis.text.y = element_text(size = 15),  # y 축 변수 크기
        axis.title.y = element_text(size = 20))+ # y 축 제목 크기
  geom_point() +
  xlim(20,35) +
  ylim(30,100)

plot2 # 확인하기

plot3 =ggplot(data = data2 %>% filter(오염범례 == "보통") , aes(x = 기온, y = 습도, col = 오염범례))+
  labs(title = "보통 ", x = "기온", y = "습도") +
  theme(plot.title = element_text(hjust = 0.5),
        axis.text.x = element_text(size = 15), # x 축 변수 크기 
        axis.title.x = element_text(size = 20), # x 축 제목 크기
        axis.text.y = element_text(size = 15),  # y 축 변수 크기
        axis.title.y = element_text(size = 20))+ # y 축 제목 크기
  geom_point() +
  xlim(20,35) +
  ylim(30,100)

plot3 # 확인하기

plot4 =ggplot(data = data2 %>% filter(오염범례 == "나쁨") , aes(x = 기온, y = 습도, col = 오염범례))+
  labs(title = "나쁨 ", x = "기온", y = "습도") +
  theme(plot.title = element_text(hjust = 0.5),
        axis.text.x = element_text(size = 15), # x 축 변수 크기 
        axis.title.x = element_text(size = 20), # x 축 제목 크기
        axis.text.y = element_text(size = 15),  # y 축 변수 크기
        axis.title.y = element_text(size = 20))+ # y 축 제목 크기
  geom_point() +
  xlim(20,35) +
  ylim(30,100)

plot4 

plot5 =ggplot(data = data2 %>% filter(오염범례 == "매우나쁨") , aes(x = 기온, y = 습도, col = 오염범례))+
  labs(title = "매우나쁨 ", x = "기온", y = "습도") +
  theme(plot.title = element_text(hjust = 0.5),
        axis.text.x = element_text(size = 15), # x 축 변수 크기 
        axis.title.x = element_text(size = 20), # x 축 제목 크기
        axis.text.y = element_text(size = 15),  # y 축 변수 크기
        axis.title.y = element_text(size = 20))+ # y 축 제목 크기
  geom_point() +
  xlim(20,35) +
  ylim(30,100)

plot5

x11()
grid.arrange(plot1,plot2,plot3,plot4,plot5, nrow=2, ncol=3)
# 어떠한 관계성이 있다고 결론짓기 힘들다. 









# 번외 -----------------
# 학생들 그냥 돌려보시고 확인하세요 ~~~~ ppt에는 없는 자료입니다.


# 통계량으로 확인하기

# 평균으로 확인하기 
data2 = data %>% filter(지역 %in% c("서울","경기","인천"))

tmp_info = data2 %>% group_by(오염범례) %>% summarise(temp_information = mean(기온)) %>% as.data.frame()
hum_info= data2 %>% group_by(오염범례) %>% summarise(humidity_information = mean(습도)) %>% as.data.frame()

barplot(tmp_info$temp_information)
barplot(hum_info$humidity_information)

data2 %>% group_by(오염범례) %>% summarise(count = n())

# 상관계수로 확인하기
cor(data2 %>% select(기온,습도,재비산먼지.평균농도))

# 연속형 자료 -> 범주형 자료로 만들기
data2$기온 %>% boxplot() # histogram과 같이 보여주는 그래프
data2$기온 %>% hist()
data2$기온 %>% summary()

data2$습도 %>% boxplot() # histogram과 같이 보여주는 그래프
data2$습도 %>% summary()
data2$재비산먼지.평균농도 %>% summary()

tmp = data2$기온
humidity = data2$습도


# 연속형 자료를 기준으로 자른 후에 범주형 자료로 변환하기!


data2$기온_info = ifelse(tmp <= 24, 0, 
                       ifelse(tmp <= 25, 1, 
                              ifelse(tmp <= 27, 2, 3)))

data2$습도_info = ifelse(humidity <= 55, 0, 
                       ifelse(humidity <= 66, 1, 
                              ifelse(humidity <= 82, 2, 3)))

data2$농도_info = ifelse(data2$재비산먼지.평균농도 <= 11, 0, 
                       ifelse(data2$재비산먼지.평균농도 <= 19, 1, 
                              ifelse(data2$재비산먼지.평균농도 <= 40, 2, 3)))


data2$기온_info = data2$기온_info %>% as.factor()
data2$습도_info = data2$습도_info %>% as.factor()
data2$농도_info = data2$농도_info %>% as.factor()


# 시각화 2 변형 (기온을 범주형 자료로 변환하여 확인 한 것)
ggplot(data = data2 , aes(x = 습도, y = 재비산먼지.평균농도, col = 기온_info )) +
  geom_point() +
  ylim(0,500)


# 그래도 어떠한 경향이 있어보이지는 않는다.


hour_info = paste(data1$측정일자, data1$측정시간, sep = " ") %>% lubridate::hour()
wday_info = paste(data1$측정일자, data1$측정시간, sep = " ") %>% lubridate::wday(label = T)

data1$hour = hour_info
data1$요일 = wday_info

data1 %>% head()
hour_info %>% unique() %>% sort()


aaaaa = data1 %>% group_by(hour) %>% summarise(mean_info = mean(재비산먼지.평균농도))

plot(aaaaa$hour, aaaaa$mean_info, type = "l", xlab = "시간", ylab = "미세먼지 농도도")

bbbbb = data1 %>% group_by(요일) %>% summarise(mean_info = mean(재비산먼지.평균농도))

barplot(bbbbb$mean_info, names.arg = bbbbb$요일, col = rainbow(5,s =.2)) # 막대그래프

# 시간에 경과를 알려주는 그래프는 선 그래프가 좋음

plot(bbbbb$mean_info, type = "l", xlab = "요일", ylab ="평균 농도", main = "요일에 따른 미세먼지 농도 그래프프")


