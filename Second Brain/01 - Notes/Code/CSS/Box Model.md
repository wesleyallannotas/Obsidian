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
O conceito de caixas se baseia na ideia que todo elementos HTML que não é *inline*, ou seja, em linha possui caixas que o envolvem, conceito de extrema importância para montagens layouts utilizando o CSS.
- `width, height` - Largura e Altura do elemento em si, ou seja, tamanho
- `content` - Conteúdo
- `padding` - Espaçamento interno
- `border` - Bordas
- `margin` - Margens
![[Desenho_HTMLCSS_BoxModel|center]]
>[!note] Especifico Dimensões
>Vale lembrar que em `padding`, `margin` e `border`, possuímos a liberdade para escolher o lado que queremos adicionar o estilo, seja em notação especifica, ou simplificada utilizando `shorthand` (No simplificado e atribuído no sentido horário, e caso possua uma omissão ele pega o valor do seu lado contrario), por exemplo
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

# Box-Sizing
Desrespeito a como o tamanho da caixa (box) será calculado, as opções mais conhecidas são:
- `content-box` - Valor padrão, aplica os tamanhos (`width`, `height`) definidos apenas ao conteúdo, ou seja, caso adicione um `padding` ou um `border` o tamanho real que o *box* ocupa aumenta.
- `border-box` - Mantem os tamanhos (`width`, `height`) definidos, ou seja, mesmo adicionando `border` e `padding` o tamanho real que a caixa ocupa não é impactado, pois, é retirado do espaço disponibilizado para o conteúdo

# Display `block` e `inline`
O display esta relacionado a como as caixas (*box*) se comportam em relação as outras, existem diversos tipos de valores aceitas para a propriedade display, mas como nesse caso estamos focado no `box-model`, vamos comparar os valores `inline` e `block`

| Block                                              | Inline                                                        |
| -------------------------------------------------- | ------------------------------------------------------------- |
| Ocupa toda linha                                   | Um do lado do outro                                           |
| `width` e `height` são respeitados                 | `width` e `height` não funciona                               |
| `padding`, `margin`, `border` funciona normalmente | Somente valores horizontais de `margin`, `padding` e `border` |

## Exemplos
- `block` - `<p>`, `<div>`, `<section>`, todos os headings `<h1><h2>...`, entre outras...
- `inline` - `<a>`, `<strong>`, `<span>`, `<em>`, entre outras...
