# Análise de sobrevivência

*****

<br><br>

<img src="32-survival_files/figure-html/unnamed-chunk-1-1.png" width="480" />

Análise de sobrevivência, também denominada análise de sobrevida, é um ramo da estatística que estuda o tempo de duração esperado até a ocorrência de um ou mais eventos, tais como morte em organismos biológicos ou falha em sistemas mecânicos. Na agronomia, tem sido bastante utilizada na avaliação residual de produtos fitossanitários em insetos, tempo até a morte em função de um doença, etc.

<br><br>

****

****

## Conjunto de dados

****

O conjunto de dados é de um experimento cujo objetivo é avaliar a mortalidade de insetos em função de alguns produtos comerciais. 


```r
tempo=c(10,10,10,10,10,10,10,24,24,24,24,48,10,10,10,10,10,10,10,10,10,10,10,10,24,24,48,48,72,72,72,72,72,72,72,72,10,10,24,24,72,72,72,72,72,72,96,96,10,10,10,48,96,96,144,144,168,168,168,168,10,10,24,24,72,72,72,96,96,120,168,168,10,10,10,10,10,10,10,24,24,24,24,48,10,10,10,24,24,120,120,144,144,144,144,144,10,10,144,144,168,168,168,168,168,168,168,168,24,72,96,96,120,144,168,168,168,168,168,168,24,72,96,120,144,168,168,168,168,168,168,168,10,10,10,10,10,10,24,72,96,168,168,168)
# criando vetor de status (Ocorreu ou nao o evento)
status=c(1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,0,0,0,1,1,1,1,1,1,1,1,1,1,1,0,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,0,0,0,1,1,1,1,1,1,1,0,0,0,1,0,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1,1,1,1,1,1,1,0,0)
trat=rep(c("T1","T2",'T3'),e=48)
dados=data.frame(trat,tempo,status)
```

<br><br>

## Histograma


```r
hist(tempo)
```

<img src="32-survival_files/figure-html/unnamed-chunk-3-1.png" width="672" />

<br><br>

****

## Método não-paramétrico de Kaplan-meier

****

<br><br>

### Sem considerar tratamentos

Somente uma análise exploratória geral


```r
library(survival)
library(survminer)
KM <- survfit(Surv(tempo,status) ~ 1, type="kaplan-meier")
summary(KM)
```

```
## Call: survfit(formula = Surv(tempo, status) ~ 1, type = "kaplan-meier")
## 
##  time n.risk n.event survival std.err lower 95% CI upper 95% CI
##    10    144      44    0.694  0.0384       0.6231        0.774
##    24    100      19    0.562  0.0413       0.4870        0.650
##    48     81       5    0.528  0.0416       0.4522        0.616
##    72     76      20    0.389  0.0406       0.3169        0.477
##    96     56      10    0.319  0.0389       0.2517        0.405
##   120     46       5    0.285  0.0376       0.2198        0.369
##   144     41      11    0.208  0.0338       0.1515        0.286
##   168     30      12    0.125  0.0276       0.0811        0.193
```

```r
ggsurvplot(
  fit = survfit(Surv(tempo, status) ~ 1),data=dados, 
  xlab = "Time (hours)", 
  ylab = "Overall survival probability")
```

<img src="32-survival_files/figure-html/unnamed-chunk-4-1.png" width="1152" />

### Tempo médio de sobrevivência


```r
a=survival:::survmean(KM, rmean=48)
a$matrix[5]
```

```
##   *rmean 
## 33.22222
```

<br><br>

### Considerando tratamentos

### Conferindo diferenças par a par


```r
pvalor=pairwise_survdiff(Surv(tempo,status)~trat,data=dados, rho=0)
knitr::kable(pvalor$p.value)
```

             T1          T2
---  ----------  ----------
T2    0.0003111          NA
T3    0.0000000   0.0006521

Todos diferem entre si

### Grafico por tratamento usando o método de Kaplan-Meier


```r
KM1 <- survfit(Surv(tempo,status) ~ trat, type="kaplan-meier")
ggsurvplot(
  fit = survfit(Surv(tempo, status) ~ trat),data=dados, 
  xlab = "Time (hours)", 
  ylab = "Overall survival probability")
```

