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
O conceito de caixas se baseia na ideia que todo elementos HTML que não é *inline*, ou seja, em linha possui caixas que o envolvem, conceito de extrema importância para montagens layouts utilizando o CSS. ([Doc](https://developer.mozilla.org/pt-BR/docs/Learn/CSS/Building_blocks/The_box_model))
- `width, height` - Largura e Altura do elemento em si, ou seja, tamanho
- `content` - Conteúdo
- `padding` - Espaçamento interno
- `border` - Bordas
- `margin` - Margens

>[!tip] Abraçando conteúdo
>Podemos definir que nosso `content-box` abrace o conteúdo, ou seja, o seu tamanho seja relacionado com o tamanho do seu conteúdo através do valor `fit-content`
>```css
>.container {
>	width: fit-content;
>}
>```

![[Desenho_HTMLCSS_BoxModel|center]]
>[!note] Especifico Dimensões
>Vale lembrar que em `padding`, `margin` e `border`, possuímos a liberdade para escolher o lado que queremos adicionar o estilo, seja em notação especifica, ou simplificada utilizando [[Introdução ao CSS#Shorthand|shorthand]] (No simplificado e atribuído no sentido horário, e caso possua uma omissão ele pega o valor do seu lado contrario), por exemplo
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
- `border-box` - Mantem os tamanhos (`width`, `height`) definidos mesmo adicionando `border` e `padding` o tamanho real que a caixa ocupa não é impactado, pois, é retirado do espaço disponibilizado para o conteúdo
- `padding-box` - Mantem os tamanhos (`width`, `height`) definidos mesmo adicionando `padding`  porem a borda (`border`) impactado.

# Display `block` e `inline`
Os display `inline` e `block` esta relacionado a como as caixas (*box*) se comportam em relação as outras **(Posicionamento da caixa)**, existem diversos tipos de valores aceitas para a propriedade display, mas como nesse caso estamos focado no `box-model`, vamos comparar os valores `inline` e `block`

| Block                                              | Inline                                                        |
| -------------------------------------------------- | ------------------------------------------------------------- |
| Ocupa toda linha                                   | Um do lado do outro                                           |
| `width` e `height` são respeitados                 | `width` e `height` não funciona                               |
| `padding`, `margin`, `border` funciona normalmente | Somente valores horizontais de `margin`, `padding` e `border` |

## Exemplos
- `block` - `<p>`, `<div>`, `<section>`, todos os headings `<h1><h2>...`, entre outras...
- `inline` - `<a>`, `<strong>`, `<span>`, `<em>`, entre outras...

# Margens (`margin`)
Através da propriedade `margin` podemos atribuir margem as lados, sendo eles `top`, `bottom`, `left` e `right`, podemos atribuir valor aos lados individualmente ou em apenas uma declaração utilizando [[Introdução ao CSS#Shorthand|shorthand]] como explicado acima.

>[!warning] Atenção
>Cuidado com o *margin colapse*, que nada mais é do que o encontro de margens de objetos diferentes que ao invés de se somarem ==anula uma dando preferenciar a maior==, importante se atentar que *margin colapse* ==só ocorre na vertical, ou seja, quando um `margin-bottom` encontra um `margin-top`==, na horizontal a soma ocorre normalmente `margin-right` e `margin-left`

Deixando como automático centraliza o objeto aplicando margem aos lados, porem não impacta a margem vertical, ou seja
```css
div {
	margin: auto;
	/* Mesma coisa */
	margin: 0 auto;
}
```

# Espaçamento Interno (`padding`)
Através da propriedade `padding` podemos adicionar espaçamento interno no objeto, a declaração funciona da mesma forma do `margin`, existindo a possibilidade de atribuição de `padding` em um lado especifico ou utilizar o [[Introdução ao CSS#Shorthand|shorthand]]

>[!warning] Atenção
>Por padrão o `padding` impacta no tamanho da caixa (*box*), podemos mudar esse comportamento através do [[Box Model#Box-Sizing|Box Sizing]]

# Bordas (`border`)
Através da propriedade `border` podemos adicionar estilos as bordas do nosso elementos, `border` é o mais complexo em relação as anteiros, possui níveis de [[Introdução ao CSS#Shorthand|shorthand]], para o pleno funcionamento das bordas, é necessário definir o estilo da borda, cor e tamanho, a seguir segui exemplos de declarações da borda:
```css
div {
	/* Mais simplificado */
	border: solid 2px black;
	/* Medio */
	border-top: solid 2px black;
	/* Especifico */
	border-top-width: 2px;
}
```
Possuímos alguns tipos de estilos para as bordas, sendo elas:
- `solid`
- `dotted`
- `dashed`
- `double`
- `grove`
- `ridge`
- `inset`
- `outset`
Para melhor entendimento recomendo a [documentação do MDN]([border - CSS: Cascading Style Sheets | MDN (mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/CSS/border)).

>[!warning] Atenção
>Por padrão o `border` impacta no tamanho da caixa (*box*), podemos mudar esse comportamento através do [[Box Model#Box-Sizing|Box Sizing]]

# Outline
Apesar do `ouline` ser muito semelhante as bordas, diferente das propriedades anteriores, `outline` não interferi no tamanho da caixa (*box*), ele pode ser diferente de retangular, não possui a possiblidade de manipular individualmente as propriedades dos lados da caixa, possui seu uso em larga escala pelo *user agent*, principalmente para adicionar acessibilidade, podemos dizer que é um tipo de borda com comportamento de margem.

# Overflow
Através da propriedade CSS _overflow_ controlamos a aceitação de "transbordar", por exemplo por padrão é liberado, ou seja, se um elemento filho for maior que o pai, ele sai dos elemento pai, porem podemos controlar e impedir isso através do _overflow_.
- `hidden` - Não aceita "transbordar", o que passar do tamanho da caixa é ocultado.