# ggplot2

****

*Em construção*

<br>

****

### Como juntar vários gráficos do ggplot2

****

No tutorial abaixo apresentamos uma das formas de juntar vários gráficos do ggplot2 em uma única figura. 

**Obs.**: Estamos usando o gráfico de colunas como exemplo, todavia, esses mesmos comandos funcionam para todos os gráficos do *ggplot2* e de outros pacotes que utilizam o *ggplot2*.

#### Conjunto de dados

Vamos trabalhar com três experimentos em DIC com quatro tratamentos e três repetições cada. 


```r
exp1=c(10,12,13,18,19,16,5,6,5,25,26,28)
exp2=c(9,12,11,18,20,16,7,6,9,25,28,28)
exp3=c(9,12,13,18,22,15,3,6,4,25,30,28)  
Trat=rep(c(paste("T",1:4)),e=3)
dados=data.frame(Trat,exp1,exp2,exp3)
dados$Trat=as.factor(Trat)
```

### Juntando três gráficos do ggplot2

*Obs* Para edição do gráfico ver tutorial sobre gráfico de colunas usando o ggplot2


```r
library(ggplot2)
m1=tapply(exp1, Trat, mean);d1=tapply(exp1, Trat, sd)
dados1=data.frame(Trat=rownames(m1),m1,d1)
a=ggplot(dados1, aes(x=Trat,y=m1))+geom_col()+theme_bw()+
  geom_errorbar(aes(ymax=m1+d1, ymin=m1-d1), width=0.25)
m2=tapply(exp2, Trat, mean);d2=tapply(exp2, Trat, sd)
dados2=data.frame(Trat=rownames(m2),m2,d2)
b=ggplot(dados2, aes(x=Trat,y=m2))+geom_col()+theme_bw()+
  geom_errorbar(aes(ymax=m2+d2,ymin=m2-d2), width=0.25)
m3=tapply(exp3, Trat, mean);d3=tapply(exp3, Trat, sd)
dados3=data.frame(Trat=rownames(m3),m3,d3)
c=ggplot(dados3, aes(x=Trat,y=m3))+geom_col()+theme_bw()+
  geom_errorbar(aes(ymax=m3+d3,ymin=m3-d3),width=0.25)
```

### Gráficos lado a lado


```r
library(gridExtra)
grid.arrange(a,b,c,ncol=3)
```

<img src="30-ggplot2_files/figure-html/unnamed-chunk-3-1.png" width="672" />

### Gráficos um abaixo do outro


```r
library(gridExtra)
grid.arrange(a,b,c,ncol=1)
```

<img src="30-ggplot2_files/figure-html/unnamed-chunk-4-1.png" width="672" />

### Dois na primeira linha e uma no lado esquerdo da segunda linha


```r
library(gridExtra)
grid.arrange(a,b,c,ncol=2)
```

<img src="30-ggplot2_files/figure-html/unnamed-chunk-5-1.png" width="672" />

### Dois na primeira linha e uma centralizado na segunda linha


```r
library(gridExtra)
grid.arrange(a,b,c,
             layout_matrix = rbind(c(1,1,2,2), c(NA,3,3,NA)))
```

<img src="30-ggplot2_files/figure-html/unnamed-chunk-6-1.png" width="672" />

### Dois na primeira linha e uma a direita na segunda linha

<br>


```r
library(gridExtra)
grid.arrange(a,b,c,
             layout_matrix = rbind(c(1,1,2,2), c(NA,NA,3,3)))
```

<img src="30-ggplot2_files/figure-html/unnamed-chunk-7-1.png" width="672" />

<br><br><br>

