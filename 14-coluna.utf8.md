# Gráfico de Colunas 

****

O gráfico em colunas consiste em construir retângulos, em que uma das dimensões é proporcional à magnitude a ser representada ($n_i$ ou $f_i$), sendo a outra arbitrária, porém igual para todas as colunas. Essas colunas são dispostas paralelamente umas às outras de forma vertical.

<br>

Além do título e fonte de referências deve-se observar o seguinte:

- as colunas devem ter todas a mesma largura;
- a distância entre as colunas deve ser constante e de preferência menor que a largura das colunas.

<br><br>


## Conjunto de dados

<br>


```r
tratamentos=rep(c(paste("T",1:5)),e=4)
resposta=c(100,120,110,90,150,145,149,165,150,144,134,139,220,206,210,210,266,249,248,260)
## Média e Desvio-padrão (Por Tratamento)
media=tapply(resposta,tratamentos, mean)
desvio=tapply(resposta,tratamentos,sd)
```

<br>


```r
barplot(media)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-2-1.png)<!-- -->

<br>

## Adicionando melhorias


```r
barplot(media, 
        las=1,
        col="lightyellow",
        ylab="Resposta",
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-3-1.png)<!-- -->

**Comandos**:

las=1: deixar escala do eixo Y na vertical

col="cor": mudar cor das barras (Ex. "red","blue","green" ou gray.colors(quantidade de tonalidades) para escala cinza ou rainbow(quantidade de cores) para escala colorida. Também é possível específicar a cor de cada barra (col=c("red","green","yellow","gray","blue"))).

xlab e ylab: nomear eixo X e Y

xlim e ylim: escala do eixo X e Y

abline(h=0): linha na horizontal em Y=0 (No caso de vertical, abline(v=0)). É possível alterar a cor pela função "col="cor"" e o tracejado pelo "lty=número" (Ver o Help do comando)

<br>

## Barras de desvio-padrão


```r
bar=barplot(media, 
        las=1,
        col="lightyellow",
        ylab="Resposta",
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-4-1.png)<!-- -->

<br>

## Unidade do eixo Y 

(Ex. $Kg\ ha^{-1}$)


```r
bar=barplot(media, 
        las=1,
        col="lightyellow",
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-5-1.png)<!-- -->

<br>

## Média dos tratamentos


```r
bar=barplot(media, 
        las=1,
        col="lightyellow",
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
text(bar,media+desvio+10,media)
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-6-1.png)<!-- -->

<br>

## Separação de casa decimal


```r
options(OutDec=",")
bar=barplot(media, 
        las=1,
        col="lightyellow",
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
text(bar,media+desvio+10,media)
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-7-1.png)<!-- -->



<br>

## Letras do teste de comparação


```r
tukey=c("d","c","c","b","a")
options(OutDec=",")
bar=barplot(media, 
        las=1,
        col="lightyellow",
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
text(bar,media+desvio+10,paste(round(media,0),tukey))
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-9-1.png)<!-- -->

<br><br>

****

## Pacote Agricolae

****

<br>

### Conjunto de dados


```r
tratamentos=rep(c(paste("T",1:5)),e=4)
resposta=c(100,120,110,90,150,145,149,165,150,144,134,139,220,206,210,210,266,249,248,260)
```

<br>

### Modelo de Anova


```r
modelo=aov(resposta~tratamentos)
```


```r
library(agricolae)
a=HSD.test(modelo,"tratamentos", group = T)
```

<br>

### Gráfico com média 


```r
plot(a, las=1)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-13-1.png)<!-- -->

<br>

### Gráfico de barras


```r
bar.group(a$groups, col="lightblue",
          las=1, 
          ylim=c(0,300))
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-14-1.png)<!-- -->

<br>

### Barras de desvio-padrão


```r
bar.err(a$means,
        variation="SD", col="lightblue",
        las=1,
        ylim=c(0,300))
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-15-1.png)<!-- -->

<br>

### Barras de erro padrão


```r
bar.err(a$means,
        variation="SE", col="lightblue",
        las=1,
        ylim=c(0,300))
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-16-1.png)<!-- -->

<br>

### Barras de máximo-mínimo


```r
bar.err(a$means,
        variation="range", col="lightblue",
        las=1,
        ylim=c(0,300))
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-17-1.png)<!-- -->

<br>

### Barras da distância interquartil


