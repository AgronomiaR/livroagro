# Estatística Descritiva

<br>

As estatísticas descritivas são números que resumem e descrevem o conjuntos de dados. As estatísticas descritivas apenas "descrevem" os dados, elas não representam generalizações da amostra para a população.

Abaixo, segue alguns comandos do software R e as respectivas explicações das análises. Foi utilizado um conjunto de dados para melhor exemplificação.

****

## Conjunto de Dados

****

Existem várias formas de entrada ou leitura de dados no R. Para um conjunto de dados pequeno, pode-se entrar com as informações diretamente no console do programa. Considere um delineamento 
inteiramente ao acaso com 5 tratamentos e 4 repetições. A entrada dos dados, entre outras, poderia ser da forma:


```r
tratamentos = rep(c(paste("T", sep='', 1:5)), each=4)
resposta = c(100, 120, 110,  90,
             150, 145, 149, 165,
             150, 144, 134, 139,
             220, 206, 211, 210,
             266, 249, 248, 260)
```

<br><br>

****

## Medidas de Tendência Central

****

As medidas de tendência central ou posição são utilizadas para resumir, em um único número, o conjunto de dados observados da variável em estudo. 

Usualmente emprega-se uma das seguintes medidas de posição (ou localização) central: média, mediana ou moda.

<br>

### Média Aritmética Simples

A medida de tendência central mais comumente usada para descrever resumidamente um conjunto de dados, tabelados ou não, é a média aritmética simples, ou simplesmente média e representa-se por $\bar{x}$. é definida como a soma das observações dividida pelo número delas.

Assim, a média amostral é dada por:

$$\overline{x} = \frac{x_1 + \ldots + x_n}{n}, \qquad \mbox{ ou, resumidamente, como } \qquad \overline{x} = \displaystyle \frac {1}{n} \sum_{i=1}^{n} x_i. $$


```r
## Comando básico para o cálculo da média geral
(média = mean(resposta))
```

```
## [1] 173.3
```

Para calcular a média por tratamento, pode-se usar o comando tapply(), que necessita dos seguintes argumentos:
`tapply(vetor de dados, fator, análise)`.

Assim

```r
## Cálculo da média por tratamento
(médias = tapply(resposta, tratamentos, mean))
```

```
##     T1     T2     T3     T4     T5 
## 105.00 152.25 141.75 211.75 255.75
```

<br>

****

### Mediana

****

A mediana, denotada por $Md$, é uma quantidade que, como a média, também procura caracterizar o centro da distribuição de frequências quando os valores são dispostos em ordem crescente ou decrescente de magnitude. 

É o valor que divide o conjunto ordenado de valores em duas partes com igual número de elementos, ou seja, 50\% das observações ficam acima da mediana e 50\% ficam abaixo.

Para calcular a mediana deve-se, em primeiro lugar, ordenar os dados para que se possa localizar a posição da mediana e assim encontrar seu valor. O número que indica a ordem ou posição em que se encontra o valor correspondente à mediana é denominado elemento mediano ($E_{Md}$).

Se o número de observações for impar, a mediana será a observação central. Se o número de observações for par, a mediana será a média aritmática das duas observações centrais.


```r
## Comando básico para o cálculo da mediana
(mediana = median(resposta))
```

```
## [1] 150
```


```r
## Cálculo da mediana por tratamento
(medianas = tapply(resposta, tratamentos, median))
```

```
##    T1    T2    T3    T4    T5 
## 105.0 149.5 141.5 210.5 254.5
```

<br>

****

### Moda

****

A moda de um conjunto de valores é definida como a realização mais frequente do conjunto de valores observados, ou seja, é o valor que apresenta a maior frequência. 

Se dois valores ocorrem com a mesma frequência máxima, cada um deles será a moda, e o conjunto se denomina **bimodal**. 

Se mais de dois valores ocorrem com a mesma frequência máxima, cada um deles é uma moda, e o conjunto é **multimodal**. 