<img src="32-survival_files/figure-html/unnamed-chunk-7-1.png" width="1152" />

### Tempo médio de sobrevivência


```r
survival:::survmean(KM1, rmean=48)$matrix[,5]
```

```
##  trat=T1  trat=T2  trat=T3 
## 27.37500 32.12500 40.16667
```

<br><br>

****

## Modelo paramétrico

****

<br><br>

****

### Distribuição exponencial

****

<br><br>

### Sem considerar tratamentos


```r
KM <- survreg(Surv(tempo,status) ~ 1, dist="exponential")
summary(KM)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ 1, dist = "exponential")
##              Value Std. Error    z      p
## (Intercept) 4.4473     0.0891 49.9 <2e-16
## 
## Scale fixed at 1 
## 
## Exponential distribution
## Loglik(model)= -686.4   Loglik(intercept only)= -686.4
## Number of Newton-Raphson Iterations: 4 
## n= 144
```

```r
s <- seq(.01, .99, by = .01)
t_0 <- predict(KM, newdata = data.frame(trat=paste("T1","T2","T3")), 
                 type = "quantile", p = s)
smod <- data.frame(time = c(t_0), # acrescentar os tratamentos 
                   surv = rep(1 - s, times = 1), # mudar o times
                   upper = NA, lower = NA)
ggsurvplot(smod)  
```

<img src="32-survival_files/figure-html/unnamed-chunk-9-1.png" width="1152" />

### Considerando tratamentos


```r
library(survival)
library(survminer)
KM2 <- survreg(Surv(tempo,status) ~ trat, dist="exponential")
summary(KM)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ 1, dist = "exponential")
##              Value Std. Error    z      p
## (Intercept) 4.4473     0.0891 49.9 <2e-16
## 
## Scale fixed at 1 
## 
## Exponential distribution
## Loglik(model)= -686.4   Loglik(intercept only)= -686.4
## Number of Newton-Raphson Iterations: 4 
## n= 144
```

```r
anova(KM2)
```

```
##      Df Deviance Resid. Df    -2*LL     Pr(>Chi)
## NULL NA       NA       143 1372.722           NA
## trat  2 44.24522       141 1328.477 2.467593e-10
```

```r
s <- seq(.01, .99, by = .01)
t_0 <- predict(KM2, newdata = data.frame(trat = "T1"), type = "quantile", p = s)
t_1 <- predict(KM2, newdata = data.frame(trat = "T2"), type = "quantile", p = s)
t_2 <- predict(KM2, newdata = data.frame(trat = "T3"), type = "quantile", p = s)
smod <- data.frame(time = c(t_0, t_1, t_2), # acrescentar os tratamentos 
                   surv = rep(1 - s, times = 3), # mudar o times
                   strata = rep(c("T1", "T2", "T3"), each = length(s)),
                   upper = NA, lower = NA)
ggsurvplot(smod)  
```

<img src="32-survival_files/figure-html/unnamed-chunk-10-1.png" width="1152" />

<br><br>

****

## Distribuição gaussiano

****

### Sem considerar tratamentos


```r
KM <- survreg(Surv(tempo,status) ~ 1, dist="gaussian")
summary(KM)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ 1, dist = "gaussian")
##               Value Std. Error    z      p
## (Intercept) 78.8982     5.9303 13.3 <2e-16
## Log(scale)   4.2519     0.0652 65.2 <2e-16
## 
## Scale= 70.2 
## 
## Gaussian distribution
## Loglik(model)= -735.6   Loglik(intercept only)= -735.6
## Number of Newton-Raphson Iterations: 5 
## n= 144
```

### Considerando tratamentos


```r
KM3 <- survreg(Surv(tempo,status) ~ trat, dist="gaussian")
summary(KM3)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ trat, dist = "gaussian")
##               Value Std. Error     z       p
## (Intercept) 36.3750     8.5829  4.24 2.3e-05
## tratT2      37.3906    12.1867  3.07  0.0022
## tratT3      89.7879    12.3737  7.26 4.0e-13
## Log(scale)   4.0854     0.0649 62.96 < 2e-16
## 
## Scale= 59.5 
## 
## Gaussian distribution
## Loglik(model)= -712.5   Loglik(intercept only)= -735.6
## 	Chisq= 46.23 on 2 degrees of freedom, p= 9.2e-11 
## Number of Newton-Raphson Iterations: 4 
## n= 144
```