```r
bar.err(a$means,
        variation="IQR", col="lightblue",
        las=1,
        ylim=c(0,300))
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-18-1.png)<!-- -->

<br><br><br>

****

## Pacote ggplot2 e ggpubr

****

### Conjunto de dados

Vamos trabalhar com três experimentos em DIC com quatro tratamentos e três repetições cada. 


```r
exp1=c(10,12,13,18,19,16,5,6,5,25,26,28)
exp2=c(9,12,11,18,20,16,7,6,9,25,28,28)
exp3=c(9,12,13,18,22,15,3,6,4,25,30,28)  
Trat=rep(c(paste("T",1:4)),e=3)
dados=data.frame(Trat,exp1,exp2,exp3)
dados$Trat=as.factor(Trat)
```

Obs. Para facilitar, vamos realizar a análise direto pelo pacote ExpDes.pt (é necessário instalar o pacote)

<br>

### Análise de exp1


```r
ExpDes.pt::dic(Trat,exp1)
```

```
## ------------------------------------------------------------------------
## Quadro da analise de variancia
## ------------------------------------------------------------------------
```

```
## Warning in data.matrix(x): NAs introduzidos por coerção
```

```
##            GL     SQ QM     Fc      Pr>Fc
## Tratamento  3 719,58    130,83 3,8864e-07
## Residuo     8  14,67                     
## Total      11 734,25                     
## ------------------------------------------------------------------------
## CV = 8,88 %
## 
## ------------------------------------------------------------------------
## Teste de normalidade dos residuos 
## Valor-p:  0,3563889 
## De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
## ------------------------------------------------------------------------
## 
## ------------------------------------------------------------------------
## Teste de homogeneidade de variancia 
## valor-p:  0,6539247 
## De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
## ------------------------------------------------------------------------
## 
## Teste de Tukey
## ------------------------------------------------------------------------
## Grupos Tratamentos Medias
## a 	 T 4 	 26,33333 
##  b 	 T 2 	 17,66667 
##   c 	 T 1 	 11,66667 
##    d 	 T 3 	 5,333333 
## ------------------------------------------------------------------------
```

<br>

### Análise de exp2


```r
ExpDes.pt::dic(Trat,exp2)
```

```
## ------------------------------------------------------------------------
## Quadro da analise de variancia
## ------------------------------------------------------------------------
```

```
## Warning in data.matrix(x): NAs introduzidos por coerção
```

```
##            GL     SQ QM     Fc      Pr>Fc
## Tratamento  3 684,92    78,276 2,8606e-06
## Residuo     8  23,33                     
## Total      11 708,25                     
## ------------------------------------------------------------------------
## CV = 10,84 %
## 
## ------------------------------------------------------------------------
## Teste de normalidade dos residuos 
## Valor-p:  0,2365244 
## De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
## ------------------------------------------------------------------------
## 
## ------------------------------------------------------------------------
## Teste de homogeneidade de variancia 
## valor-p:  0,9823917 
## De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
## ------------------------------------------------------------------------
## 
## Teste de Tukey
## ------------------------------------------------------------------------
## Grupos Tratamentos Medias
## a 	 T 4 	 27 
##  b 	 T 2 	 18 
##   c 	 T 1 	 10,66667 
##   c 	 T 3 	 7,333333 
## ------------------------------------------------------------------------
```

<br>

### Análise de exp3


```r
ExpDes.pt::dic(Trat,exp3)
```

```
## ------------------------------------------------------------------------
## Quadro da analise de variancia
## ------------------------------------------------------------------------
```

```
## Warning in data.matrix(x): NAs introduzidos por coerção
```

```
##            GL     SQ QM     Fc      Pr>Fc
## Tratamento  3 894,25    47,066 1,9902e-05
## Residuo     8  50,67                     
## Total      11 944,92                     
## ------------------------------------------------------------------------
## CV = 16,32 %
## 
## ------------------------------------------------------------------------
## Teste de normalidade dos residuos 
## Valor-p:  0,9419794 
## De acordo com o teste de Shapiro-Wilk a 5% de significancia, os residuos podem ser considerados normais.
## ------------------------------------------------------------------------
## 
## ------------------------------------------------------------------------
## Teste de homogeneidade de variancia 
## valor-p:  0,7583526 
## De acordo com o teste de bartlett a 5% de significancia, as variancias podem ser consideradas homogeneas.
## ------------------------------------------------------------------------
## 
## Teste de Tukey
## ------------------------------------------------------------------------
## Grupos Tratamentos Medias
## a 	 T 4 	 27,66667 
##  b 	 T 2 	 18,33333 
##   c 	 T 1 	 11,33333 
##    d 	 T 3 	 4,333333 
## ------------------------------------------------------------------------
```

<br>

## Utilizando o *ggplot2*


```r
library(ggplot2)
library(gridExtra)
```

<br>

### Média e desvio-padrão


```r
media=tapply(exp1, Trat, mean)
desvio=tapply(exp1, Trat, sd)
## Construindo uma nova data.frame com a media e desvio
dados1=data.frame(Trat=rownames(media),media,desvio)
```

<br>

### Gráfico básico


```r
ggplot(dados1, 
       aes(x=Trat,y=media))+
  geom_col()
```

![](14-coluna_files/figure-epub3/unnamed-chunk-25-1.png)<!-- -->

### Média no gráfico


```r
ggplot(dados1, 
       aes(x=Trat,y=media))+
  geom_col()+
  geom_text(label=round(media,1), vjust=-1) 
```

![](14-coluna_files/figure-epub3/unnamed-chunk-26-1.png)<!-- -->

```r
# Obs. Round é para arrendondar o valor, neste caso estamos pedindo até a primeira casa decimal
```

<br>

### Letras do teste de comparação


```r
ggplot(dados1, 
       aes(x=Trat,y=media))+
  geom_col()+
  geom_text(label=paste(round(media,1),c("c","b","d","a")), vjust=-1)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-27-1.png)<!-- -->

```r
#Obs. a função paste serve para juntar palavras, nesse caso está juntando cada média com suas respectivas letras do teste de comparação de médias
```

<br>

### Escala do eixo Y


```r
ggplot(dados1, 
       aes(x=Trat,y=media))+
  geom_col()+
  geom_text(label=paste(round(media,1),c("c","b","d","a")), vjust=-1)+
  ylim(c(0,40))
```

![](14-coluna_files/figure-epub3/unnamed-chunk-28-1.png)<!-- -->

