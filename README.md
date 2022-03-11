
# Habon_plots

<!-- badges: start -->
<!-- badges: end -->

The goal of Habon_plots is to ...
Keep a record of changes committed to plot scripts

library(ggplot2)
library(lubridate)
library(dplyr)
library(patchwork)
library(hrbrthemes)
Alex<- read.csv(file= "Bowdoin_Alex.csv", header= TRUE, sep= ",")
Alex
Alex$Date <- as.POSIXct(Alex$Date, format = "%m/%d/%Y %H:%M")

tiff(file= "Bowdoin_Alex.tiff", units = "in", width = 12, height = 8, res =800)
Bowdoin_Alex<-ggplot(data = Alex, aes (x= Date, y = A_L))+ geom_point(color = "#00AFBB", size = 4)+ 
  labs(x = "Date", y = "Alexandrium cell density (cells/L)")+ 
  scale_x_datetime("", date_labels = "%b-%d", date_breaks= "2 days")+theme(axis.text.x=element_text(angle=60, hjust=1))+theme(axis.text.x=element_text(angle=60, hjust=1)) +scale_y_continuous(limits= c(0,2000)) + theme(axis.line = element_line(size = 0.7, 
                                                                                                                                                                                                                                                   linetype = "solid"), panel.background = element_rect(fill = "white")) + theme(axis.ticks = element_line(colour = "black"), 
                                                                                                                                                                                                                                                                                                                                 axis.title = element_text(size = 17, ), axis.text = element_text(family = "serif", 
                                                                                                                                                                                                                                                                                                                                                                                                  size = 14), axis.text.y = element_text(family = "serif", 
                                                                                                                                                                                                                                                                                                                                                                                                                                         size = 17), plot.title = element_text(size = 17)) + theme(axis.ticks = element_line(size = 1), 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   axis.title = element_text(size = 19), 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   axis.text = element_text(size = 19, colour = "black"), 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   axis.text.x = element_text(family = "serif", 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              size = 19), axis.text.y = element_text(size = 19))
Bowdoin_Alex
dev.off()

Alex_T<- ggplot(Alex, aes(x=Date, y=A_L, shape=Tide, color=Tide, size=Tide, na.rm= TRUE)) +
  geom_point()+
  scale_shape_manual(values=c(19, 17, 1, 18))+ 
  scale_color_manual(values=c('black','darkorchid4', 'black', 'darkorchid4'))+
  scale_size_manual(values=c(4,4,4,4)) +theme(axis.line = element_line (size = 0.6, 
                                                                        linetype = "solid"), axis.title = element_text(size = 19), 
                                              axis.text = element_text(size = 19), 
                                              panel.background = element_rect(fill = "white")) + scale_y_continuous(limits= c(0,1000), name="Alexandrium (cells/L)") + scale_x_datetime(date_labels = "%b-%d", date_breaks =  "1 day")+theme(axis.text.x=element_text(angle=60, hjust=1))

Alex_Tide<- Alex_T+theme(axis.ticks = element_line(size = 1), 
                         axis.title = element_text(size = 19), 
                         axis.text = element_text(size = 19, colour = "black"), 
                         axis.text.x = element_text(family = "serif", 
                                                    size = 19), axis.text.y = element_text(size = 19))
Alex_Tide
dev.off()

#Plotting dinophysis acuminata and norvegica

Dino<- read.csv(file= "Bowdoin_Dino.csv", header= TRUE, sep= ",")
Dino
Dino$Date <- as.POSIXct(Dino$Date, format = "%m/%d/%Y %H:%M")

tiff(file= "Bowdoin_Dino.tiff", units = "in", width = 12, height = 8, res =800)
Dino_C<-ggplot(Dino, aes(x=Date)) +geom_point(aes(y=DA_L),size = 5, shape = 17, col = "#009E73")+ 
  geom_point(aes(y=DN_L),  size = 5, col = "#D55E00") +
  scale_y_continuous(limits= c(0,5000), name="Dinophysis cell density (cell/L)") +
  theme(
    axis.title.y.left=element_text(color="black"),
    axis.text.y.left=element_text(color="black"))+ scale_x_datetime("", date_labels = "%b-%d", date_breaks= "2 days")+theme(axis.text.x=element_text(angle=60, hjust=1))
Dino_CA<- Dino_C + theme(axis.ticks = element_line(size = 1), 
                         axis.title = element_text(size = 19), 
                         axis.text = element_text(size = 19, colour = "black"), 
                         axis.text.x = element_text(family = "serif", 
                                                    size = 19), axis.text.y = element_text(size = 19))
Bowdoin_Dino<- Dino_CA + theme(axis.line = element_line (size = 0.6, 
                                                         linetype = "solid"), axis.title = element_text(size = 19), 
                               axis.text = element_text(size = 19), 
                               panel.background = element_rect(fill = "white"))
Bowdoin_Dino
dev.off()