```r
anova(KM3)
```

```
##      Df Deviance Resid. Df    -2*LL     Pr(>Chi)
## NULL NA       NA       142 1471.295           NA
## trat  2 46.22645       140 1425.069 9.163355e-11
```

```r
t_0 <- predict(KM3, newdata = data.frame(trat = "T1"), type = "lp")
t_1 <- predict(KM3, newdata = data.frame(trat = "T2"),type = "lp")
t_2 <- predict(KM3, newdata = data.frame(trat = "T3"),type = "lp")
x_grid <- 1:400
sur_curves <- sapply(t_0, function(x)survreg.distributions[[KM3$dist]]$density((x - x_grid)/KM3$scale)[, 1])
sur_curves1 <- sapply(t_1, function(x)survreg.distributions[[KM3$dist]]$density((x - x_grid)/KM3$scale)[, 1])
sur_curves2 <- sapply(t_2, function(x)survreg.distributions[[KM3$dist]]$density((x - x_grid)/KM3$scale)[, 1])
matplot(x_grid, sur_curves, type = "l", lty = 1,ylim=c(0,1))
lines(x_grid,sur_curves1,col="red")
lines(x_grid,sur_curves2,col="blue")
```

<img src="32-survival_files/figure-html/unnamed-chunk-12-1.png" width="1152" />

<br><br>

****

## Distribuição logistico

****

### Sem considerar tratamentos


```r
KM <- survreg(Surv(tempo,status) ~ 1, dist="logistic")
summary(KM)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ 1, dist = "logistic")
##               Value Std. Error    z      p
## (Intercept) 72.5020     6.3768 11.4 <2e-16
## Log(scale)   3.7594     0.0722 52.0 <2e-16
## 
## Scale= 42.9 
## 
## Logistic distribution
## Loglik(model)= -739.5   Loglik(intercept only)= -739.5
## Number of Newton-Raphson Iterations: 5 
## n= 144
```

### Considerando tratamentos


```r
KM4 <- survreg(Surv(tempo,status) ~ trat, dist="logistic")
summary(KM4)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ trat, dist = "logistic")
##               Value Std. Error     z       p
## (Intercept) 35.4968     7.7296  4.59 4.4e-06
## tratT2      31.3587    12.2695  2.56   0.011
## tratT3      98.9211    12.4589  7.94 2.0e-15
## Log(scale)   3.5544     0.0737 48.20 < 2e-16
## 
## Scale= 35 
## 
## Logistic distribution
## Loglik(model)= -714.3   Loglik(intercept only)= -739.5
## 	Chisq= 50.45 on 2 degrees of freedom, p= 1.1e-11 
## Number of Newton-Raphson Iterations: 4 
## n= 144
```

```r
anova(KM4)
```

```
##      Df Deviance Resid. Df    -2*LL     Pr(>Chi)
## NULL NA       NA       142 1479.091           NA
## trat  2 50.45218       140 1428.639 1.107765e-11
```

```r
t_0 <- predict(KM4, newdata = data.frame(trat = "T1"), type = "lp")
t_1 <- predict(KM4, newdata = data.frame(trat = "T2"),type = "lp")
t_2 <- predict(KM4, newdata = data.frame(trat = "T3"),type = "lp")
x_grid <- 1:400
sur_curves <- sapply(t_0, function(x)survreg.distributions[[KM4$dist]]$density((x - x_grid)/KM4$scale)[, 1])
sur_curves1 <- sapply(t_1, function(x)survreg.distributions[[KM4$dist]]$density((x - x_grid)/KM4$scale)[, 1])
sur_curves2 <- sapply(t_2, function(x)survreg.distributions[[KM4$dist]]$density((x - x_grid)/KM4$scale)[, 1])
matplot(x_grid, sur_curves, type = "l", lty = 1,ylim=c(0,1))
lines(x_grid,sur_curves1,col="red")
lines(x_grid,sur_curves2,col="blue")
```