<br>

### Cor das colunas


```r
ggplot(dados1, 
       aes(x=Trat,y=media))+
  geom_col(fill=c(1,2,3,4))+
  geom_text(label=paste(round(media,1),c("c","b","d","a")), vjust=-1)+
  ylim(c(0,40))
```

![](14-coluna_files/figure-epub3/unnamed-chunk-29-1.png)<!-- -->

<br>

### Removendo cor de fundo


```r
ggplot(dados1, 
       aes(x=Trat,y=media))+
  geom_col(fill=c(1,2,3,4))+
  geom_text(label=paste(round(media,1),c("c","b","d","a")), vjust=-1)+
  ylim(c(0,40))+
  theme_bw()
```

![](14-coluna_files/figure-epub3/unnamed-chunk-30-1.png)<!-- -->

<br>

### Removendo linhas de grade


```r
ggplot(dados1, 
       aes(x=Trat,y=media))+
  geom_col(fill=c(1,2,3,4))+
  geom_text(label=paste(round(media,1),c("c","b","d","a")), vjust=-1)+
  ylim(c(0,40))+
  theme_bw()+
  theme_classic()
```

![](14-coluna_files/figure-epub3/unnamed-chunk-31-1.png)<!-- -->

<br>

### Nome dos eixos X e Y

**Obs**. A função `expression()` funciona nesses argumentos.


```r
ggplot(dados1, aes(x=Trat,y=media))+
  geom_col(fill=c(1,2,3,4))+
  geom_text(label=paste(round(media,1),c("c","b","d","a")), vjust=-1)+
  ylim(c(0,40))+
  theme_bw()+
  theme_classic()+
  ylab("Resposta")+
  xlab(" ")
```

![](14-coluna_files/figure-epub3/unnamed-chunk-32-1.png)<!-- -->

<br>

### Cor do contorno das colunas


```r
ggplot(dados1, 
       aes(x=Trat,y=media))+
  geom_col(fill=c(1,2,3,4),col="black")+     # Modifiquei aqui
  geom_text(label=paste(round(media,1),c("c","b","d","a")), vjust=-1)+
  ylim(c(0,40))+
  theme_bw()+
  theme_classic()+
  ylab("Resposta")+
  xlab(" ")
```

![](14-coluna_files/figure-epub3/unnamed-chunk-33-1.png)<!-- -->

<br>

### Barras de desvio-padrão


```r
ggplot(dados1, aes(x=Trat,y=media))+
  geom_col(fill=c(1,2,3,4),col="black")+
  geom_text(label=paste(round(media,1),c("c","b","d","a")), vjust=-2)+
  ylim(c(0,40))+
  theme_bw()+
  theme_classic()+
  ylab("Resposta")+
  xlab(" ")+
  geom_errorbar(aes(ymax=media+desvio,ymin=media-desvio), width=0.25) # Width é a largura da barra
```

![](14-coluna_files/figure-epub3/unnamed-chunk-34-1.png)<!-- -->

<br>

### Juntando os gráficos

Obs. Vamos chamar todo o plot de cada uma das variáveis de `a,b,c`, respectivamente. 

<br>

### Variável exp1


```r
media=tapply(exp1, Trat, mean)
desvio=tapply(exp1, Trat, sd)
dados1=data.frame(Trat=rownames(media),media,desvio)
a=ggplot(dados1, aes(x=Trat,y=media))+
  geom_col(fill=c(1,2,3,4),col="black")+
  geom_text(label=paste(round(media,1),
                        c("c","b","d","a")), vjust=-3)+
  ylim(c(0,40))+theme_bw()+theme_classic()+ylab("Resposta")+xlab(" ")+
  geom_errorbar(aes(ymax=media+desvio,
                   ymin=media-desvio), width=0.25)
```

<br>

### Variável exp2


```r
media=tapply(exp2, Trat, mean)
desvio=tapply(exp2, Trat, sd)
dados2=data.frame(Trat=rownames(media),media,desvio)
b=ggplot(dados2, aes(x=Trat,y=media))+
  geom_col(fill=c(1,2,3,4),col="black")+
  geom_text(label=paste(round(media,1),
                        c("c","b","c","a")), vjust=-3)+
  ylim(c(0,40))+theme_bw()+theme_classic()+ylab("Resposta")+xlab(" ")+
  geom_errorbar(aes(ymax=media+desvio,
                   ymin=media-desvio), width=0.25)
```

<br>

### Variável exp3


```r
media=tapply(exp3, Trat, mean)
desvio=tapply(exp3, Trat, sd)
dados3=data.frame(Trat=rownames(media),media,desvio)
c=ggplot(dados3, aes(x=Trat,y=media))+
  geom_col(fill=c(1,2,3,4),col="black")+
  geom_text(label=paste(round(media,1),
                        c("c","b","d","a")), vjust=-4)+
  ylim(c(0,40))+theme_bw()+theme_classic()+ylab("Resposta")+xlab(" ")+
  geom_errorbar(aes(ymax=media+desvio,
                   ymin=media-desvio), width=0.25)
```


