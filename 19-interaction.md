# Interação

****

O gráfico de interações é usado quando temos ao menos dois fatores. Tem como função identificar visualmente se os fatores apresentam efeito conjunto ou se são independentes

### Conjunto de dados

Um experimento foi realizado com o intuito de avaliar 5 manejos na entrelinha do pomar de laranja Natal e sua influência em relação a linha de plantio. O experimento foi instalado em Delineamento em blocos casualizados com 12 repetições por tratamento em esquema de parcelas subdividida (2 [linha e entrelinha] x 5[ *U. brizantha* (T1),*U. decumbens* (T2), *U. ruziziensis* (T3), *Glifosato* (T4), *Pousio* (T5). Foi analisado o carbono da biomassa microbiana (CBM).


```r
RESP=c(224.92, 180.32, 130.19, 110.31, 163.74,193.03, 211.49, 137.65, 127.15, 203.39,182.36, 124.75, 177.70, 231.01, 202.14,214.89, 198.42, 267.85, 207.67, 176.74,162.18, 124.59, 158.99, 209.12, 128.14,113.95, 215.53, 190.51, 174.58, 148.70,150.90, 209.03, 210.40, 199.03, 237.05,196.97, 176.06, 263.27, 240.19, 160.72,239.90, 188.07, 251.35, 215.45, 198.50,271.42, 226.56, 217.65, 213.69, 101.26,115.41, 140.10, 117.67, 106.45, 139.34,104.22, 206.13, 195.89, 147.11, 122.93,176.55, 173.63, 112.83, 184.82, 178.18,115.85, 183.89, 134.92, 086.49, 103.96,096.33, 091.64, 157.76, 107.45, 106.61,095.28, 152.37, 066.02, 125.75, 075.34,088.64, 104.00, 066.38, 084.74, 101.76,173.70, 101.24, 143.71, 119.88, 157.79,070.42, 152.75, 111.65, 153.08, 146.64,142.57, 098.96, 065.92, 065.62, 063.26,095.72, 084.14, 054.92, 090.49, 112.11,102.68, 144.77, 122.58, 125.14, 127.61,117.14, 147.87, 156.18, 154.82, 183.91,159.11, 155.41, 184.55, 121.39, 155.77)
FATOR1=rep(rep(c("L","EL"), e=12),5); FATOR1=factor(FATOR1)
FATOR2=rep(c(paste("T",1:5)),e=24); FATOR2=factor(FATOR2)
repe=rep(c(paste("R",1:12)),10); repe=factor(repe)
dados = data.frame(FATOR1,FATOR2,repe,RESP)
```

### Fator1 x Fator 2


```r
with(dados, interaction.plot(FATOR1, FATOR2, RESP))
```

![](19-interaction_files/figure-epub3/unnamed-chunk-2-1.png)<!-- -->

### Editando o gráfico


```r
with(dados, interaction.plot(FATOR1, FATOR2, RESP, las=1, col=1:6, bty='l', 
                             ylab='CBM', trace.label="FATOR2"))
```

![](19-interaction_files/figure-epub3/unnamed-chunk-3-1.png)<!-- -->

### Fator2 x Fator 1


```r
with(dados, interaction.plot(FATOR2, FATOR1, RESP))
```

![](19-interaction_files/figure-epub3/unnamed-chunk-4-1.png)<!-- -->

### Editando o gráfico


```r
with(dados, interaction.plot(FATOR2,FATOR1, RESP, las=1, col=c("blue","red"), bty='l',xlab='', ylab='CBM', trace.label="repe"))
```

![](19-interaction_files/figure-epub3/unnamed-chunk-5-1.png)<!-- -->

## Usando o interaction(s)

### Conjunto de dados

Este conjunto de dados pertence ao pacote ExpDes.pt (data6). Ao qual é composto de três fatores (fatorA, fatorB e fatorC), cuja resposta é nomeada como resp.


```r
x=scan(dec=",",text="
1       1      1      1   1 10,0
2       1      1      1   2 10,8
3       1      1      1   3  9,8
4       1      1      2   1 10,3
5       1      1      2   2 11,3
6       1      1      2   3 10,3
7       1      2      1   1  9,7
8       1      2      1   2 10,1
9       1      2      1   3 10,2
10      1      2      2   1  9,4
11      1      2      2   2 11,6
12      1      2      2   3  9,1
13      2      1      1   1  9,2
14      2      1      1   2  8,6
15      2      1      1   3 10,1
16      2      1      2   1  9,3
17      2      1      2   2 10,3
18      2      1      2   3  9,1
19      2      2      1   1 11,5
20      2      2      1   2  9,5
21      2      2      1   3 10,8
22      2      2      2   1 10,7
23      2      2      2   2 10,4
24      2      2      2   3  9,6
")
data=data.frame(t(matrix(x,6,24)))
colnames(data)=c("N","fatorA", "fatorB", "fatorC","rep","resp")
data
```

```
##     N fatorA fatorB fatorC rep resp
## 1   1      1      1      1   1 10.0
## 2   2      1      1      1   2 10.8
## 3   3      1      1      1   3  9.8
## 4   4      1      1      2   1 10.3
## 5   5      1      1      2   2 11.3
## 6   6      1      1      2   3 10.3
## 7   7      1      2      1   1  9.7
## 8   8      1      2      1   2 10.1
## 9   9      1      2      1   3 10.2
## 10 10      1      2      2   1  9.4
## 11 11      1      2      2   2 11.6
## 12 12      1      2      2   3  9.1
## 13 13      2      1      1   1  9.2
## 14 14      2      1      1   2  8.6
## 15 15      2      1      1   3 10.1
## 16 16      2      1      2   1  9.3
## 17 17      2      1      2   2 10.3
## 18 18      2      1      2   3  9.1
## 19 19      2      2      1   1 11.5
## 20 20      2      2      1   2  9.5
## 21 21      2      2      1   3 10.8
## 22 22      2      2      2   1 10.7
## 23 23      2      2      2   2 10.4
## 24 24      2      2      2   3  9.6
```

### Separado por Fator A


```r
par(mfrow=c(1,2))
interaction.plot(data$fatorB[data$fatorA=="1"],
                 data$fatorC[data$fatorA=="1"],
                 data$resp[data$fatorA=="1"])
interaction.plot(data$fatorB[data$fatorA=="2"],
                 data$fatorC[data$fatorA=="2"],
                 data$resp[data$fatorA=="2"])
```

![](19-interaction_files/figure-epub3/unnamed-chunk-7-1.png)<!-- -->

### Alterando escala do eixo Y


```r
par(mfrow=c(1,2))
interaction.plot(data$fatorB[data$fatorA=="1"],
                 data$fatorC[data$fatorA=="1"],
                 data$resp[data$fatorA=="1"], 
                 las=1)
interaction.plot(data$fatorB[data$fatorA=="2"],
                 data$fatorC[data$fatorA=="2"],
                 data$resp[data$fatorA=="2"], 
                 las=1)
```

![](19-interaction_files/figure-epub3/unnamed-chunk-8-1.png)<!-- -->

### Título do eixo x e y


```r
par(mfrow=c(1,2))
interaction.plot(data$fatorB[data$fatorA=="1"],
                 data$fatorC[data$fatorA=="1"],
                 data$resp[data$fatorA=="1"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta")
interaction.plot(data$fatorB[data$fatorA=="2"],
                 data$fatorC[data$fatorA=="2"],
                 data$resp[data$fatorA=="2"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta")
```

![](19-interaction_files/figure-epub3/unnamed-chunk-9-1.png)<!-- -->

### Removendo linhas da caixa


```r
par(mfrow=c(1,2))
interaction.plot(data$fatorB[data$fatorA=="1"],
                 data$fatorC[data$fatorA=="1"],
                 data$resp[data$fatorA=="1"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta",
                 bty="l")
interaction.plot(data$fatorB[data$fatorA=="2"],
                 data$fatorC[data$fatorA=="2"],
                 data$resp[data$fatorA=="2"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta",
                 bty="l")
```

![](19-interaction_files/figure-epub3/unnamed-chunk-10-1.png)<!-- -->

### Cor da linhas


```r
par(mfrow=c(1,2))
interaction.plot(data$fatorB[data$fatorA=="1"],
                 data$fatorC[data$fatorA=="1"],
                 data$resp[data$fatorA=="1"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta",
                 bty="l", 
                 col = c("red","blue"))
interaction.plot(data$fatorB[data$fatorA=="2"],
                 data$fatorC[data$fatorA=="2"],
                 data$resp[data$fatorA=="2"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta",
                 bty="l",
                 col = c("red","blue"))
```

![](19-interaction_files/figure-epub3/unnamed-chunk-11-1.png)<!-- -->

### Título dos gráficos


```r
par(mfrow=c(1,2))
interaction.plot(data$fatorB[data$fatorA=="1"],
                 data$fatorC[data$fatorA=="1"],
                 data$resp[data$fatorA=="1"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta",
                 bty="l", 
                 col = c("red","blue"),
                 main="Fator A = 1")
interaction.plot(data$fatorB[data$fatorA=="2"],
                 data$fatorC[data$fatorA=="2"],
                 data$resp[data$fatorA=="2"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta",
                 bty="l",
                 col = c("red","blue"),
                 main="Fator A = 2")
```

![](19-interaction_files/figure-epub3/unnamed-chunk-12-1.png)<!-- -->

### Título da legenda


```r
par(mfrow=c(1,2))
interaction.plot(data$fatorB[data$fatorA=="1"],
                 data$fatorC[data$fatorA=="1"],
                 data$resp[data$fatorA=="1"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta",
                 bty="l", 
                 col = c("red","blue"),
                 main="Fator A = 1",
                 trace.label = "Fator C")
interaction.plot(data$fatorB[data$fatorA=="2"],
                 data$fatorC[data$fatorA=="2"],
                 data$resp[data$fatorA=="2"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta",
                 bty="l",
                 col = c("red","blue"),
                 main="Fator A = 2",
                 trace.label = "Fator C")
```

![](19-interaction_files/figure-epub3/unnamed-chunk-13-1.png)<!-- -->


### Pontos da média

Calculando as médias


```r
# Média para nível 1 do fator A
media=with(data, 
           tapply(resp[fatorA=="1"], 
                      list(fatorB[fatorA=="1"],
                           fatorC[fatorA=="1"]), 
                  mean))

# Média e desvio-padrão para nível 2 do fator A
media1=with(data, 
            tapply(resp[fatorA=="2"], 
                      list(fatorB[fatorA=="2"],
                           fatorC[fatorA=="2"]), 
                   mean))           
```



```r
par(mfrow=c(1,2))
interaction.plot(data$fatorB[data$fatorA=="1"],
                 data$fatorC[data$fatorA=="1"],
                 data$resp[data$fatorA=="1"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta",
                 bty="l", 
                 col = c("red","blue"),
                 main="Fator A = 1",
                 trace.label = "Fator C")
points(c(1,2,1,2),media, col="red", pch=16)

interaction.plot(data$fatorB[data$fatorA=="2"],
                 data$fatorC[data$fatorA=="2"],
                 data$resp[data$fatorA=="2"], 
                 las=1,
                 xlab="Fator B",
                 ylab="Resposta",
                 bty="l",
                 col = c("red","blue"),
                 main="Fator A = 2",
                 trace.label = "Fator C")
points(c(1,2,1,2),media1, col="red", pch=16)
```

![](19-interaction_files/figure-epub3/unnamed-chunk-15-1.png)<!-- -->

### Barras de desvio-padrão

Calculando os desvios-padrões


```r
# Desvio-padrão para nível 1 do fator A
desvio=with(data, 
            tapply(resp[fatorA=="1"], 
                      list(fatorB[fatorA=="1"],
                           fatorC[fatorA=="1"]), 
                         sd))

# Desvio-padrão para nível 2 do fator A
desvio1=with(data, 
             tapply(resp[fatorA=="2"], 
                      list(fatorB[fatorA=="2"],
                           fatorC[fatorA=="2"]), 
                    sd))
```


```r
par(mfrow=c(1,2))
interaction.plot(data$fatorB[data$fatorA=="1"],
                 data$fatorC[data$fatorA=="1"],
                 data$resp[data$fatorA=="1"], 
                 las=1, args.legend=list(x="topleft"),
                 xlab="Fator B", ylim=c(8,13),
                 ylab="Resposta", 
                 bty="l", 
                 col = c("red","blue"),
                 main="Fator A = 1",
                 trace.label = "Fator C")
```

```
## Warning in plot.window(...): "args.legend" não é um parâmetro gráfico
```

```
## Warning in plot.xy(xy, type, ...): "args.legend" não é um parâmetro gráfico
```

```
## Warning in axis(side = side, at = at, labels = labels, ...): "args.legend" não é
## um parâmetro gráfico

## Warning in axis(side = side, at = at, labels = labels, ...): "args.legend" não é
## um parâmetro gráfico
```

```
## Warning in box(...): "args.legend" não é um parâmetro gráfico
```

```
## Warning in title(...): "args.legend" não é um parâmetro gráfico
```

```
## Warning in axis(1, x, ...): "args.legend" não é um parâmetro gráfico
```

```r
points(c(1,2,1,2),media, col="red", pch=16)
arrows(c(1,2,1,2), media+desvio,c(1,2,1,2),media-desvio, code=3,angle=90,length = 0.1, col=c("red","red","blue","blue"))

interaction.plot(data$fatorB[data$fatorA=="2"],
                 data$fatorC[data$fatorA=="2"],
                 data$resp[data$fatorA=="2"], 
                 las=1,
                 xlab="Fator B", ylim=c(8,13),
                 ylab="Resposta",
                 bty="l",
                 col = c("red","blue"),
                 main="Fator A = 2",
                 trace.label = "Fator C")
points(c(1,2,1,2),media1, col="red", pch=16)
arrows(c(1,2,1,2), media1+desvio1,c(1,2,1,2),media1-desvio1, code=3,angle=90,length = 0.1, col=c("red","red","blue","blue"))
```

![](19-interaction_files/figure-epub3/unnamed-chunk-17-1.png)<!-- -->

## Pacote dae

### Conjunto de dados


```r
resp=c(4599.55,6203.50,4566.02,5616.38,4978.35,5126.15,4816.23,4251.00,4106.79,
       4600.58,4012.14,4623.41,4274.16,4683.50,4433.33,4326.16,4932.66,5066.67,
       4697.29,5011.38,5156.72,4744.21,4826.80,4663.26,4807.19,4377.19,4442.07,
       4685.58,5066.90,5317.66,5144.19,4580.18,4860.37,5204.21,5146.19,5015.67,
       5801.99,4668.05,5393.16,5282.27,5369.41,5494.43,4980.32,5715.76,4754.54,
       5000.83,4664.11,4969.41,5315.43,4872.29,5546.79,4765.79,4649.63,4899.31,
       4890.89,5117.10,4942.97,4548.97,4916.97,4225.38,4820.21,4150.44,4648.46,
       4271.57,5143.54,4808.97,5459.66,4928.35,5224.70,4900.90,4770.88,4977.68,
       5816.80,5107.11,5555.80,5767.65,5117.10,5573.08,5673.87,4859.00,4687.26,
       5055.22,5235.22,4961.72,4984.93,5425.67,4978.33,5172.60,5328.07,4973.87,
       5296.55,4928.01,4528.12,5337.93,5809.20,4914.70,5191.89,5261.24,5287.53,
       5680.55,5080.06,5425.53,4949.13,5300.57,4481.23,5039.54,5223.75,4581.65)
FATOR1=rep(rep(c("A1","A2","A3"), e=12),3)
FATOR2=rep(c("B1","B2","B3"), e=36)
FATOR3=rep(rep(c("C1","c2","c3"),e=4),9)
dados=data.frame(FATOR1,FATOR2,FATOR3,resp)
```

<br>

### Gráfico com a média

Para se construir esse gráfico é necessário instalar o pacote `dae`


```r
library(dae)
```

```
## Carregando pacotes exigidos: ggplot2
```

```r
interaction.ABC.plot(resp,FATOR1,FATOR2,FATOR3,data=dados)
```

![](19-interaction_files/figure-epub3/unnamed-chunk-19-1.png)<!-- -->

```r
interaction.ABC.plot(resp,FATOR1,FATOR3,FATOR2,data=dados)
```

![](19-interaction_files/figure-epub3/unnamed-chunk-19-2.png)<!-- -->

```r
interaction.ABC.plot(resp,FATOR2,FATOR3,FATOR1,data=dados)
```

![](19-interaction_files/figure-epub3/unnamed-chunk-19-3.png)<!-- -->

```r
interaction.ABC.plot(resp,FATOR2,FATOR1,FATOR3,data=dados)
```

![](19-interaction_files/figure-epub3/unnamed-chunk-19-4.png)<!-- -->

```r
interaction.ABC.plot(resp,FATOR3,FATOR2,FATOR1,data=dados)
```

![](19-interaction_files/figure-epub3/unnamed-chunk-19-5.png)<!-- -->

```r
interaction.ABC.plot(resp,FATOR3,FATOR1,FATOR2,data=dados)
```

![](19-interaction_files/figure-epub3/unnamed-chunk-19-6.png)<!-- -->

### Média e desvio-padrão


```r
media=tapply(resp, paste(FATOR1,FATOR2,FATOR3),mean)
desvio=tapply(resp, paste(FATOR1,FATOR2,FATOR3),sd)
```


```r
(F1=rep(c("A1","A2","A3"), e=9))
```

```
##  [1] "A1" "A1" "A1" "A1" "A1" "A1" "A1" "A1" "A1" "A2" "A2" "A2" "A2" "A2" "A2"
## [16] "A2" "A2" "A2" "A3" "A3" "A3" "A3" "A3" "A3" "A3" "A3" "A3"
```

```r
(F2=rep(rep(c("B1","B2","B3"), e=3),3)) 
```

```
##  [1] "B1" "B1" "B1" "B2" "B2" "B2" "B3" "B3" "B3" "B1" "B1" "B1" "B2" "B2" "B2"
## [16] "B3" "B3" "B3" "B1" "B1" "B1" "B2" "B2" "B2" "B3" "B3" "B3"
```

```r
(F3=rep(c("C1","c2","c3"),9))
```

```
##  [1] "C1" "c2" "c3" "C1" "c2" "c3" "C1" "c2" "c3" "C1" "c2" "c3" "C1" "c2" "c3"
## [16] "C1" "c2" "c3" "C1" "c2" "c3" "C1" "c2" "c3" "C1" "c2" "c3"
```

```r
paste(F1,F2,F3) # tratamentos
```

```
##  [1] "A1 B1 C1" "A1 B1 c2" "A1 B1 c3" "A1 B2 C1" "A1 B2 c2" "A1 B2 c3"
##  [7] "A1 B3 C1" "A1 B3 c2" "A1 B3 c3" "A2 B1 C1" "A2 B1 c2" "A2 B1 c3"
## [13] "A2 B2 C1" "A2 B2 c2" "A2 B2 c3" "A2 B3 C1" "A2 B3 c2" "A2 B3 c3"
## [19] "A3 B1 C1" "A3 B1 c2" "A3 B1 c3" "A3 B2 C1" "A3 B2 c2" "A3 B2 c3"
## [25] "A3 B3 C1" "A3 B3 c2" "A3 B3 c3"
```

### Criando uma data.frame


```r
data=data.frame(F1,F2,F3,media,desvio)
```

### Construindo o gráfico


```r
interaction.ABC.plot(media,F1,F2,F3,data=data,
                     ggplotFunc=
                       list(geom_errorbar(data=data,
                                          aes(ymax=media+desvio, 
                                              ymin=media-desvio), 
                                                   width=0.2)))
```

![](19-interaction_files/figure-epub3/unnamed-chunk-23-1.png)<!-- -->

<br><br><br>

****

