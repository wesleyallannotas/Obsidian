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
- [[#Direção dos Itens]]
- [[#Multilinhas]]
- [[#Alinhamento]]
	- Principal
	- Cruzado
- [[#Espaço Entre os Elementos]]

## Direção dos Itens
O *Flex* possui uma direção sendo ela horizontal ou vertical, que temos a liberdade de trocar a nossa vontade através da propriedade [[#`flex-direction`|flex-direction]].

## `flex-direction`
Através da propriedade `flex-direction` podemos alterar a direção dos elementos, por padrão é em linha, ou seja, a propriedade tem o valor `row` atribuido ([Doc)](https://developer.mozilla.org/pt-BR/docs/Web/CSS/flex-direction)), podemos utilizar os seguintes valores:
- `row` - Em linha, se posicionando um ao lado do outro
- `column` - Em coluna, se posicionando um abaixo do outro
- `row-reverse` - Em linha e inverte a ordem dos itens e direção do eixo trocando o `start` pelo `end`, ou seja o final da linha se torna  `start`, se posicionando um ao lado do outro
- `column-reverse` - Em coluna e inverte a ordem dos itens e a direção do eixo trocando o `start` pelo `end`, ou seja o final da coluna se torna , se posicionando um abaixo do outro

## Multilinhas
O *Flex* possui a possibilidade de usar multilinha ==criando praticamente outros eixos respeitando a direção do eixo principal==, como se fosse um novo *Flex container* através do `flex-wrap`

### `flex-warp`
Através da propriedade `flex-warp` podemos possibilitar que "Quebre a linha" quando for necessário. Por padrão as dimensões dos *Flex itens* é totalmente flexível não ocorrendo nunca essa "Quebra", quando atribuímos o valor `warp` para a propriedade `flex-warp`, ele "Quebra" quando não for possível manter todos no mesmo eixo
- `wrap-reverse` - Inverso, "Quebrando" para cima caso em linha, para esquerda caso em coluna
- `wrap` - Normal, "Quebrando" para baixo caso em linha, para direita caso em coluna
```css
.box {
	display: flex;
	flex-wrap: wrap;
}
.box div {
	width: 80px;
}
```
No exemplo acima os elementos *flex item* desse HTML imaginário são todos `<div>`, com esse estilo, todos possuíram `80px` e quando não couber "Quebra" para linha de baixo.

>[!tip] Dica mantendo responsivo
Podemos utilizar uma melhor forma para atribuir dimensões para manter flexível até certo ponto e quando atingir um mínimo quebrar.

## `flex-flow`
A propriedade `flex-flow` é um [[Introdução ao CSS#Shorthand|shorthand]] que possibilita atribuir valor para as propriedades [[#`flex-direction`|flex-direction]] e [[#`flex-warp`|flex-wrap]], podemos utilizar para atribuir apenas em uma ou em ambas, quando enviado apenas um valor ele consegui identificar para qual propriedade é o valor
```css
.container {
	display: flex;
	flex-flow: row wrap;
	/* flex-flow: wrap; */
}
```

## Alinhamento
O *Flex* traz propriedades para o *Flex container* que facilita  o alinhamento dos nossos *Flex Itens*

### `justify-content`
Desrespeito a como ira alinhar e distribuir os elementos internos do *Flex container* em relação ao eixo principal (main) ([Doc](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content)), Alguns valores aceitos são:
- `flex-start` - Valor Padrão , inicio do eixo principal
- `flex-end` - Final do eixo principal
- `center` - Centraliza no eixo principal
- `space-between` - Espaço entre os elementos, mantendo a proporção responsiva.
- `space-around` - Espaço ao redor igual
- `space-evenly` - Espaço por igual
- Entre outros...

### `align-items`
Desrespeito a como ira alinhar os elementos internos do *Flex container* em relação ao eixo cruzado (cross). A propriedade CSS **`align-items`** ==estabelece o valor [[#`align-self`|align-self]] em todos filhos diretos como um grupo==. A propriedade `align-self` estabelece o alinhamento de um certo item dentro do bloco que o contém. ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/align-items))
Alguns valores aceitos;
- `stretch` - Valor padrão, esticar, ou seja, se estica no eixo cruzado
- `center` - Centraliza no eixo cruzado
- `flex-start` - Inicio do eixo cruzado
- `flex-end` - Final do eixo cruzado
- Entre outros...

## Espaço Entre os Elementos
O *Flex* traz propriedades para o *Flex container* que facilita a definição de espaços entre os nossos *Flex Itens*

### `gap`
Através da propriedade `gap` no nosso *flex container* podemos definir os ==espaços entre os nossos *flex itens*== passando como valor unidades de medidas [[Valores e Unidades de Medidas#Distancias Absolutas|absoluta]] ou [[Valores e Unidades de Medidas#Distancias Relativas|relativa]]
```css
.container {
	display: flex;
	gap: 2px;
}
```

# Propriedades do Flex Item
Ao adicionar o valor `flex` ao `display` de um elemento, o tornamos um *Flex container*, por consequência seus filhos se tornam *Flex item* onde temos acessos a  algumas propriedades para eles
- [[#`flex-basis`|Flex-basis]] - Mudar o tamanho do item
- [[#`flex-grow`|Flex-grow]] - Se adapta crescendo automaticamente
- [[#`flex-shrink`|Flex-shrink]] - Encurtar, comprimir, dependendo do tamanho da caixa
- [[#`flex`|Flex]] - [[Introdução ao CSS#Shorthand|Shorthand]] para [[#`flex-basis`|flex-basis]], [[#`flex-grow`|flex-grow]] e [[#`flex-shrink`|flex-shrink]] 
- [[#`order`|Order]] - Controla a ordem do *flex item* dentro do *flex container*
- [[#`align-self`|Align-Self]]

## `flex-basis`
Controla a largura (`width`) quando o eixo principal for em linha ou controla a altura (`height`) quando o eixo principal for em coluna dos *flex itens*.
- `auto` - Valor padrão.
- `0` - Tamanho do conteúdo, sendo diferente de `auto` não se altera com `width`
- Valores como unidades de medidas absolutas ou relativas
>[!attention] Atenção ao eixo principal
>O eixo principal definido por [[#`flex-direction`|flex-direction]] determina qual dimensão [[#`flex-basis`|flex-basis]] ira controlar
```css
.container div {
	flex-direction: row;
	flex-basis: 25%;
}
.container div:nth-child(1) {
	width: 250px;
}
```
Quando o `flex-basis` possui um valor diferente de `auto`, ==perdemos a possibilidade de alterar a largura== pela propriedade `width`, tornando ele o responsável por controlar essa dimensões.

## `flex-grow`
A propriedade `flex-grow` que esta disponível para os *flex itens*, possibilita ==controlar o crescimento do item dentro do container em relação aos espaços vazios==, o valor padrão é `0` assim não "Crescendo", o valor que passamos e como se fosse "Pega N frações do espaço disponível"
>[!attention] Atenção ao eixo principal
>O eixo principal definido por [[#`flex-direction`|flex-direction]] determina qual dimensão [[#`flex-grow`|flex-grow]] ira controlar
```css
.container {
	display: flex;
}
.container .item:nth-child(2), 
.container .item:nth-child(3) {
	flex-grow: 1;
}
.container .item:nth-child(1) {
	flex-grow: 2;
} 
```
No caso acima o *flex item* `.item:nth-child(1)` ocupara duas frações, ou seja, duas vezes maior que o filho 2 e 3.

## `flex-shrink`
A propriedade `flex-shrink` que esta disponível para os *flex itens*, possibilita ==controlar o encolhimento do item dentro do container==, por padrão todos os *flex item* possui a propriedade `flex-shrik` com valor `1`, assim encolhendo para caber na caixa. ([Doc](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-shrink))
- `0` - Atribuindo o valor `0`, ele não encolhe mais, podendo ate empurrar os outros para fora caso não caiba
- Valores acima vai encolhendo mais dando mais espaço para os valores mais baixos, no caso se adicionar valor 2 a um *flex item* e 1 em todos os outros, dependendo do `flex-basis` se existir ou da dimensão do eixo ele fica com o tamanho apenas do conteúdo
>[!attention] Atenção ao eixo principal
>O eixo principal definido por [[#`flex-direction`|flex-direction]] determina qual dimensão [[#`flex-grow`|flex-grow]] ira controlar
```css
.container {
	display: flex;
}
.item {
	flex-basis: 50px;
}
.item:nth-child(2),
.item:nth-child(1) {
	flex-shrink: 1;
}
.item:nth-child(3) {
	flex-shrink: 2;
}
```
Esse é o mais confuso que necessita de mais testes e leitura da documentação para entender

## `flex`
A propriedade `flex` é um [[Introdução ao CSS#Shorthand|shorthand]] para as propriedades [[#`flex-grow`|flex-grow]], [[#`flex-shrink`|flex-shrink]] e [[#`flex-basis`|flex-basis]] dos *flex item*, pode possuir 1, 2 ou 3 valores, normalmente seguinte a ordem *grow*, *shrink* e *basis*
- 1 Valor - Quantos passamos para a propriedade [[Introdução ao CSS#Shorthand|shorthand]] `flex` apenas o valor 1 ele preenche da seguinte forma
```css
.container .item {
	flex: 1;
	/* grow: 1 ; shrink: 1 ; basis: 0*
}
```
- 2 Valore com um sendo unidade de medida - Ele entende que a unidade de medida desrespeito ao `flex-basis`

### Exemplo
Preferencia para atingir os `120px` do segundo, com os sendo flexíveis com o primeiro pegando 2/3 e o ultimo 1/3
```css
main section:nth-child(1) {
	flex: 2;
}

main section:nth-child(2) {
	flex: 0 120px;
}

main section:nth-child(3) {
	flex: 1;
}
```

## `order`
Através da propriedade `order` podemos alterar a ordem dos *flex itens*, por padrão todos possuem valor `0`, causa alterações visuais apenas.
```css
.item:nth-child(2) {
	order: 1;
}
```

## `align-self`
A propriedade CSS `align-self` alinha `itens-flex` da linha flex alvo ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/align-self))
- `stretch`
- `center`
- `start`
- `end`
- Entre outros...