```r
grid.arrange(a,b,c,ncol=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-38-1.png)<!-- -->

<br><br>

****

## Pacote ggpubr

****

**Obs.** Existem vários *packages* que utilizam o `ggplot2` e geram saídas similares, contudo, com argumentos dos comandos mais simples.


```r
exp1=c(10,12,13,18,19,16,5,6,5,25,26,28)
exp2=c(9,12,11,18,20,16,7,6,9,25,28,28)
exp3=c(9,12,13,18,22,15,3,6,4,25,30,28)  
Trat=rep(c(paste("T",1:4)),e=3)
dados=data.frame(Trat,exp1,exp2,exp3)
dados$Trat=as.factor(Trat)
```


```r
library(ggpubr)
```

```
## Carregando pacotes exigidos: magrittr
```

```r
library(gridExtra)
```

<br>

### Comando base 


```r
ggbarplot(dados, 
          x = "Trat", 
          y = "exp1",
          add="mean")
```

![](14-coluna_files/figure-epub3/unnamed-chunk-41-1.png)<!-- -->

<br>

### Barras de desvio-padrão


```r
ggbarplot(dados, 
          x = "Trat", 
          y = "exp1",
          add = "mean_sd")
```

![](14-coluna_files/figure-epub3/unnamed-chunk-42-1.png)<!-- -->

<br>

### Cor da coluna 


```r
ggbarplot(dados, 
          x = "Trat", 
          y = "exp1",
          add = "mean_sd", 
          fill = "Trat")
```

![](14-coluna_files/figure-epub3/unnamed-chunk-43-1.png)<!-- -->


```r
ggbarplot(dados, 
          x = "Trat", 
          y = "exp1",
          add = "mean_sd", 
          fill = "Trat",
          palette = c(1,2,3,4))
```

![](14-coluna_files/figure-epub3/unnamed-chunk-44-1.png)<!-- -->

<br>

### Letra do teste de comparação


```r
ggbarplot(dados, 
          x = "Trat", 
          y = "exp1",
          add = "mean_sd", 
          fill = "Trat",
          label = c("c","b","d","a"),
          lab.vjust=-2)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-45-1.png)<!-- -->

<br>

### Adicionando a média


```r
media=tapply(exp1,Trat,mean)
ggbarplot(dados, 
          x = "Trat", 
          y = "exp1",
          add = "mean_sd", 
          fill = "Trat",
          label = paste(round(media,1),c("c","b","c","a")),
          lab.vjust=-2)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-46-1.png)<!-- -->

<br>

### Escala do eixo Y


```r
ggbarplot(dados, 
          x = "Trat", 
          y = "exp1",
          add = "mean_sd", 
          fill = "Trat",
          label = paste(round(media,1),c("c","b","d","a")),
          lab.vjust=-2)+ylim(c(0,40))
```

![](14-coluna_files/figure-epub3/unnamed-chunk-47-1.png)<!-- -->

<br>

### Removendo legenda


```r
ggbarplot(dados, 
          x = "Trat", 
          y = "exp1",
          add = "mean_sd", 
          fill = "Trat",
          label = paste(round(media,1),c("c","b","d","a")),
          lab.vjust=-2,
          legend="n")+ylim(c(0,40))
```

![](14-coluna_files/figure-epub3/unnamed-chunk-48-1.png)<!-- -->

<br>

### Juntando os gráficos

<br>

### Variável exp1


```r
media=tapply(exp1,Trat,mean)
a=ggbarplot(dados, 
          x = "Trat", 
          y = "exp1",
          add = "mean_sd", 
          fill = "Trat",
          label = paste(round(media,1),c("c","b","d","a")),
          lab.vjust=-3,
          legend="n")+ylim(c(0,40))
```

<br>

### Variável exp2


```r
media=tapply(exp2,Trat,mean)
b=ggbarplot(dados, 
          x = "Trat", 
          y = "exp2",
          add = "mean_sd", 
          fill = "Trat",
          label = paste(round(media,1),c("c","b","d","a")),
          lab.vjust=-3,
          legend="n")+ylim(c(0,40))
```

<br>

### Variável exp3


```r
media=tapply(exp3,Trat,mean)
c=ggbarplot(dados, 
          x = "Trat", 
          y = "exp3",
          add = "mean_sd", 
          fill = "Trat",
          label = paste(round(media,1),c("c","b","d","a")),
          lab.vjust=-3,
          legend="n")+ylim(c(0,40))
```


```r
grid.arrange(a,b,c,ncol=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-52-1.png)<!-- -->

<br>

**Como deixar apenas o gráfico a esquerda com a escala de Y?**

Existem casos em que uma mesma variável foi analisada em várias situações e dessa forma, geramos gráficos com a mesma unidade de medida. Nesse sentido, é frequente apresentar apenas uma escala de Y, geralmente o gráfico a esquerda. No pacote ggpubr, podemos efetuar da seguinte forma:

<br>


```r
media=tapply(exp1,Trat,mean)
a=ggbarplot(dados, 
          x = "Trat", 
          y = "exp1",
          add = "mean_sd", 
          fill = "Trat",
          ylab="Resposta",
          label = paste(round(media,1),c("c","b","d","a")),
          lab.vjust=-3,
          legend="n")+ylim(c(0,40))
```

<br>


```r
media=tapply(exp2,Trat,mean)
b=ggbarplot(dados, 
          x = "Trat", 
          y = "exp2",
          add = "mean_sd", 
          fill = "Trat",
          label = paste(round(media,1),c("c","b","c","a")),
          lab.vjust=-3,
          legend="n",
          yscale="n")+
  ylim(c(0,40))+
  theme(axis.text.y=element_blank())+ # Comando para remover os números da escala de Y
  ylab("") # Remover nome do eixo Y 
```

