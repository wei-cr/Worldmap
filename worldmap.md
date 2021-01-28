```bash
#更新R
install.packages("installr") 
library(installr) 
updateR(fast=TRUE,cran_mirror="https://mirrors.ustc.edu.cn/CRAN/") 
# 修改镜像
options(repos="https://mirrors.ustc.edu.cn/CRAN/")
# bioconductor
source("http://bioconductor.org/biocLite.R")
options(BioC_mirror="http://mirrors.ustc.edu.cn/bioc/")

mydata<-read.csv("D:\\1.csv",header=TRUE)
visit.x<-mydata$Longitude
visit.y<-mydata$Latitude  #数据准备
library(ggplot2)
library(ggmap)
library(sp)
library(maptools)
library(maps) #导入需要的按照包，如果没有相关的包可通过install.packages("xxx")获得
mp<-NULL #定义一个空的地图
mapworld<-borders("world",colour = "gray50",fill="white") #绘制基本地图
mp<-ggplot()+mapworld+ylim(-60,90) #利用ggplot呈现，同时地图纵坐标范围从-60到90
mp2<-mp+geom_point(aes(x=visit.x,y=visit.y,size=mydata$number),color="darkorange")+scale_size(range=c(2,9))+ggtitle("plot name")+theme(plot.title=element_text(size=25,color="red",face="italic"))+theme_grey(base_size = 32)  
#绘制带点的地图，geom_point是在地图上绘制点，x轴为经度信息，y轴为纬度信息，size是将点的大小按照收集的个数确定，color为暗桔色，scale_size是将点变大一些,ggtitle是添加标题，theme是改变标题大小、颜色和字体类型,theme_grey调节坐标轴字体大小
mp3<-mp2+theme(legend.position = "none") #将图例去掉
mp3 #将地图呈现出来
```