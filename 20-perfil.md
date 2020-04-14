# Perfil Individual

****

### Conjunto de dados

Um experimento foi realizado com o intuito de avaliar 5 manejos na entrelinha do pomar de laranja Natal e sua influência em relação a linha de plantio. O experimento foi instalado em Delineamento em blocos casualizados com 12 repetições por tratamento em esquema de parcelas subdividida (2 [linha e entrelinha] x 5[ *U. brizantha* (T1),*U. decumbens* (T2), *U. ruziziensis* (T3), *Glifosato* (T4), *Pousio* (T5). Foi analisado o carbono da biomassa microbiana (CBM).


```r
RESP=c(224.92, 180.32, 130.19, 110.31, 163.74,193.03, 211.49, 137.65, 127.15, 203.39,182.36, 124.75, 177.70, 231.01, 202.14,214.89, 198.42, 267.85, 207.67, 176.74,162.18, 124.59, 158.99, 209.12, 128.14,113.95, 215.53, 190.51, 174.58, 148.70,150.90, 209.03, 210.40, 199.03, 237.05,196.97, 176.06, 263.27, 240.19, 160.72,239.90, 188.07, 251.35, 215.45, 198.50,271.42, 226.56, 217.65, 213.69, 101.26,115.41, 140.10, 117.67, 106.45, 139.34,104.22, 206.13, 195.89, 147.11, 122.93,176.55, 173.63, 112.83, 184.82, 178.18,115.85, 183.89, 134.92, 086.49, 103.96,096.33, 091.64, 157.76, 107.45, 106.61,095.28, 152.37, 066.02, 125.75, 075.34,088.64, 104.00, 066.38, 084.74, 101.76,173.70, 101.24, 143.71, 119.88, 157.79,070.42, 152.75, 111.65, 153.08, 146.64,142.57, 098.96, 065.92, 065.62, 063.26,095.72, 084.14, 054.92, 090.49, 112.11,102.68, 144.77, 122.58, 125.14, 127.61,117.14, 147.87, 156.18, 154.82, 183.91,159.11, 155.41, 184.55, 121.39, 155.77)
FATOR1=rep(rep(c("L","EL"), e=12),5); FATOR1=factor(FATOR1)
FATOR2=rep(c(paste("T",1:5)),e=24); FATOR2=factor(FATOR2)
repe=rep(c(paste("R",1:12)),10); repe=factor(repe)
dados = data.frame(FATOR1,FATOR2,repe,RESP)
```

### Fator 2 x Fator 1


```r
library(lattice)
with(dados, xyplot(RESP ~ FATOR1|FATOR2, groups=repe))
```

![](20-perfil_files/figure-epub3/unnamed-chunk-2-1.png)<!-- -->


```r
with(dados, xyplot(RESP ~ FATOR1|FATOR2, groups=repe, aspect="xy"))
```

![](20-perfil_files/figure-epub3/unnamed-chunk-3-1.png)<!-- -->


```r
with(dados, xyplot(RESP ~ FATOR1|FATOR2, groups=repe, aspect="xy", type="o"))
```

![](20-perfil_files/figure-epub3/unnamed-chunk-4-1.png)<!-- -->


```r
with(dados, xyplot(RESP ~ FATOR1|FATOR2, groups=repe, aspect="xy", type="o", ylab='CBM',strip=strip.custom(strip.names=TRUE, strip.levels=TRUE)))
```

![](20-perfil_files/figure-epub3/unnamed-chunk-5-1.png)<!-- -->

### Fator 1 x Fator 2


```r
with(dados, xyplot(RESP ~ FATOR2|FATOR1, groups=repe, type="o", ylab='CBM', strip=strip.custom(strip.names=TRUE,strip.levels=TRUE)))
```

![](20-perfil_files/figure-epub3/unnamed-chunk-6-1.png)<!-- -->

<br><br><br>

****
