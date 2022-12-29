---
title: Criando layout usando flexbox
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Como criar layouts usando flexbox 
---
# Introdução
Quando definimos a propriedade `display` de um elemento como `flex` temos aceso as propriedades `flex` para o controle do comportamento dos elementos internos desse elemento pai **(Posicionamento dentro da caixa)**, facilita o posicionamento, ordenação e a responsividade criando regras para alteração das dimensões dos elementos. ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox))
```css
.container {
	display: flex;
}
```

# Terminologia
- **Flex container** - Elemento pai, o que possui a propriedade `display` com o valor `flex`
	- **Flex item** - Elementos filhos
- **Nesting** - Elemento que contem outros elementos
- **Axis** - Em português eixo
	- **Main** - Principal, em coluna seria o Y em linha seria o X
		- **Start**, **End** - Inicio e final
	- **Cross** - Cruzado, o eixo que cruza o principal
		- **Start**, **End** - Inicio e final
- **Flex sizing** - Flexível, Altera width/height dos itens para preenchimento dos espaços do flex container

# Propriedades do Flex Container
Ao adicionar o valor `flex` ao `display` de um elemento, o tornamos um *Flex container*, e com isso temos acesso as propriedades do *flex container*, tendo acesso a manipulação da
- Direção dos itens
- Multilinhas
- Alinhamento
	- Principal
	- Cruzado
- Espaço entre os itens

# CONTINUAR DAQUI


# `order`
Através da propriedade `order` podemos alterar a ordem dos elemento filho selecionado.
```css
.item:nth-child(2) {
	order: 1;
}
```
  
# `flex-direction`
Através da propriedade `flex-direction` podemos alterar a direção dos elementos ([Doc)](https://developer.mozilla.org/pt-BR/docs/Web/CSS/flex-direction)), podemos utilizar os seguintes valores:
- `row` - Em linha, se posicionando um ao lado do outro
- `column` - Em coluna, se posicionando um abaixo do outro
- `row-reverse` - Em linha e inverte a ordem, se posicionando um ao lado do outro
- `column-reverse` - Em coluna e inverte a ordem, se posicionando um abaixo do outro

# `justify-content`
Desrespeito a como ira distribuir os elementos internos ([Doc](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content)), Alguns valores aceitos são:
- `start` 
- `center`
- `space-between` - Espaço entre os elementos, mantendo a proporção responsiva.
- `space-around`
- `space-evenly`
- Entre outros...

# `align-items`
A propriedade CSS **`align-items`** ==estabelece o valor [[#`align-self`|align-self]] em todos filhos diretos como um grupo==. A propriedade `align-self` estabelece o alinhamento de um certo item dentro do bloco que o contém. ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/align-items))
Alguns valores aceitos;
- `stretch`
- `center`
- `start`
- `end`
- Entre outros...

# `align-self`
A propriedade CSS `align-self` alinha `itens-flex` da linha flex alvo ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/align-self))
- `stretch`
- `center`
- `start`
- `end`
- Entre outros...