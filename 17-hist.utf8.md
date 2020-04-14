# Histograma

****

Histograma é uma representação gráfica (um gráfico de barras verticais ou barras horizontais) da distribuição de frequências de um conjunto de dados quantitativos contínuos. O histograma pode ser um gráfico por valores absolutos ou frequência relativa ou densidade. No caso de densidade, a frequência relativa do intervalo $i$, ($fr_i$), é representada pela área de um retângulo que é colocado acima do ponto médio da classe  i. Consequentemente, a área total do histograma (igual a soma das áreas de todos os retângulos) será igual a 1. Assim, ao construir o histograma, cada retângulo deverá ter área proporcional à frequência relativa (ou à frequência absoluta, o que é indiferente) correspondente. No caso em que os intervalos são de tamanhos (amplitudes) iguais, as alturas dos retângulos serão iguais às frequências relativas (ou iguais às frequências absolutas) dos intervalos correspondentes.

<br>

### Conjunto de dados


```r
tratamentos=rep(c(paste("T",1:5)),e=8)
resposta=c(100,170,160,90,150,145,179,165,180,144,184,139,220,206,187,210,166,235,220,190,100,120,110,190,140,145,149,165,150,144,134,139,188,206,190,140,166,224,148,160)
data=data.frame(tratamentos, resposta)
```

### Gráfico básico


```r
hist(resposta)
```

![](17-hist_files/figure-epub3/unnamed-chunk-2-1.png)<!-- -->

<br>

### Melhorias


```r
hist(resposta, 
        las=1,
        col="lightyellow",
        ylab="Frequência",
        xlab="Resposta",
        ylim=c(0,10),
        main="Histograma")
abline(h=0)
```

![](17-hist_files/figure-epub3/unnamed-chunk-3-1.png)<!-- -->

**Comandos**:

las=1: deixar escala do eixo Y na vertical

col="cor": mudar cor das barras (Ex. "red","blue","green" ou gray.colors(quantidade de tonalidades) para escala cinza ou rainbow(quantidade de cores) para escala colorida. Também é possível específicar a cor de cada barra (col=c("red","green","yellow","gray","blue"))).

xlab e ylab: nomear eixo X e Y

xlim e ylim: escala do eixo X e Y

main: Título

abline(h=0): linha na horizontal em Y=0 (No caso de vertical, abline(v=0)). É possível alterar a cor pela função "col="cor"" e o tracejado pelo "lty=número" (Ver o Help do comando)

<br>

### Plotando curva normal


```r
histograma=hist(resposta, 
        las=1,
        col="lightyellow",
        ylab="Frequência",
        xlab="Resposta",
        ylim=c(0,10),
        main="Histograma")
abline(h=0)

## Criando sequência de dados quantitativos discretos entre o mínimo e o máximo da resposta
xfit<-seq(min(resposta),max(resposta))

## dnorm (Função para encontrar os possíveis valores para Y e suas densidade de probabilidade)
yfit<-dnorm(xfit,mean=mean(resposta),sd=sd(resposta))

## diff é o comando para diferença e length para comprimento
yfit <- yfit*diff(histograma$mids[1:2])*length(resposta)

## Plotando linha da curva normal
lines(xfit, yfit, col="blue", lwd=2)
```

![](17-hist_files/figure-epub3/unnamed-chunk-4-1.png)<!-- -->

<br>

****

## Pacote ggplot2

****

<br>

instalar pacote ggplot2:

``install.packages("ggplot2")``


```r
# Carregar pacote
library(ggplot2)

# Obs. Não esquecer de criar uma data.frame (Ex. chamei de data no início do material)

# Criar histograma
mean=mean(resposta);sd= sd(resposta);n=length(resposta); largura=20
ggplot(data, aes(data$resposta))+
  geom_histogram(binwidth = 20, col="red", fill="green")+
  labs(title="Histograma")+
  labs(x="Resposta", y="Frequência")+
stat_function(fun = function(x) dnorm(x, mean = mean, sd = sd) * n * largura,
    color = "red", size = 1)
```

