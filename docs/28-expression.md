# Expression()

****

Durante a elaboração de gráficos no R, os títulos são inseridos conforme o nome da variável em que está analisando. Muitas vezes é necessário editar esses nomes no gráfico, entretanto, existem casos complexos em que é necessário inserir uma série de comandos para conseguir o desejado. Neste tutorial, iremos abordar a função `expression()` e alguns exemplos.

Não iremos trabalhar com um conjunto de dados neste exemplo, dessa forma, a linha respectiva ao `plot(1,1,axes=F, col="white", ylab="",xlab="")` serve apenas para utilizar a função legend() posteriormente. Lembrando que, a função `expression()` pode ser usada para todos os argumentos de renomeação (ylab, xlab, main, title, etc...)


<div style="column-count: 2;">

<br>


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend="Resposta", 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-1-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(sum()=="sum()"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-2-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(delta == "delta"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-3-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(alpha == "alpha"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-4-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(beta =="beta"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-5-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(gamma == "gamma"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-6-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(mu == "mu"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-7-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(sigma == "sigma"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-8-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(pi == "pi"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-9-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(epsilon == "epsilon"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-10-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(lambda == "lambda"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-11-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(italic(A) == "italic(A)"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-12-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",legend=
      expression(bold(A) == "bold(A)"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-13-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center", 
       legend = expression(sigma^2==frac(sum((X[i]-mu)^2,i==1,n),N)), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-14-1.png" width="672" />

<br>


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(hat(Y) == "hat(y)"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-15-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(bar(x) =="bar(x)"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-16-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(sqrt(Y)=="sqrt(Y)"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-17-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(x^2 == "x^2"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-18-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
       legend=expression(x[2] == "x[2]"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-19-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",legend=
expression("nome\nresposta"=="nome\\nresposta"), 
bty="n", 
cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-20-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
legend=expression(hat(Y)==ax^2+bx+c,R^2==0.99), 
bty="n", 
cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-21-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
legend=expression(hat(Y)==ax^2+bx+c,R^2==0.99,italic(p-valor)==0.0001),
bty="n", cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-22-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
legend=expression(Produtividade~(kg~ha^-1)), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-23-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",legend=
expression(H[2]*0[2]~(mu*"mol"~g^-1~MFPA)), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-24-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center", 
legend=expression(MSPA~(g~kg^-1)), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-25-1.png" width="672" style="display: block; margin: auto;" />



```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",legend=
expression(bold(italic(A)) == "bold(italic(A))"), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-26-1.png" width="672" style="display: block; margin: auto;" />


```r
plot(1,1,axes=F, col="white", ylab="",xlab="")
legend("center",
legend=expression(hat(Y)==ax^2+bx+c), 
       bty="n", 
       cex=2)
```

<img src="28-expression_files/figure-html/unnamed-chunk-27-1.png" width="672" style="display: block; margin: auto;" />

</div>

<br><br><br>

****
