---
title: Box Model no CSS
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Funcionamento do box model utilizando CSS e HTML 
---
# Introdução
O conceito de caixas se baseia na ideia que todo elementos HTML que não é *inline*, ou seja, em linha possui caixas que o envolvem.
- `width, height` - Largura e Altura do elemento em si
- `padding` - Espaçamento interno
- `border` - Bordas
- `margin` - Margin
![[Desenho_HTMLCSS_BoxModel|center]]
>[!note] Especifico Dimensões
>Vale lembrar que em `padding`, `margin` e `border`, possuímos a liberdade para escolher o lado que queremos adicionar o estilo, seja em notação especifica, ou simplificada (No simplificado e atribuído no sentido horário), por exemplo
>```css
>.container {
>	/*Simplificado*/
>	padding: 10px; /*Aplica 10px em todas os lados*/
>	padding: 10px 5px; /*Aplica 10px top e bottom, 5px left e rigth*/
>	padding: 10px 5px 3px; /*Aplica 10px top, 5px left e right, 3px bottom*/
>	padding: 10px 5px 2px 1px /*Aplica 10px top, 5px rigth, 3px bottom e 1px left*/
>	/*Especifico*/
>	padding-bottom: 10px;
>}
>```