<img src="32-survival_files/figure-html/unnamed-chunk-14-1.png" width="1152" />

<br><br>

****

## Distribuição Log normal

****

### Sem considerar tratamentos


```r
KM <- survreg(Surv(tempo,status) ~ 1, dist="lognormal")
summary(KM)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ 1, dist = "lognormal")
##              Value Std. Error     z       p
## (Intercept) 3.8658     0.1080 35.80 < 2e-16
## Log(scale)  0.2438     0.0648  3.76 0.00017
## 
## Scale= 1.28 
## 
## Log Normal distribution
## Loglik(model)= -681.1   Loglik(intercept only)= -681.1
## Number of Newton-Raphson Iterations: 5 
## n= 144
```

### Considerando tratamentos


```r
KM5 <- survreg(Surv(tempo,status) ~ trat, dist="lognormal")
summary(KM5)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ trat, dist = "lognormal")
##              Value Std. Error     z      p
## (Intercept) 3.2165     0.1655 19.43 <2e-16
## tratT2      0.5650     0.2352  2.40  0.016
## tratT3      1.3925     0.2394  5.82  6e-09
## Log(scale)  0.1369     0.0644  2.12  0.034
## 
## Scale= 1.15 
## 
## Log Normal distribution
## Loglik(model)= -665.4   Loglik(intercept only)= -681.1
## 	Chisq= 31.54 on 2 degrees of freedom, p= 1.4e-07 
## Number of Newton-Raphson Iterations: 4 
## n= 144
```

```r
anova(KM5)
```

```
##      Df Deviance Resid. Df    -2*LL     Pr(>Chi)
## NULL NA       NA       142 1362.288           NA
## trat  2 31.54326       140 1330.744 1.414059e-07
```

```r
s <- seq(.01, .99, by = .01)
t_0 <- predict(KM5, newdata = data.frame(trat = "T1"), type = "quantile", p = s)
t_1 <- predict(KM5, newdata = data.frame(trat = "T2"), type = "quantile", p = s)
t_2 <- predict(KM5, newdata = data.frame(trat = "T3"), type = "quantile", p = s)
smod <- data.frame(time = c(t_0, t_1, t_2), # acrescentar os tratamentos 
                   surv = rep(1 - s, times = 3), # mudar o times
                   strata = rep(c("T1", "T2", "T3"), each = length(s)),
                   upper = NA, lower = NA)
ggsurvplot(smod)  
```

<img src="32-survival_files/figure-html/unnamed-chunk-16-1.png" width="1152" />

<br><br>

****

## Distribuição Log-Logístico

****

### Sem considerar tratamentos


```r
KM <- survreg(Surv(tempo,status) ~ 1, dist="loglogistic")
summary(KM)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ 1, dist = "loglogistic")
##               Value Std. Error     z      p
## (Intercept)  3.8717     0.1192 32.49 <2e-16
## Log(scale)  -0.2265     0.0711 -3.19 0.0014
## 
## Scale= 0.797 
## 
## Log logistic distribution
## Loglik(model)= -687   Loglik(intercept only)= -687
## Number of Newton-Raphson Iterations: 5 
## n= 144
```

### Considerando tratamentos


```r
KM6 <- survreg(Surv(tempo,status) ~ trat, dist="loglogistic")
summary(KM6)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ trat, dist = "loglogistic")
##               Value Std. Error     z       p
## (Intercept)  3.1947     0.1689 18.92 < 2e-16
## tratT2       0.5839     0.2530  2.31   0.021
## tratT3       1.5687     0.2441  6.43 1.3e-10
## Log(scale)  -0.3709     0.0725 -5.11 3.2e-07
## 
## Scale= 0.69 
## 
## Log logistic distribution
## Loglik(model)= -669.2   Loglik(intercept only)= -687
## 	Chisq= 35.64 on 2 degrees of freedom, p= 1.8e-08 
## Number of Newton-Raphson Iterations: 4 
## n= 144
```

```r
anova(KM6)
```

```
##      Df Deviance Resid. Df    -2*LL     Pr(>Chi)
## NULL NA       NA       142 1373.973           NA
## trat  2 35.64462       140 1338.328 1.819156e-08
```

