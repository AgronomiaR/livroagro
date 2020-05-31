---
title: "Untitled"
output: html_document
---



Acessar: https://www.r-project.org/ 
 
Ir em: Download > CRAN

![](install1.png) 

Ir em: Universidade Federal do Paraná

![](install2.png) 
 
Ir em: Escolher a opção do sistema operacional do computador

![](install3.png)  

Ir em: Instalar R pela primeira vez

![](install4.png) 

![](install5.png) 

[Versões anteriores do R](https://cran.r-project.org/bin/windows/base/old/)

Executar o instalador

## Instalando RStudio

Acessar: https://www.rstudio.com/ 
 
Ir em: Download 

![](install6.png)

![](install7.png)
 
Baixar a versão do Rstudio correspondente ao seu sistema operacional

![](install8.png)

Executar o instalador.



## Primeiros passos

Abra o Rstudio

![](install9.png)
 
Ambiente Rstudio

![](install10.png)
 
Source: é seu script (Sempre construir o script aqui, nunca no console)
Console: é a saída
Dados e histórico: é onde está os dados e tudo que foi realizado durante a análise
Plots, files, packages, ajuda: é a saída gráfica, as pastas do diretório atual, os pacotes instalados e a ajuda

## Instalando packages

![](install11.png)

![](install12.png) 

![](install13.png)
 
Digitar o nome do pacote desejado e depois em “Install”.

![](install16.png) 
Toda vez que aparecer o ícone em vermelho, o Rstudio está trabalhando, dessa forma, não executar mais nada até o ícone desaparecer.
 
![](install15.png) 

## Chamando pacote no Rstudio

Função: 

`library(nome do pacote)`
`require(nome do pacote)`

nome do pacote::

Ex. library(readxl); require(readxl); readxl::