<br>


```r
media=tapply(exp3,Trat,mean)
c=ggbarplot(dados, 
          x = "Trat", 
          y = "exp3",
          add = "mean_sd", 
          fill = "Trat",
          label = paste(round(media,1),c("c","b","d","a")),
          lab.vjust=-4,
          legend="n")+
  ylim(c(0,40))+
  theme(axis.text.y=element_blank())+
  ylab("")
```


```r
grid.arrange(a,b,c,ncol=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-56-1.png)<!-- -->

<br><br><br>

****

## Duas variáveis categóricas

****

<br>

### Conjunto de dados


```r
Fator1=factor(rep(c(paste("F",1:2)),e=20))
Fator2=factor(c(rep(c(paste("T",1:5)),e=4),rep(c(paste("T",1:5)),e=4)))
resposta=c(100,120,110,90,150,145,149,165,250,244,220,239,220,206,210,210,266,249,248,260,110,130,120,100,160,165,169,175,160,154,144,149,230,216,220,220,276,259,258,270)
dados=data.frame(Fator1,Fator2,resposta)
## Média e Desvio-padrão (Por Tratamento)
media=with(dados, tapply(dados$resposta,list(Fator1, Fator2), mean))
desvio=with(dados, tapply(resposta,list(Fator1, Fator2), sd))
```

<br>

### Gráfico simples


```r
barplot(media, beside = T)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-58-1.png)<!-- -->

O argumento beside=T é refente a um gráfico de barras em que as barras são posicionadas lado a lado. Do contrário, as barras serão empilhadas (*stacked*). 

<br>

### Melhorias


```r
barplot(media, beside = T,
        las=1, col=c("lawngreen","gold"),
        ylab="Resposta",
        xlab="Fator2",
        ylim=c(0,300))
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-59-1.png)<!-- -->

**Comandos**:

**las=1**: deixar escala do eixo Y na vertical

**col="cor"**: mudar cor das barras (Ex. "red","blue","green" ou gray.colors(quantidade de tonalidades) para escala cinza ou rainbow(quantidade de cores) para escala colorida. Também é possível específicar a cor de cada barra (col=c("red","green","yellow","gray","blue"))).

**xlab** e **ylab**: nomear eixo X e Y

**xlim** e **ylim**: escala do eixo X e Y

**abline(h=0)**: linha na horizontal em Y=0 (No caso de vertical, abline(v=0)). É possível alterar a cor pela função "col="cor"" e o tracejado pelo "lty=número" (Ver o Help do comando)

<br>

### Cores


```r
barplot(1:21, col=c("red","white","black","lightyellow","green","blue","orange",
                        "yellow","gray","pink","brown","Gainsboro", "Lavender", 
                        "DeepSkyBlue","LawnGreen", "Gold","MediumOrchid",
                        "LightSalmon", "Sienna", "Tomato", "DeepPink1"))
```

![](14-coluna_files/figure-epub3/unnamed-chunk-60-1.png)<!-- -->

<br>

### Barras de desvio-padrão


```r
bar=barplot(media,beside=T, 
        las=1,
        ylab="Resposta",
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-61-1.png)<!-- -->

<br>

### Unidade do eixo Y 

(Ex. $Kg\ ha^{-1}$)


```r
bar=barplot(media, beside=T,
        las=1,
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-62-1.png)<!-- -->

<br>

### Média acima das barras


```r
bar=barplot(media, beside=T,
        las=1,
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
text(bar,media+desvio+10,media, cex=0.8)
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-63-1.png)<!-- -->

<br>

### Separação de casa decimal


```r
options(OutDec=",")
bar=barplot(media, beside=T,
        las=1,
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
text(bar,media+desvio+10,media, cex=0.8)
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-64-1.png)<!-- -->

<br>

### Letras do teste de comparação


```r
tukey=c("dB","dA","cB","cA","cB","cA","bB","bA","aB","aA")
options(OutDec=",")
bar=barplot(media, beside=T,
        las=1,
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
text(bar,media+desvio+10,paste(round(media,0),tukey), cex=0.8)
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-65-1.png)<!-- -->

<br>

### Adicionando legenda

**legend.text=rownames(media)**: adicionar a legenda (neste caso em relação ao Fator 2)

**args.legend**: argumentos da legenda (x="topleft": legenda será adicionada no parte superior esquerda, podemos adicionar superior direito ("topright"), inferior esquerdo ("bottomleft"), inferior direito ("bottomright"), centralizado ("center"))


```r
tukey=c("dB","dA","cB","cA","cB","cA","bB","bA","aB","aA")
options(OutDec=",")
bar=barplot(media, 
            beside=T,
            legend.text = rownames(media),
            args.legend = list(x="topleft", bty="n"),
        las=1,
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,300))
abline(h=0)
text(bar,media+desvio+10,paste(round(media,0),tukey), cex=0.8)
arrows(bar,media+desvio,bar,media-desvio,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-66-1.png)<!-- -->

<br><br><br>

****

## Colunas empilhadas

****

<br>

### Conjunto de dados


```r
Fator1=factor(rep(c(paste("F",1:2)),e=20))
Fator2=factor(c(rep(c(paste("T",1:5)),e=4),rep(c(paste("T",1:5)),e=4)))
resposta=c(100,120,110,90,150,145,149,165,250,244,220,239,220,206,210,
           210,266,249,248,260,110,130,120,100,160,165,169,175,160,154,
           144,149,230,216,220,220,276,259,258,270)