Quando nenhum valor é repetido, o conjunto não tem moda (**amodal**). 

A moda pode ser obtida mesmo que a variável seja **qualitativa**. Os comandos para se determinar a moda são:


```r
tab = table(resposta)
(moda = names(tab)[tab == max(tab)])
```

```
## [1] "150"
```

<br>

****

### Máximo 

****

O maior valor observado no conjunto de dados.


```r
## Comando básico para o cálculo do valor máximo
(máximo = max(resposta))
```

```
## [1] 266
```


```r
## Cálculo do valor máximo para cada tratamento
(máximos = tapply(resposta, tratamentos, max))
```

```
##  T1  T2  T3  T4  T5 
## 120 165 150 220 266
```

<br>

****

### Mínimo

****

O menor valor observado no conjunto de dados.


```r
## Comando básico para valor mínimo
(mínimo = min(resposta))
```

```
## [1] 90
```


```r
## Cálculo do valor mínimo para cada tratamento
(mínimos = tapply(resposta, tratamentos, min))
```

```
##  T1  T2  T3  T4  T5 
##  90 145 134 206 248
```

<br> <br>

****

## Medidas de Dispersão

****

As medidas de dispersão servem para indicar o quanto os dados se apresentam dispersos, ou afastados, em relação ao seu valor médio, por exemplo.

<br>

****

### Amplitude Total

****

A maneira mais simples de se medir a variabilidade de uma variável é através da "distância" entre o maior e o menor valor observado em um conjunto de dados. Essa diferença é a amplitude total, denotada por $A_t$. 

Considere o conjunto de dados ordenado:
$$X_{(1)} \leq X_{(2)} \leq X_{(3)} \leq \cdots \leq X_{(n-1)} \leq X_{(n)}.$$	

A amplitude $A_t$ dos dados é dada por:

$$A_t = X_{(n)} - X_{(1)}$$

```r
(amplitude = max(resposta) - min(resposta))
```

```
## [1] 176
```

```r
# ou
(amplitude = diff(range(resposta)))
```

```
## [1] 176
```

<br>

****

### Variância Amostral

****

A medida de variabilidade mais utilizada é a variância, que é simplesmente a soma dos quadrados dos desvios, dividida pelo total de observações menos um. 

A variância de uma amostra $\left\{x_1, \ldots, x_n \right\}$ de $n$ elementos é definida por:
$$s^2 = \sum_{i=1}^n \frac{(x_i - \overline{x})^2}{n-1} \qquad \mbox{ ou } \qquad s^2 = \frac{1}{n-1} \left[ 
\sum_{i=1}^n x_i^2 - \frac{ \left( \displaystyle \sum_{i=1}^n x_i \right)^2  }{n} \right].$$


```r
## Comando básico para o cálculo da variância amostral
(variância = var(resposta))
```

```
## [1] 3090.747
```


```r
## Cálculo da variância amostral para cada tratamento
(variâncias = tapply(resposta, tratamentos, var))
```

```
##        T1        T2        T3        T4        T5 
## 166.66667  76.91667  46.91667  34.91667  76.25000
```

<br>

Algumas propriedades da variância são:

- somar (ou subtrair) um valor constante e arbitrário $c$ a cada elemento de um conjunto de números não altera a variância;

- multiplicar (ou dividir) por um valor constante e arbitrário $c$ cada elemento de um conjunto de números, a variância fica multiplicada (ou dividida) pelo quadrado da constante.

<br>

****

### Desvio-padrão Amostral

****

Observe que, devido ao fato de se elevar os desvios ao quadrado, a unidade de medida também fica elevada ao quadrado, gerando escalas sem sentido prático. Assim, caso a unidade de mensuração seja metros ($m$), a unidade de medida da variância será $m^2$.