```r
s <- seq(.01, .99, by = .01)
t_0 <- predict(KM6, newdata = data.frame(trat = "T1"), type = "quantile", p = s)
t_1 <- predict(KM6, newdata = data.frame(trat = "T2"), type = "quantile", p = s)
t_2 <- predict(KM6, newdata = data.frame(trat = "T3"), type = "quantile", p = s)
smod <- data.frame(time = c(t_0, t_1, t_2), # acrescentar os tratamentos 
                   surv = rep(1 - s, times = 3), # mudar o times
                   strata = rep(c("T1", "T2", "T3"), each = length(s)),
                   upper = NA, lower = NA)
ggsurvplot(smod)  
```

<img src="32-survival_files/figure-html/unnamed-chunk-18-1.png" width="1152" />

<br><br>

****

## Distribuição Weibull (default)

*****

### Sem considerar tratamentos


```r
KM <- survreg(Surv(tempo,status) ~ 1, dist="weibull")
summary(KM)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ 1, dist = "weibull")
##              Value Std. Error     z      p
## (Intercept) 4.4310     0.0969 45.72 <2e-16
## Log(scale)  0.0685     0.0740  0.93   0.35
## 
## Scale= 1.07 
## 
## Weibull distribution
## Loglik(model)= -685.9   Loglik(intercept only)= -685.9
## Number of Newton-Raphson Iterations: 6 
## n= 144
```

### Considerando tratamentos


```r
KM7 <- survreg(Surv(tempo,status) ~ trat, dist="weibull")
summary(KM7)
```

```
## 
## Call:
## survreg(formula = Surv(tempo, status) ~ trat, dist = "weibull")
##               Value Std. Error     z       p
## (Intercept)  3.6259     0.1334 27.18 < 2e-16
## tratT2       0.7769     0.1906  4.08 4.6e-05
## tratT3       1.4392     0.2043  7.05 1.8e-12
## Log(scale)  -0.0969     0.0744 -1.30    0.19
## 
## Scale= 0.908 
## 
## Weibull distribution
## Loglik(model)= -663.4   Loglik(intercept only)= -685.9
## 	Chisq= 45 on 2 degrees of freedom, p= 1.7e-10 
## Number of Newton-Raphson Iterations: 5 
## n= 144
```

```r
anova(KM7)
```

```
##      Df Deviance Resid. Df    -2*LL     Pr(>Chi)
## NULL NA       NA       142 1371.840           NA
## trat  2 44.99626       140 1326.844 1.695061e-10
```

```r
s <- seq(.01, .99, by = .01)
t_0 <- predict(KM7, newdata = data.frame(trat = "T1"), type = "quantile", p = s)
t_1 <- predict(KM7, newdata = data.frame(trat = "T2"), type = "quantile", p = s)
t_2 <- predict(KM7, newdata = data.frame(trat = "T3"), type = "quantile", p = s)
smod <- data.frame(time = c(t_0, t_1, t_2), # acrescentar os tratamentos 
                   surv = rep(1 - s, times = 3), # mudar o times
                   strata = rep(c("T1", "T2", "T3"), each = length(s)),
                   upper = NA, lower = NA)
ggsurvplot(smod)  
```

<img src="32-survival_files/figure-html/unnamed-chunk-20-1.png" width="1152" />


<br><br><br>

****

## Gompertz

****


```r
library(flexsurv)
KM9=flexsurvreg(Surv(tempo,status)~trat,dist="Gompertz")
summary(KM9)
```

