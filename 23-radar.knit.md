# Radar

****

<br>

Um gráfico de radar é um método gráfico de apresentar dados multivariáveis na forma de um gráfico bidimensional de três ou mais variáveis quantitativas representadas em eixos que partem do mesmo ponto. A posição relativa e o ãngulo dos eixos normalmente é pouco informativo.

O gráfico de radar é também conhecido como gráfico de teia, gráfico de aranha, gráfico de estrela, polígono irregular, gráfico polar, ou diagrama Kiviat.

<br>

### Conjunto de dados


```r
cor=c(6,6,6,7,7,7,3,4,3,3,3,3,6,6,7,6,6,7,6,7,5,6,5,3,3,5,5,5,3,3)
aroma=c(6,7,5,6,6,7,3,3,3,3,5,3,4,6,6,6,5,7,5,6,5,3,3,6,4,4,5,5,4,3)
sabor=c(5,6,6,6,5,6,3,4,3,4,2,2,3,6,7,6,7,7,6,6,5,4,5,3,6,6,5,5,4,6)
corpo=c(6,5,4,6,4,5,4,4,4,5,2,4,6,6,5,6,6,7,5,6,4,5,5,4,4,5,5,4,2,4)
global=c(5,6,6,7,5,6,3,4,3,3,2,3,4,6,6,6,6,7,6,6,5,6,5,5,4,5,5,4,3,5)
(Amostra=rep(c(paste("A", 1:5)), e=6))
```

```
##  [1] "A 1" "A 1" "A 1" "A 1" "A 1" "A 1" "A 2" "A 2" "A 2" "A 2" "A 2" "A 2"
## [13] "A 3" "A 3" "A 3" "A 3" "A 3" "A 3" "A 4" "A 4" "A 4" "A 4" "A 4" "A 4"
## [25] "A 5" "A 5" "A 5" "A 5" "A 5" "A 5"
```

```r
dados=data.frame(Amostra, cor, aroma, sabor, corpo, global)
```

**Tratamentos**:

- B100: 100% de B (Amostra A1)
- N100: 100% de N (Amostra A2)
- B75N25: 75% de B e 25% de N (Amostra A3)
- B50N50: 50% de B e 50% de N (Amostra A4)
- B25N75: 25% de B e 75% de N (Amostra A5)

### Média por variável


```r
mediacor=tapply(cor, Amostra, mean)
mediaaroma=tapply(aroma, Amostra, mean)
mediasabor=tapply(sabor, Amostra, mean)
mediacorpo=tapply(corpo, Amostra, mean)
mediaglobal=tapply(global, Amostra, mean)
medias=c(mediacor,mediaaroma, mediasabor,mediacorpo,mediaglobal)
```

<br>

### Pacote radarchart

<br>

### Lista com as médias

<br>


```r
labs=c("Cor","Aroma","Sabor","Corpo","Global")
scores=list("B100"=as.numeric(medias[c(1,6,11,16,21)]),
            "N100"=as.numeric(medias[c(2,7,12,17,22)]),
            "B75N25"=as.numeric(medias[c(3,8,13,18,23)]),  
            "B50N50"=as.numeric(medias[c(4,9,14,19,24)]),
            "B25N75"=as.numeric(medias[c(5,10,15,20,25)]))
```

Instalar pacote radarchart


```r
library(radarchart)
chartJSRadar(scores = scores,
             labs=labs, 
             plwd=4 , 
             plty=1,
             axistype=0, 
             maxmin=F,
             cglcol="grey", 
             cglty=1, 
             axislabcol="grey", 
             caxislabels=seq(0,20,5), 
             cglwd=0.8,
             vlcex=0.8)
```

```
## PhantomJS not found. You can install it with webshot::install_phantomjs(). If it is installed, please make sure the phantomjs executable can be found via the PATH variable.
```