dados=data.frame(Fator1,Fator2,resposta)
## Média e Desvio-padrão (Por Tratamento)
media=with(dados, tapply(dados$resposta,list(Fator1, Fator2), mean))
desvio=with(dados, tapply(resposta,list(Fator1, Fator2), sd))
```

<br>

### Gráfico básico


```r
barplot(media, beside=F)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-68-1.png)<!-- -->

O argumento beside=F é refente a um gráfico de barras em que as barras são posicionadas lado a lado. Do contrário, as barras serão empilhadas (*stacked*). 

<br>

### Melhorias


```r
barplot(media, beside=F,
        las=1, col=c("lawngreen","gold"),
        ylab="Resposta",
        xlab="Fator2",
        ylim=c(0,600))
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-69-1.png)<!-- -->

**Comandos**:

**las=1**: deixar escala do eixo Y na vertical

**col="cor"**: mudar cor das barras (Ex. "red","blue","green" ou gray.colors(quantidade de tonalidades) para escala cinza ou rainbow(quantidade de cores) para escala colorida. Também é possível específicar a cor de cada barra (col=c("red","green","yellow","gray","blue"))).

**xlab** e **ylab**: nomear eixo X e Y

**xlim** e **ylim**: escala do eixo X e Y

**abline(h=0)**: linha na horizontal em Y=0 (No caso de vertical, abline(v=0)). É possível alterar a cor pela função "col="cor"" e o tracejado pelo "lty=número" (Ver o Help do comando)

### Barras de desvio-padrão


```r
bar=barplot(media,beside=F, 
        las=1,col=c("lawngreen","gold"),
        ylab="Resposta",
        xlab="Tratamentos",
        ylim=c(0,600))
abline(h=0)
arrows(bar,media[1,]+desvio[1,],bar,media[1,]-desvio[1,],length = 0.1,angle=90,code=3)
arrows(bar,media[1,]+media[2,]+desvio[2,],bar,media[1,]+media[2,]-desvio[2,],length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-70-1.png)<!-- -->

<br>

### Unidade do eixo Y 

(Ex. $Kg\ ha^{-1}$)


