---
layout: post
title: "R语言按分钟统计weekday 的转化"
date: 2014-02-11 17:16
comments: true
categories: statistics
tags: [r,statistics]
---


```r
all0 <- read.csv("~/sem1/booking_path/week0_min",header=T)
all1 <- read.csv("~/sem1/booking_path/week1_min",header=T)
all2 <- read.csv("~/sem1/booking_path/week2_min",header=T)
all3 <- read.csv("~/sem1/booking_path/week3_min",header=T)
all4 <- read.csv("~/sem1/booking_path/week4_min",header=T)
all5 <- read.csv("~/sem1/booking_path/week5_min",header=T)
all6 <- read.csv("~/sem1/booking_path/week6_min",header=T)

order0 <- read.csv("~/sem1/booking_path/week0_min_order",header=T)
order1 <- read.csv("~/sem1/booking_path/week1_min_order",header=T)
order2 <- read.csv("~/sem1/booking_path/week2_min_order",header=T)
order3 <- read.csv("~/sem1/booking_path/week3_min_order",header=T)
order4 <- read.csv("~/sem1/booking_path/week4_min_order",header=T)
order5 <- read.csv("~/sem1/booking_path/week5_min_order",header=T)
order6 <- read.csv("~/sem1/booking_path/week6_min_order",header=T)

colnames(cvr0) <- c('time','count')
colnames(cvr1) <- c('time','count')
colnames(cvr2) <- c('time','count')
colnames(cvr3) <- c('time','count')
colnames(cvr4) <- c('time','count')
colnames(cvr5) <- c('time','count')
colnames(cvr6) <- c('time','count')

colnames(all0) <- c('time','count')
colnames(all1) <- c('time','count')
colnames(all2) <- c('time','count')
colnames(all3) <- c('time','count')
colnames(all4) <- c('time','count')
colnames(all5) <- c('time','count')
colnames(all6) <- c('time','count')

colnames(order0) <- c('time','count')
colnames(order1) <- c('time','count')
colnames(order2) <- c('time','count')
colnames(order3) <- c('time','count')
colnames(order4) <- c('time','count')
colnames(order5) <- c('time','count')
colnames(order6) <- c('time','count')


cvr0 <-  all0
cvr0$count <- order0$count / all0$count

cvr1 <-  all1
cvr1$count <- order1$count / all1$count

cvr2 <-  all2
cvr2$count <- order2$count / all2$count

cvr3 <-  all3
cvr3$count <- order3$count / all3$count

cvr4 <-  all4
cvr4$count <- order4$count / all4$count

cvr5 <-  all5
cvr5$count <- order5$count / all5$count

cvr6 <-  all6
cvr6$count <- order6$count / all6$count

require(ggplot2)
p_all_0 = ggplot(all0,aes(x=time,y=count)) +geom_point()
p_all_1 = ggplot(all1,aes(x=time,y=count)) +geom_point()
p_all_2 = ggplot(all2,aes(x=time,y=count)) +geom_point()
p_all_3 = ggplot(all3,aes(x=time,y=count)) +geom_point()
p_all_4 = ggplot(all4,aes(x=time,y=count)) +geom_point()
p_all_5 = ggplot(all5,aes(x=time,y=count)) +geom_point()
p_all_6 = ggplot(all6,aes(x=time,y=count)) +geom_point()

p_order_0 = ggplot(order0,aes(x=time,y=count)) +geom_point()
p_order_1 = ggplot(order1,aes(x=time,y=count)) +geom_point()
p_order_2 = ggplot(order2,aes(x=time,y=count)) +geom_point()
p_order_3 = ggplot(order3,aes(x=time,y=count)) +geom_point()
p_order_4 = ggplot(order4,aes(x=time,y=count)) +geom_point()
p_order_5 = ggplot(order5,aes(x=time,y=count)) +geom_point()
p_order_6 = ggplot(order6,aes(x=time,y=count)) +geom_point()

p_cvr_0 = ggplot(cvr0,aes(x=time,y=count)) +geom_point()
p_cvr_1 = ggplot(cvr1,aes(x=time,y=count)) +geom_point()
p_cvr_2 = ggplot(cvr2,aes(x=time,y=count)) +geom_point()
p_cvr_3 = ggplot(cvr3,aes(x=time,y=count)) +geom_point()
p_cvr_4 = ggplot(cvr4,aes(x=time,y=count)) +geom_point()
p_cvr_5 = ggplot(cvr5,aes(x=time,y=count)) +geom_point()
p_cvr_6 = ggplot(cvr6,aes(x=time,y=count)) +geom_point()


ggsave(p_all_0, filename="/tmp/p_all_0.png",width=50,limitsize=F)
ggsave(p_all_1, filename="/tmp/p_all_1.png",width=50,limitsize=F)
ggsave(p_all_2, filename="/tmp/p_all_2.png",width=50,limitsize=F)
ggsave(p_all_3, filename="/tmp/p_all_3.png",width=50,limitsize=F)
ggsave(p_all_4, filename="/tmp/p_all_4.png",width=50,limitsize=F)
ggsave(p_all_5, filename="/tmp/p_all_5.png",width=50,limitsize=F)
ggsave(p_all_6, filename="/tmp/p_all_6.png",width=50,limitsize=F)

ggsave(p_cvr_0, filename="/tmp/p_cvr_0.png",width=50,limitsize=F)
ggsave(p_cvr_1, filename="/tmp/p_cvr_1.png",width=50,limitsize=F)
ggsave(p_cvr_2, filename="/tmp/p_cvr_2.png",width=50,limitsize=F)
ggsave(p_cvr_3, filename="/tmp/p_cvr_3.png",width=50,limitsize=F)
ggsave(p_cvr_4, filename="/tmp/p_cvr_4.png",width=50,limitsize=F)
ggsave(p_cvr_5, filename="/tmp/p_cvr_5.png",width=50,limitsize=F)
ggsave(p_cvr_6, filename="/tmp/p_cvr_6.png",width=50,limitsize=F)

ggsave(p_order_0, filename="/tmp/p_order_0.png",width=50,limitsize=F)
ggsave(p_order_1, filename="/tmp/p_order_1.png",width=50,limitsize=F)
ggsave(p_order_2, filename="/tmp/p_order_2.png",width=50,limitsize=F)
ggsave(p_order_3, filename="/tmp/p_order_3.png",width=50,limitsize=F)
ggsave(p_order_4, filename="/tmp/p_order_4.png",width=50,limitsize=F)
ggsave(p_order_5, filename="/tmp/p_order_5.png",width=50,limitsize=F)
ggsave(p_order_6, filename="/tmp/p_order_6.png",width=50,limitsize=F)

```