Uma forma de se obter uma medida de dispersão com a mesma unidade de medida dos dados observados é, simplesmente, extrair a raiz quadrada da variância, obtendo-se o desvio padrão. Ele é representado por $s$. Logo,

$$ s = \sqrt{s^2} = \sqrt{\sum_{i=1}^n \frac{(x_i - \overline{x})^2}{n-1}}$$


```r
## Comando básico para Desvio-padrão amostral
(desvio = sd(resposta))
```

```
## [1] 55.59449
```


```r
## Separando por tratamento
(desvios = tapply(resposta, tratamentos, sd))
```

```
##        T1        T2        T3        T4        T5 
## 12.909944  8.770215  6.849574  5.909033  8.732125
```

<br>

****

### Coeficiente de Variação

****

A interpretação do desvio padrão depende da ordem de grandeza da variável em estudo. Assim, um desvio padrão de 10 pode ser insignificante se os valores típicos observados forem muito altos, por exemplo, em torno de 1.000; mas pode ser muito expressivo para um conjunto de dados cuja observação típica seja em torno de 100.

Logo, pode ser conveniente expressar a variabilidade dos dados de uma variável de modo **independente da sua unidade de medida** utilizada, tirando a influência da ordem de grandeza da variável. Tal medida é denominada coeficiente de variação.

O coeficiente de variação de Pearson é a razão entre o desvio padrão e a média. Em geral, o resultado é multiplicado por 100, para que o coeficiente de variação seja expresso em porcentagem. 

É dado por:

$$CV = \dfrac{s} {\overline{x} } \times 100$$


```r
## Comando para o cálculo do Coeficiente de Variação
(CV = sd(resposta) / mean(resposta)*100)
```

```
## [1] 32.07991
```

```r
# ou
(CV = desvio / média * 100)
```

```
## [1] 32.07991
```


```r
## Cálculo do Coeficiente de Variação por tratamento
(CVs = tapply(resposta, tratamentos, sd) / tapply(resposta, tratamentos, mean)*100)
```

```
##        T1        T2        T3        T4        T5 
## 12.295185  5.760404  4.832151  2.790570  3.414320
```

<br>

****

## Gerando uma Tabela com as Estatísticas

****

Pode-se construir uma única tabela com as estatísticas geradas usando-se o comando ``rbind`` ou ``cbind``. Assim,


```r
descritiva = rbind(Média = média,
                   Mediana = mediana,
                   Máximo=max(resposta),
                   Mínimo=min(resposta),
                   Amplitude=amplitude,
                   Variância=variância,
                   "Desvio-padrão"=desvio,
                   "CV(%)"=CV)
colnames(descritiva) = 'Estatísticas'
descritiva
```

```
##               Estatísticas
## Média            173.30000
## Mediana          150.00000
## Máximo           266.00000
## Mínimo            90.00000
## Amplitude        176.00000
## Variância       3090.74737
## Desvio-padrão     55.59449
## CV(%)             32.07991
```

<br>

****

## Gerando as estatísticas por tratamento:

****


```r
# Cálculo das Estatísticas por tratamento

Descritiva = cbind(Médias=round(médias, 1), 
                   Medianas=medianas,
                   Máximos=máximos,
                   Mínimos=mínimos,
                   Amplitudes=máximos - mínimos,
                   Variâncias=round(variâncias, 4), 
                   "Desvios-padrão"=round(desvios, 4), 
                   "CVs(%)"=round(CVs, 1))
Descritiva
```

```
##    Médias Medianas Máximos Mínimos Amplitudes Variâncias Desvios-padrão CVs(%)
## T1  105.0    105.0     120      90         30   166.6667        12.9099   12.3
## T2  152.2    149.5     165     145         20    76.9167         8.7702    5.8
## T3  141.8    141.5     150     134         16    46.9167         6.8496    4.8
## T4  211.8    210.5     220     206         14    34.9167         5.9090    2.8
## T5  255.8    254.5     266     248         18    76.2500         8.7321    3.4
```