<!--html_preserve--><canvas id="htmlwidget-9ed759046224edd62ba6" class="chartJSRadar html-widget" width="480" height="384"></canvas>
<script type="application/json" data-for="htmlwidget-9ed759046224edd62ba6">{"x":{"data":{"labels":["Cor","Aroma","Sabor","Corpo","Global"],"datasets":[{"label":"B100","data":[6.5,6.16666666666667,5.66666666666667,5,5.83333333333333],"backgroundColor":"rgba(255,0,0,0.2)","borderColor":"rgba(255,0,0,0.8)","pointBackgroundColor":"rgba(255,0,0,0.8)","pointBorderColor":"#fff","pointHoverBackgroundColor":"#fff","pointHoverBorderColor":"rgba(255,0,0,0.8)"},{"label":"N100","data":[3.16666666666667,3.33333333333333,3,3.83333333333333,3],"backgroundColor":"rgba(0,255,0,0.2)","borderColor":"rgba(0,255,0,0.8)","pointBackgroundColor":"rgba(0,255,0,0.8)","pointBorderColor":"#fff","pointHoverBackgroundColor":"#fff","pointHoverBorderColor":"rgba(0,255,0,0.8)"},{"label":"B75N25","data":[6.33333333333333,5.66666666666667,6,6,5.83333333333333],"backgroundColor":"rgba(0,0,255,0.2)","borderColor":"rgba(0,0,255,0.8)","pointBackgroundColor":"rgba(0,0,255,0.8)","pointBorderColor":"#fff","pointHoverBackgroundColor":"#fff","pointHoverBorderColor":"rgba(0,0,255,0.8)"},{"label":"B50N50","data":[5.33333333333333,4.66666666666667,4.83333333333333,4.83333333333333,5.5],"backgroundColor":"rgba(255,255,0,0.2)","borderColor":"rgba(255,255,0,0.8)","pointBackgroundColor":"rgba(255,255,0,0.8)","pointBorderColor":"#fff","pointHoverBackgroundColor":"#fff","pointHoverBorderColor":"rgba(255,255,0,0.8)"},{"label":"B25N75","data":[4,4.16666666666667,5.33333333333333,4,4.33333333333333],"backgroundColor":"rgba(255,0,255,0.2)","borderColor":"rgba(255,0,255,0.8)","pointBackgroundColor":"rgba(255,0,255,0.8)","pointBorderColor":"#fff","pointHoverBackgroundColor":"#fff","pointHoverBorderColor":"rgba(255,0,255,0.8)"}]},"options":{"responsive":true,"title":{"display":false,"text":null},"scale":{"ticks":{"min":0},"pointLabels":{"fontSize":18}},"tooltips":{"enabled":true,"mode":"label"},"legend":{"display":true},"plwd":4,"plty":1,"axistype":0,"maxmin":false,"cglcol":"grey","cglty":1,"axislabcol":"grey","caxislabels":[0,5,10,15,20],"cglwd":0.8,"vlcex":0.8}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

<br>

### Pacote plotly

<br>

### Médias por tratamento


```r
B100=c(as.numeric(medias[c(1,6,11,16,21)]))
N100=c(as.numeric(medias[c(2,7,12,17,22)]))
B75N25=c(as.numeric(medias[c(3,8,13,18,23)]))  
B50N50=c(as.numeric(medias[c(4,9,14,19,24)]))
B25N75=c(as.numeric(medias[c(5,10,15,20,25)]))
```

<br>

<center>


```r
library(plotly)
```

```
## Carregando pacotes exigidos: ggplot2
```

```
## 
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggplot2':
## 
##     last_plot
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```

```
## The following object is masked from 'package:graphics':
## 
##     layout
```

```r
(p <- plot_ly(type = 'scatterpolar',fill = 'toself') %>%
  add_trace(r = B100,theta = c('Cor','Aroma','Sabor', 'Corpo', 'Global'),name = 'B100') %>%
  add_trace(r = N100,theta = c('Cor','Aroma','Sabor', 'Corpo', 'Global'),name = 'N100') %>%
  add_trace(r = B75N25,theta = c('Cor','Aroma','Sabor', 'Corpo', 'Global'),name = 'B75N25') %>%
  add_trace(r = B50N50,theta = c('Cor','Aroma','Sabor', 'Corpo', 'Global'),name = 'B50N50') %>%
  add_trace(r = B25N75,theta = c('Cor','Aroma','Sabor', 'Corpo', 'Global'),name = 'B25N75') %>% layout(polar = list(radialaxis = list(visible = T))))
```

```
## No scatterpolar mode specifed:
##   Setting the mode to markers
##   Read more about this attribute -> https://plot.ly/r/reference/#scatter-mode
```

```
## No scatterpolar mode specifed:
##   Setting the mode to markers
##   Read more about this attribute -> https://plot.ly/r/reference/#scatter-mode
## No scatterpolar mode specifed:
##   Setting the mode to markers
##   Read more about this attribute -> https://plot.ly/r/reference/#scatter-mode
## No scatterpolar mode specifed:
##   Setting the mode to markers
##   Read more about this attribute -> https://plot.ly/r/reference/#scatter-mode
## No scatterpolar mode specifed:
##   Setting the mode to markers
##   Read more about this attribute -> https://plot.ly/r/reference/#scatter-mode
## No scatterpolar mode specifed:
##   Setting the mode to markers
##   Read more about this attribute -> https://plot.ly/r/reference/#scatter-mode
```

<!--html_preserve--><div id="htmlwidget-8dbd329d6bca68433e27" style="width:480px;height:384px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-8dbd329d6bca68433e27">{"x":{"visdat":{"39c70022586":["function () ","plotlyVisDat"]},"cur_data":"39c70022586","attrs":{"39c70022586":{"fill":"toself","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scatterpolar"},"39c70022586.1":{"fill":"toself","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scatterpolar","r":[6.5,6.16666666666667,5.66666666666667,5,5.83333333333333],"theta":["Cor","Aroma","Sabor","Corpo","Global"],"name":"B100","inherit":true},"39c70022586.2":{"fill":"toself","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scatterpolar","r":[3.16666666666667,3.33333333333333,3,3.83333333333333,3],"theta":["Cor","Aroma","Sabor","Corpo","Global"],"name":"N100","inherit":true},"39c70022586.3":{"fill":"toself","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scatterpolar","r":[6.33333333333333,5.66666666666667,6,6,5.83333333333333],"theta":["Cor","Aroma","Sabor","Corpo","Global"],"name":"B75N25","inherit":true},"39c70022586.4":{"fill":"toself","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scatterpolar","r":[5.33333333333333,4.66666666666667,4.83333333333333,4.83333333333333,5.5],"theta":["Cor","Aroma","Sabor","Corpo","Global"],"name":"B50N50","inherit":true},"39c70022586.5":{"fill":"toself","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scatterpolar","r":[4,4.16666666666667,5.33333333333333,4,4.33333333333333],"theta":["Cor","Aroma","Sabor","Corpo","Global"],"name":"B25N75","inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"polar":{"radialaxis":{"visible":true}},"hovermode":"closest","showlegend":true},"source":"A","config":{"showSendToCloud":false},"data":[{"fillcolor":"rgba(31,119,180,0.5)","fill":"toself","type":"scatterpolar","mode":"markers","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"line":{"color":"rgba(31,119,180,1)"},"frame":null},{"fillcolor":"rgba(255,127,14,0.5)","fill":"toself","type":"scatterpolar","r":[6.5,6.16666666666667,5.66666666666667,5,5.83333333333333],"theta":["Cor","Aroma","Sabor","Corpo","Global"],"name":"B100","mode":"markers","marker":{"color":"rgba(255,127,14,1)","line":{"color":"rgba(255,127,14,1)"}},"line":{"color":"rgba(255,127,14,1)"},"frame":null},{"fillcolor":"rgba(44,160,44,0.5)","fill":"toself","type":"scatterpolar","r":[3.16666666666667,3.33333333333333,3,3.83333333333333,3],"theta":["Cor","Aroma","Sabor","Corpo","Global"],"name":"N100","mode":"markers","marker":{"color":"rgba(44,160,44,1)","line":{"color":"rgba(44,160,44,1)"}},"line":{"color":"rgba(44,160,44,1)"},"frame":null},{"fillcolor":"rgba(214,39,40,0.5)","fill":"toself","type":"scatterpolar","r":[6.33333333333333,5.66666666666667,6,6,5.83333333333333],"theta":["Cor","Aroma","Sabor","Corpo","Global"],"name":"B75N25","mode":"markers","marker":{"color":"rgba(214,39,40,1)","line":{"color":"rgba(214,39,40,1)"}},"line":{"color":"rgba(214,39,40,1)"},"frame":null},{"fillcolor":"rgba(148,103,189,0.5)","fill":"toself","type":"scatterpolar","r":[5.33333333333333,4.66666666666667,4.83333333333333,4.83333333333333,5.5],"theta":["Cor","Aroma","Sabor","Corpo","Global"],"name":"B50N50","mode":"markers","marker":{"color":"rgba(148,103,189,1)","line":{"color":"rgba(148,103,189,1)"}},"line":{"color":"rgba(148,103,189,1)"},"frame":null},{"fillcolor":"rgba(140,86,75,0.5)","fill":"toself","type":"scatterpolar","r":[4,4.16666666666667,5.33333333333333,4,4.33333333333333],"theta":["Cor","Aroma","Sabor","Corpo","Global"],"name":"B25N75","mode":"markers","marker":{"color":"rgba(140,86,75,1)","line":{"color":"rgba(140,86,75,1)"}},"line":{"color":"rgba(140,86,75,1)"},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

</center>


```r
library(fmsb)
data=rbind(round(B100,1),
           round(N100,1),
           round(B75N25,1),
           round(B50N50,1),
           round(B25N75,1))
rownames(data)=c("B100","N100","B75N25","B50N50","B25N75")
colnames(data)=c('Cor','Aroma','Sabor', 'Corpo', 'Global')
data=data.frame(data)
radarchart(data,axistype = 2)
```

![](23-radar_files/figure-epub3/unnamed-chunk-7-1.png)<!-- -->

<br><br><br>

****

