# Setores circulares 

****

O gráfico de Setores, também conhecido como gráfico de pizza ou gráfico circular é um diagrama circular onde os valores de cada categoria estatística representada são proporcionais às respectivas frequências. Este gráfico pode vir acompanhado de porcentagens. É utilizado para dados qualitativos nominais. Para construir um gráfico de setores é necessário determinar o ângulo dos setores circulares correspondentes à contribuição percentual de cada valor no total.

<br><br>

### Conjunto de dados


```r
variedade=c("Hass","Breda","Quintal","Geada","Margarida","Hass","Geada","Margarida","Hass","Margarida","Hass","Breda","Quintal","Breda","Quintal","Geada","Margarida","Breda","Quintal","Hass","Margarida","Hass","Breda","Hass","Margarida","Hass","Breda","Quintal","Breda","Quintal","Geada","Margarida","Breda","Quintal","Hass","Margarida","Hass","Breda","Geada","Margarida","Breda","Quintal","Hass","Margarida","Hass","Breda","Hass","Margarida","Hass","Breda","Quintal","Breda","Quintal","Geada","Margarida","Breda","Quintal","Hass","Margarida","Hass","Breda","Hass","Margarida","Hass","Breda","Quintal","Breda","Quintal","Geada","Margarida","Breda","Quintal","Quintal","Breda","Quintal")
```

<br>

### Frequências


```r
factor(variedade)
```

```
##  [1] Hass      Breda     Quintal   Geada     Margarida Hass      Geada    
##  [8] Margarida Hass      Margarida Hass      Breda     Quintal   Breda    
## [15] Quintal   Geada     Margarida Breda     Quintal   Hass      Margarida
## [22] Hass      Breda     Hass      Margarida Hass      Breda     Quintal  
## [29] Breda     Quintal   Geada     Margarida Breda     Quintal   Hass     
## [36] Margarida Hass      Breda     Geada     Margarida Breda     Quintal  
## [43] Hass      Margarida Hass      Breda     Hass      Margarida Hass     
## [50] Breda     Quintal   Breda     Quintal   Geada     Margarida Breda    
## [57] Quintal   Hass      Margarida Hass      Breda     Hass      Margarida
## [64] Hass      Breda     Quintal   Breda     Quintal   Geada     Margarida
## [71] Breda     Quintal   Quintal   Breda     Quintal  
## Levels: Breda Geada Hass Margarida Quintal
```

```r
n=length(variedade)
table(variedade)
```

```
## variedade
##     Breda     Geada      Hass Margarida   Quintal 
##        19         7        18        15        16
```

```r
proporção = prop.table(table(variedade))
```

<br>

### Gráfico básico


```r
pie(proporção*100)
```

![](18-pizza_files/figure-epub3/unnamed-chunk-3-1.png)<!-- -->

<br>

### Melhorias


```r
pie(proporção*100, 
    edges=400, 
    radius=1, 
    col=c("red","green","yellow","blue","orange"), 
    main="Variedades de abacate")
```

![](18-pizza_files/figure-epub3/unnamed-chunk-4-1.png)<!-- -->

<br>

### Plotando valores

Obs. sem casa decimal


```r
pie(proporção*100, 
    edges=400, 
    radius=1, 
    labels=paste(names(proporção),"(",round(proporção*100,0),"%",")"), 
    col=c("red","green","yellow","blue","orange"), 
    main="Variedades de abacate")
```

![](18-pizza_files/figure-epub3/unnamed-chunk-5-1.png)<!-- -->

<br><br>

<br>

****

## Gráfico de Setores Circulares 3D

****

<br><br>

### Descobrindo as frequências


```r
factor(variedade)
```

```
##  [1] Hass      Breda     Quintal   Geada     Margarida Hass      Geada    
##  [8] Margarida Hass      Margarida Hass      Breda     Quintal   Breda    
## [15] Quintal   Geada     Margarida Breda     Quintal   Hass      Margarida
## [22] Hass      Breda     Hass      Margarida Hass      Breda     Quintal  
## [29] Breda     Quintal   Geada     Margarida Breda     Quintal   Hass     
## [36] Margarida Hass      Breda     Geada     Margarida Breda     Quintal  
## [43] Hass      Margarida Hass      Breda     Hass      Margarida Hass     
## [50] Breda     Quintal   Breda     Quintal   Geada     Margarida Breda    
## [57] Quintal   Hass      Margarida Hass      Breda     Hass      Margarida
## [64] Hass      Breda     Quintal   Breda     Quintal   Geada     Margarida
## [71] Breda     Quintal   Quintal   Breda     Quintal  
## Levels: Breda Geada Hass Margarida Quintal
```

```r
n=length(variedade)
table(variedade)
```

```
## variedade
##     Breda     Geada      Hass Margarida   Quintal 
##        19         7        18        15        16
```

```r
proporção = prop.table(table(variedade))
```

<br>

### Gráfico em 3D


```r
library(plotrix)
pie3D(proporção*100)
```

![](18-pizza_files/figure-epub3/unnamed-chunk-7-1.png)<!-- -->

<br>

### Separando os setores


```r
pie3D(proporção*100, 
      explode=0.1, 
      main="Variedades de abacate")
```

![](18-pizza_files/figure-epub3/unnamed-chunk-8-1.png)<!-- -->

<br>

### Adicionando nomes e frequências


```r
pie3D(proporção*100, 
      explode=0.1, 
      cex=0.8,
      labels=paste(names(proporção),
                   "(",round(proporção*100,0),"%",")"), 
      main="Variedades de abacate")
```

![](18-pizza_files/figure-epub3/unnamed-chunk-9-1.png)<!-- -->

<br><br><br>

****

