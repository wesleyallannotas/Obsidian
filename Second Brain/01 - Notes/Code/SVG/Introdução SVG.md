---
title: Introdução SVG
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [svg]
description: Entenda o que é svg. 
---
# 🚀 Introdução
SVG é a abreviatura de _Scalable Vector Graphics_ que pode ser traduzido do inglês como **gráficos vetoriais escalonáveis**. Trata-se de uma linguagem XML para descrever de forma vetorial desenhos e gráficos bidimensionais, quer de forma estática, quer dinâmica ou animada

# 🏗️ Criando
Para criarmos um SVG iniciamos com um elemento de mesmo  nome `<svg></svg>`, onde através de atributos passaremos informações sobre todo o SVG, por exemplo posicionamento e dimensões do elementos através do atributo `viewBox`.
Dentro do mesmo criaremos os elementos e formas geométricas passando informações para a contrução.
- `viewBox` - Passaremos em consecutivamente os seguintes valores posição no eixo x, posição no eixo y, largura e altura, importante adicionar o tamanho das bordas no mesmo.

>[!attention] Comportamento
>Diferente do HTML que por padrão posiciona um elemento abaixo do outro, o SVG empilha em na frente do outro.

```html
<svg viewBox="0 0 232 230">
	{ ... }
</svg>
```

## ⭕ Círculos
Podemos criar círculos facilmente através do elemento vazio `<circle />` onde através de propriedades passamos informações sobre o mesmo.
- `cx` - Posicionamento dentro no eixo X dentro da `viewBox`.
- `cy` - Posicionamento dentro no eixo Y dentro da `viewBox`.
- `r` - Raio da circunferência.
- `fill` - Cor de preenchimento, basta informar `none` caso queira vazio.
- `opacity` - Opacidade.
- `stroke` - Bordas

# 📋 Definições
Podemos definir informações que utilizaremos no nosso SVG, como por exemplo um gradiente, conseguimos por meio do elemento `<defs></defs>`.

## Gradiente Linear
Podemos definir um gradiente linear através do elemento `<linearGradient>`, muito importante informar um Id, pois é através do mesmo que o conectaremos aos elementos SVG.

```html
<linearGradient
	id="paint0_linear_201_85"
	x1="-9"
	y1="82"
	x2="145"
	y2="178"
	gradientUnits="userSpaceOnUse"
>
	<stop stop-color="#CE9FFC" />
	<stop offset="1" stop-color="#7367F0" />
 </linearGradient>
```