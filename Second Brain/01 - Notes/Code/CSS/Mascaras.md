---
title: Mascaras
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Utilziando Mascara no CSS 
---
# Introdução
Mascaras são amplamente utilizadas no mundo do design para diversas finalidades, entre elas a possibilidade de alterar a forma original de um elemento por exemplo.
Por se tratar de uma propriedade nova é interessante sempre averiguar a forma de uso através do <https://caniuse.com>, por exemplo no momento para o funcionamento do chrome é necessário o uso de [[Vendor Prefixes]].

# Utilizando
Para uma mascara o ==transparente é o preto==, para mascaras utilizamos uma imagem e como sabemos `linear-graident()` e `redial-gradient` geram imagens então vamos construir uma imagem gradient utilizando as cores que queremos usando do preto para "furar"

```css
.card{
	mask: radial-gradient(15px, transparent 95%, black);
}

```

# Exemplo
Vamos utilizar o mesmo desafio vista com `lienar-gradient` e `radial-gradient` onde [[Cores e Background#Técnica de bordas invertida|comemos as bordas]], utilizando da ideia que ao passar da borda ele aparece o reto no lado contrario utilizaremos apenas um gradiente porem so vai funcionar  caso usado por fora geração da imagem.

```css
/* Bolinhas do meio */--mask: radial-gradient(1.2rem at 1.2rem 1.2rem, transparent 95%, black) -1.2rem -1.2rem;

/* Tecnica para tiarar borda passsando */
-webkit-mask-repeat: repeat-x;
 mask-repeat: repeat-x;
```