```r
bar=barplot(media, beside=F,
        las=1,col=c("lawngreen","gold"),
        ylab=expression(Resposta~~(kg~ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,600))
abline(h=0)
arrows(bar,media[1,]+desvio[1,],bar,media[1,]-desvio[1,],length = 0.1,angle=90,code=3)
arrows(bar,media[1,]+media[2,]+desvio[2,],bar,media[1,]+media[2,]-desvio[2,],length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-71-1.png)<!-- -->

### Média acima das barras


```r
bar=barplot(media, beside=F,
        las=1,col=c("lawngreen","gold"),
        ylab=expression(Resposta~~(kg~ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,600))
abline(h=0)
text(bar,media[1,]+desvio[1,]+20,media[1,], cex=0.8)
text(bar,media[1,]+media[2,]+desvio[2,]+20,media[2,], cex=0.8)
arrows(bar,media[1,]+desvio[1,],bar,media[1,]-desvio[1,],length = 0.1,angle=90,code=3)
arrows(bar,media[1,]+media[2,]+desvio[2,],bar,media[1,]+media[2,]-desvio[2,],length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-72-1.png)<!-- -->

<br>

### Separação de casa decimal


```r
options(OutDec=",")
bar=barplot(media, beside=F,
        las=1,col=c("lawngreen","gold"),
        ylab=expression(Resposta~~(kg~ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,600))
abline(h=0)
text(bar,media[1,]+desvio[1,]+20,media[1,], cex=0.8)
text(bar,media[1,]+media[2,]+desvio[2,]+20,media[2,], cex=0.8)
arrows(bar,media[1,]+desvio[1,],bar,media[1,]-desvio[1,],length = 0.1,angle=90,code=3)
arrows(bar,media[1,]+media[2,]+desvio[2,],bar,media[1,]+media[2,]-desvio[2,],length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-73-1.png)<!-- -->

<br>

### Letras do teste de comparação 


```r
tukey=c("dB","dA","cB","cA","cB","cA","bB","bA","aB","aA")
options(OutDec=",")
bar=barplot(media, beside=F,
        las=1,col=c("lawngreen","gold"),
        ylab=expression(Resposta~~(kg~ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,600))
abline(h=0)
text(bar,media[1,]+desvio[1,]+20,paste(media[1,], tukey[c(1,3,6,7,9)]), cex=0.8)
text(bar,media[1,]+media[2,]+desvio[2,]+20,paste(media[2,], tukey[c(2,4,6,8,10)]), cex=0.8)
arrows(bar,media[1,]+desvio[1,],bar,media[1,]-desvio[1,],length = 0.1,angle=90,code=3)
arrows(bar,media[1,]+media[2,]+desvio[2,],bar,media[1,]+media[2,]-desvio[2,],length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-74-1.png)<!-- -->

<br>

### Adicionando legenda

**legend.text=rownames(media)**: adicionar a legenda (neste caso em relação ao Fator 2)

**args.legend**: argumentos da legenda (x="topleft": legenda será adicionada no parte superior esquerda, podemos adicionar superior direito ("topright"), inferior esquerdo ("bottomleft"), inferior direito ("bottomright"), centralizado ("center"))


```r
tukey=c("dB","dA","cB","cA","cB","cA","bB","bA","aB","aA")
options(OutDec=",")
bar=barplot(media, 
            beside=F,
            legend.text = rownames(media),
            args.legend = list(x="topleft", bty="n"),
        las=1,col=c("lawngreen","gold"),
        ylab=expression(Resposta~(kg~ha^-1)),
        xlab="Tratamentos",
        ylim=c(0,600))
abline(h=0)
text(bar,media[1,]+desvio[1,]+20,paste(media[1,], tukey[c(1,3,6,7,9)]), cex=0.8)
text(bar,media[1,]+media[2,]+desvio[2,]+20,paste(media[2,], tukey[c(2,4,6,8,10)]), cex=0.8)
arrows(bar,media[1,]+desvio[1,],bar,media[1,]-desvio[1,],length = 0.1,angle=90,code=3)
arrows(bar,media[1,]+media[2,]+desvio[2,],bar,media[1,]+media[2,]-desvio[2,],length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-75-1.png)<!-- -->

<br><br><br>

****

## Dois lados com escala positiva

****

<br>

### Conjunto de dados


```r
trat=rep(c("T1","T2","T3","T4","T5"),e=3)
mspa=c(8,10,12,18,20,22,28,30,32,38,40,42,48,50,52)
msr=c(14,15,16,19,20,21,24,25,26,29,30,31,34,35,36)
```

<br>

### Média e desvio-padrão


```r
m1=tapply(mspa, trat, mean)
m2=tapply(msr, trat, mean)
sd1=tapply(mspa, trat, sd)
sd2=tapply(msr, trat, sd)
```


```r
# alterando margem e configurando para dois plots um abaixo do outro
op <- list(mfrow = c(2,1),
          oma = c(5,4,0,0) + 0.1,
          mar = c(0,0,0,1))
```

<br>

### Somente colunas

**Obs.** Nesse caso em específico, estamos querendo que ambas as variáveis assumem respostas positivas. Todavia, queremo a coluna da variável MSPA acima e MSR abaixo. 


```r
par(op)
b1=barplot(m1, 
           axes=F, 
           col="blue",
           ylim=c(0,60),
           axisnames = F,
           las=1)
b2=barplot(m2, 
           axes=F,
           col="red",
           ylim=c(60,0),
           las=1)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-79-1.png)<!-- -->

<br>

### Escala do eixo Y


```r
par(op)
b1=barplot(m1, 
           axes=F, 
           col="blue",
           ylim=c(0,60),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
b1=barplot(m2, 
           axes=F,
           col="red",
           ylim=c(60,0),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-80-1.png)<!-- -->

<br>

### Barras de desvio-padrão


```r
par(op)
b1=barplot(m1, 
           axes=F, 
           col="blue",
           ylim=c(0,60),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
arrows(b1,m1+sd1,b1,m1-sd1,angle = 90,code=3, length = 0.05)
b2=barplot(m2, 
           axes=F,
           col="red",
           ylim=c(60,0),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
arrows(b2,m2+sd2,b2,m2-sd2,angle = 90,code=3, length = 0.05)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-81-1.png)<!-- -->

<br>

### Linha em 0 e título de Y


```r
par(op)
b1=barplot(m1, 
           axes=F, 
           col="blue",
           ylim=c(0,60),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
arrows(b1,m1+sd1,b1,m1-sd1,angle = 90,code=3, length = 0.05)
b2=barplot(m2, 
           axes=F,
           col="red",
           ylim=c(60,0),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
title(ylab = "Resposta",outer=T, line = 3)
arrows(b2,m2+sd2,b2,m2-sd2,angle = 90,code=3, length = 0.05)
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-82-1.png)<!-- -->

<br>

### Título para MS (g)


```r
par(op)
b1=barplot(m1, 
           axes=F, 
           col="blue",
           ylim=c(0,60),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
arrows(b1,m1+sd1,b1,m1-sd1,angle = 90,code=3, length = 0.05)
b2=barplot(m2, 
           axes=F,
           col="red",
           ylim=c(60,0),
#           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
title(ylab = expression(MS~(g)),outer=T, line = 3)
arrows(b2,m2+sd2,b2,m2-sd2,angle = 90,code=3, length = 0.05)
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-83-1.png)<!-- -->

<br>

### Coluna hachurada


```r
par(op)
b1=barplot(m1, 
           axes=F, 
           col="blue",
           density = 40,
           ylim=c(0,60),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
arrows(b1,m1+sd1,b1,m1-sd1,angle = 90,code=3, length = 0.05)
b2=barplot(m2, 
           axes=F,
           col="red",
           ylim=c(60,0),
           density = 20,
#           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
title(ylab = expression(MS~(g)),outer=T, line = 3)
arrows(b2,m2+sd2,b2,m2-sd2,angle = 90,code=3, length = 0.05)
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-84-1.png)<!-- -->

<br>

### Adicionando legenda


```r
par(op)
b1=barplot(m1, 
           axes=F, 
           col="blue",
           density = 40,
           ylim=c(0,60),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
arrows(b1,m1+sd1,b1,m1-sd1,angle = 90,code=3, length = 0.05)
legend("topleft",
       fill=c("blue","red"),
       legend=c("MSPA","MSR"),
       density = c(40,20),
       bty="n")
b2=barplot(m2, 
           axes=F,
           col="red",
           ylim=c(60,0),
           density = 20,
#           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
title(ylab = expression(MS~(g)),outer=T, line = 3)
arrows(b2,m2+sd2,b2,m2-sd2,angle = 90,code=3, length = 0.05)
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-85-1.png)<!-- -->

<br>

### Teste de comparação


```r
par(op)
b1=barplot(m1, 
           axes=F, 
           col="blue",
           density = 40,
           ylim=c(0,60),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
arrows(b1,m1+sd1,b1,m1-sd1,angle = 90,code=3, length = 0.05)
legend("topleft",
       fill=c("blue","red"),
       legend=c("MSPA","MSR"),
       density = c(40,20),
       bty="n")
text(b1,m1+sd1+5,c("e","d","c","b","a"))
b2=barplot(m2, 
           axes=F,
           col="red",
           ylim=c(60,0),
           density = 20,
#           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
text(b2,m2+sd2+5,c("e","d","c","b","a"))
title(ylab = expression(MS~(g)),outer=T, line = 3)
arrows(b2,m2+sd2,b2,m2-sd2,angle = 90,code=3, length = 0.05)
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-86-1.png)<!-- -->

<br>

### Mudando fonte 


```r
par(family="serif")
par(op)
b1=barplot(m1, 
           axes=F, 
           col="blue",
           density = 40,
           ylim=c(0,60),
           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
arrows(b1,m1+sd1,b1,m1-sd1,angle = 90,code=3, length = 0.05)
legend("topleft",
       fill=c("blue","red"),
       legend=c("MSPA","MSR"),
       density = c(40,20),
       bty="n")
text(b1,m1+sd1+5,c("e","d","c","b","a"))
b2=barplot(m2, 
           axes=F,
           col="red",
           ylim=c(60,0),
           density = 20,
#           axisnames = F,
           las=1)
axis(2,seq(0,50,10),las=1)
text(b2,m2+sd2+5,c("e","d","c","b","a"))
title(ylab = expression(MS~(g)),outer=T, line = 3)
arrows(b2,m2+sd2,b2,m2-sd2,angle = 90,code=3, length = 0.05)
abline(h=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-87-1.png)<!-- -->

<br><br><br>

****

# Gráfico de Barras

****

<br>

O gráfico em barras consiste em construir retângulos, em que uma das dimensões é proporcional à magnitude a ser representada ($n_i$ ou $f_i$), sendo a outra arbitrária, porém igual para todas as barras. Essas colunas são dispostas paralelamente umas às outras de forma horizontal.

Além do título e fonte de referências deve-se observar o seguinte:

- as barras devem ter todas a mesma largura;
- a distância entre as barras deve ser constante e de preferência menor que a largura das barras.

<br>

### Conjunto de dados


```r
tratamentos=rep(c(paste("T",1:5)),e=4)
resposta=c(100,120,110,90,150,145,149,165,150,144,134,139,220,206,210,210,266,249,248,260)
## Média e Desvio-padrão (Por Tratamento)
media=tapply(resposta,tratamentos, mean)
desvio=tapply(resposta,tratamentos,sd)
```

<br>

### Gráfico básico


```r
barplot(media, horiz = T)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-89-1.png)<!-- -->

<br>

### Melhorias


```r
barplot(media, horiz = T, 
        las=1,
        col="lightyellow",
        ylab="Resposta",
        xlab="Tratamentos",
        xlim=c(0,300))
abline(v=0)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-90-1.png)<!-- -->

<br>

### Barras de desvio-padrão


```r
bar=barplot(media, 
        las=1,horiz = T,
        col="lightyellow",
        ylab="Resposta",
        xlab="Tratamentos",
        xlim=c(0,300))
abline(v=0)
arrows(media+desvio,bar,media-desvio,bar,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-91-1.png)<!-- -->

<br>

### Unidade do eixo Y 

(Ex. $Kg\ ha^{-1}$)


```r
bar=barplot(media, 
        las=1,horiz = T,
        col="lightyellow",
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        xlim=c(0,300))
abline(v=0)
arrows(media+desvio,bar,media-desvio,bar,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-92-1.png)<!-- -->

<br>

### Média acima das barras


```r
bar=barplot(media, 
        las=1,horiz = T,
        col="lightyellow",
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        xlim=c(0,300))
abline(v=0)
text(media+desvio+20,bar,media)
arrows(media+desvio,bar,media-desvio,bar,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-93-1.png)<!-- -->

<br>

### Separação de casa decimal


```r
options(OutDec=",")
bar=barplot(media, 
        las=1,horiz = T,
        col="lightyellow",
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        xlim=c(0,300))
abline(v=0)
text(media+desvio+20,bar,media)
arrows(media+desvio,bar,media-desvio,bar,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-94-1.png)<!-- -->

<br>

### Letras do teste de comparação 


```r
tukey=c("d","c","c","b","a")
options(OutDec=",")
bar=barplot(media, 
        las=1,horiz = T,
        col="lightyellow",
        ylab=expression("Resposta"*" "*(kg*" "*ha^-1)),
        xlab="Tratamentos",
        xlim=c(0,300))
abline(v=0)
text(media+desvio+20,bar,paste(round(media,0),tukey))
arrows(media+desvio,bar,media-desvio,bar,length = 0.1,angle=90,code=3)
```

![](14-coluna_files/figure-epub3/unnamed-chunk-95-1.png)<!-- -->

<br><br><br>