```
## trat=T1 
##   time         est          lcl        ucl
## 1   10 0.786371074 7.187338e-01 0.83738134
## 2   24 0.549854904 4.451279e-01 0.63862411
## 3   48 0.279640531 1.790314e-01 0.38288353
## 4   72 0.130206542 6.334527e-02 0.21531499
## 5   96 0.054871360 1.911752e-02 0.11354777
## 6  120 0.020657887 4.247756e-03 0.05747200
## 7  144 0.006846406 7.114686e-04 0.02824022
## 8  168 0.001964497 7.212948e-05 0.01341603
## 
## trat=T2 
##   time        est        lcl       ucl
## 1   10 0.91229451 0.87233985 0.9413002
## 2   24 0.79577094 0.71969924 0.8575090
## 3   48 0.61465240 0.50410842 0.7127744
## 4   72 0.45902365 0.34168956 0.5705144
## 5   96 0.32998531 0.22378318 0.4357505
## 6  120 0.22722132 0.13795535 0.3222539
## 7  144 0.14902446 0.07589203 0.2354252
## 8  168 0.09250403 0.03798742 0.1668742
## 
## trat=T3 
##   time       est       lcl       ucl
## 1   10 0.9585577 0.9322168 0.9746135
## 2   24 0.9000225 0.8442063 0.9363724
## 3   48 0.7989822 0.7077183 0.8630863
## 4   72 0.6983485 0.5870620 0.7832759
## 5   96 0.5997606 0.4737519 0.6965202
## 6  120 0.5049620 0.3783229 0.6111961
## 7  144 0.4157087 0.2887969 0.5281183
## 8  168 0.3336543 0.2144052 0.4515043
```

```r
plot(KM9,col=c(1,2,3))
```

<img src="32-survival_files/figure-html/unnamed-chunk-21-1.png" width="672" />

****

## Gamma

****


```r
library(flexsurv)
KM10=flexsurvreg(Surv(tempo,status)~trat,dist="gamma")
summary(KM10)
```

```
## trat=T1 
##   time         est         lcl        ucl
## 1   10 0.790201487 0.716314014 0.85306545
## 2   24 0.537681788 0.442594349 0.62835481
## 3   48 0.267748022 0.182488188 0.36404586
## 4   72 0.130741530 0.071150531 0.21047110
## 5   96 0.063206831 0.027455096 0.12386594
## 6  120 0.030369861 0.010503693 0.07206528
## 7  144 0.014531118 0.003959448 0.04223269
## 8  168 0.006931519 0.001462594 0.02411293
## 
## trat=T2 
##   time       est        lcl       ucl
## 1   10 0.9055576 0.85483298 0.9450987
## 2   24 0.7671054 0.67758957 0.8397180
## 3   48 0.5650288 0.44835976 0.6679526
## 4   72 0.4110387 0.29288694 0.5259440
## 5   96 0.2969771 0.19041900 0.4113474
## 6  120 0.2136179 0.12080451 0.3199308
## 7  144 0.1531754 0.07659963 0.2492097
## 8  168 0.1095770 0.04714501 0.1936260
## 
## trat=T3 
##   time       est       lcl       ucl
## 1   10 0.9552715 0.9229031 0.9763875
## 2   24 0.8838874 0.8278315 0.9274564
## 3   48 0.7645536 0.6784217 0.8317849
## 4   72 0.6563859 0.5532722 0.7411864
## 5   96 0.5610497 0.4466789 0.6608527
## 6  120 0.4781342 0.3574859 0.5870168
## 7  144 0.4065841 0.2856213 0.5232180
## 8  168 0.3451603 0.2255266 0.4599759
```

```r
plot(KM10,col=c(1,2,3))
```

<img src="32-survival_files/figure-html/unnamed-chunk-22-1.png" width="672" />

<br><br>

****

## Método semi-paramétrico de Cox

****

Serve para um modelo de regressão de riscos proporcionais de Cox. Variáveis dependentes do tempo, estratos dependentes do tempo, vários eventos por assunto e outras extensões são incorporadas usando a formulação do processo de contagem de Andersen e Gill.

**Reference**: Andersen, P. and Gill, R. (1982). Cox's regression model for counting processes, a large sample study. Annals of Statistics 10, 1100-1120.

### Sem considerar tratamentos


```r
KM <- coxph(Surv(tempo,status) ~ 1)
summary(KM)
```

```
## Call:  coxph(formula = Surv(tempo, status) ~ 1)
## 
## Null model
##   log likelihood= -538.6621 
##   n= 144
```

### Considerando tratamentos


```r
KM8 <- coxph(Surv(tempo,status) ~ strata(trat),data=dados)
summary(KM8)
```

```
## Call:  coxph(formula = Surv(tempo, status) ~ strata(trat), data = dados)
## 
## Null model
##   log likelihood= -394.6821 
##   n= 144
```