![](17-hist_files/figure-epub3/unnamed-chunk-5-1.png)<!-- -->

**binwidth** = largura de caixa

**col**= cor do contorno das caixas

**fill**= cor do interior das caixas

**Comando para plotar a curva normal:**

stat_function(fun = function(x) dnorm(x, mean = mean, sd = sd) \* n \* lagura,color = "red", size = 1)

<br><br>

****

## Distribuição normal padrão (Z)

****

### Simulando dados


```r
x=seq(-3,3,length=400)
y=dnorm(x,0,1)
```

<br>

### gráfico simples


```r
plot(x,
     y,
     type="l",
     xlab="",
     ylim=c(-0.1,0.5),
     ylab="")
```

![](17-hist_files/figure-epub3/unnamed-chunk-7-1.png)<!-- -->

<br>

### Removendo marca da escala


```r
plot(x,y,type="l",axes=F,xlab="",ylim=c(-0.1,0.5),
     ylab="")
```

![](17-hist_files/figure-epub3/unnamed-chunk-8-1.png)<!-- -->

<br>

### Preenchimento tracejado


```r
plot(x,y,type="l",axes=F,xlab="",ylim=c(-0.1,0.5),
     ylab="",col="white")
polygon(c(-3,x,3),c(0,y,0),density = 30)
```

![](17-hist_files/figure-epub3/unnamed-chunk-9-1.png)<!-- -->

<br>

### Valor crítico (90%)


```r
plot(x,y,type="l",axes=F,xlab="",ylim=c(-0.1,0.5),
     ylab="",col="white")
polygon(c(-3,x,3),c(0,y,0),density = 30)
x1=seq(-1.645,1.645,length=100) # 90
y1=dnorm(x1)
polygon(c(-1.645,x1,1.645),c(0,y1,0),col="white")
abline(h=0);
lines(x=c(0,0),y=c(0,max(y)),lty=2)
```

![](17-hist_files/figure-epub3/unnamed-chunk-10-1.png)<!-- -->

<br>

### Valor crítico (95%)


```r
plot(x,y,type="l",axes=F,xlab="",ylim=c(-0.1,0.5),
     ylab="",col="white")
polygon(c(-3,x,3),c(0,y,0),density = 30)
x1=seq(-1.96,1.96,length=100) # 95%
y1=dnorm(x1)
polygon(c(-1.96,x1,1.96),c(0,y1,0),col="white")
abline(h=0);
lines(x=c(0,0),y=c(0,max(y)),lty=2)
```

![](17-hist_files/figure-epub3/unnamed-chunk-11-1.png)<!-- -->

<br>

### Valor crítico (99%)


```r
plot(x,y,type="l",axes=F,xlab="",ylim=c(-0.1,0.5),
     ylab="",col="white")
polygon(c(-3,x,3),c(0,y,0),density = 30)
x1=seq(-2.575,2.575,length=100) # 99
y1=dnorm(x1)
polygon(c(-2.575,x1,2.575),c(0,y1,0),col="white")
abline(h=0);
lines(x=c(0,0),y=c(0,max(y)),lty=2)
```

![](17-hist_files/figure-epub3/unnamed-chunk-12-1.png)<!-- -->

<br>

### Adicionando legendas


```r
plot(x,y,type="l",axes=F,xlab="",ylim=c(-0.1,0.5),
     ylab="",col="white")
polygon(c(-3,x,3),c(0,y,0),density = 30)
x1=seq(-1.96,1.96,length=100)
y1=dnorm(x1)
polygon(c(-1.96,x1,1.96),c(0,y1,0),col="white")
abline(h=0);
lines(x=c(0,0),y=c(0,max(y)),lty=2)
text(-1.96,-.05,expression(frac(-Z,(alpha/2))))
text(+1.96,-.05,expression(frac(Z,(alpha/2))))
text(-2.5,0.1,expression(frac(alpha,2)))
text(+2.5,0.1,expression(frac(alpha,2)))
axis(1)
```

![](17-hist_files/figure-epub3/unnamed-chunk-13-1.png)<!-- -->

<br><br><br>

****