```r
library(ggfortify)
autoplot(survfit(KM8),conf.int = F)+theme_classic()
```

<img src="32-survival_files/figure-html/unnamed-chunk-24-1.png" width="1152" />

<br><br>

****

## Modelo de riscos proporcionais de COX

****

<br><br>

Mostra as taxas de risco (HR) derivadas do modelo para todas as covariáveis incluídas na fórmula coxph. Resumidamente, uma FC> 1 indica um risco aumentado de morte (de acordo com a definição de h(t)) se uma condição específica for atendida por um paciente. Uma FC <1, por outro lado, indica uma diminuição do risco.

<br><br>

### Considerando trat


```r
library(forestmodel)
colnames(dados)=c("Treatments","tempo","status")
fit.coxph <- coxph(Surv(tempo, status) ~ Treatments, data = dados)
#ggforest(fit.coxph, data = dados)
print(forest_model(fit.coxph, limits=log( c(0.05, 5))))
```

```
## Warning: Ignoring unknown aesthetics: x
```

<img src="32-survival_files/figure-html/unnamed-chunk-25-1.png" width="1152" />

## Critério de inferência de Akaike


```r
library(car)
```

```
## Warning: package 'car' was built under R version 3.6.3
```

```
## Carregando pacotes exigidos: carData
```

```r
AIC(KM2) # exponencial
```

```
## [1] 1334.477
```

```r
AIC(KM3) # normal
```

```
## [1] 1433.069
```

```r
AIC(KM4) # logistico
```

```
## [1] 1436.639
```

```r
AIC(KM5) # lognormal
```

```
## [1] 1338.744
```

```r
AIC(KM6) # loglogistic
```

```
## [1] 1346.328
```

```r
AIC(KM7) # weibull
```

```
## [1] 1334.844
```

```r
AIC(KM8) # coxph
```

```
## [1] 789.3642
```

```r
AIC(KM9) # Gompertz
```

```
## [1] 1331.275
```

## Resíduo


```r
residuo2 <- residuals(KM2, type = "deviance")
g2=ggplot(data = dados, mapping = aes(x = tempo, y = residuo2)) +
    geom_point() + labs(title="Exponential")+
    geom_smooth() +
    theme_bw() + theme(legend.key = element_blank())
residuo3 <- residuals(KM3, type = "deviance")
g3=ggplot(data = dados, mapping = aes(x = tempo, y = residuo3)) +
    geom_point() + labs(title="Normal")+
    geom_smooth() +
    theme_bw() + theme(legend.key = element_blank())
residuo4 <- residuals(KM4, type = "deviance")
g4=ggplot(data = dados, mapping = aes(x = tempo, y = residuo4)) +
    geom_point() + labs(title="Logístico")+
    geom_smooth() +
    theme_bw() + theme(legend.key = element_blank())
residuo5 <- residuals(KM5, type = "deviance")
g5=ggplot(data = dados, mapping = aes(x = tempo, y = residuo5)) +
    geom_point() + labs(title="lognormal")+
    geom_smooth() +
    theme_bw() + theme(legend.key = element_blank())
residuo6 <- residuals(KM6, type = "deviance")
g6=ggplot(data = dados, mapping = aes(x = tempo, y = residuo6)) +
    geom_point() + labs(title="loglogistico")+
    geom_smooth() +
    theme_bw() + theme(legend.key = element_blank())
residuo7 <- residuals(KM7, type = "deviance")
g7=ggplot(data = dados, mapping = aes(x = tempo, y = residuo7)) +
    geom_point() + labs(title="weibull")+
    geom_smooth() +
    theme_bw() + theme(legend.key = element_blank())
residuo8 <- residuals(KM8, type = "deviance")
g8=ggplot(data = dados, mapping = aes(x = tempo, y = residuo8)) +
    geom_point() + labs(title="coxph")+
    geom_smooth() +
    theme_bw() + theme(legend.key = element_blank())
library(gridExtra)
grid.arrange(g2,g3,g4,g5,g6,g7,g8,ncol=4)
```

```
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
```

<img src="32-survival_files/figure-html/unnamed-chunk-27-1.png" width="672" />

<br><br><br><br><br><br>
