---
title: Criando layout com Grid
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Criando layout para página utilizando grid 
---
# Introdução
Através da propriedade CSS `display` podemos atribuir o valor `grid` assim podendo utilizar todos as propriedades do Grid para poder construir nosso layout, parte da ideia de criar um Grid onde podemos posicionar e definir tamanho a partir do mesmo **(Posicionamento dentro da caixa)**, pode ser flexível ou não. ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/grid))

>[!tip] Centralizando uma div
Utilziando `grid` conseguimos tal feito facilmente através da propriedade `place-items`
>```css
>body {
>	display: grid;
>	place-items: center;
>}
>```

# Definindo Áreas
Através da propriedade `grid-template-areas` podemos definir o funcionamento do nosso grid de forma extremamente simples atribuindo nomes de nossa escolha ([Doc](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-areas)), por exemplo

```css
body {
	display: grid;
	grid-template-areas:
		"header header"
		"main aside"
		"footer footer";
}
```

O nome utilizado não precisa ser o nome do elemento podemos escolher qualquer nome, e para ligar o elemento a o nome da área utilizamos o elementos `grid-area` ([Doc](https://developer.mozilla.org/en-US/docs/Glossary/Grid_Areas)), por exemplo

```css
header {
	grid-area: header;
}
main {
	grid-area: main;
}
aside {
	grid-area: aside;
}
footer {
	grid-area: footer;
}
```

# Definindo Inicio e Fim
Outro forma de posicionar os blocos no grid é definir manualmente posição de inicio e fim dentro das colunas (_column_) e linhas (_row_), se iniciando de 1 (Ao contrario de _arrays_ que inicia do 0).

```css
.container {
	display: grid;
	grid-row-start: 1;
	grid-row-end: 2;
	grid-row: 1/2; /* start/end */
	grid-column-start: 1;
	grid-column-end: 3;
	grid-column: 1/3; /* start/end */
}
```

# Tamanho das Linhas
Através da propriedade `grid-template-rows` podemos definir o tamanho das linhas, ou seja, alterar a altura ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/grid-template-rows)), por exemplo:

```css
body {
	display: grid;
	grid-template-areas:
		"header header"
		"main aside"
		"footer footer";
	grid-template-rows: 30px 1fr 40px;
}
```

# Tamanho das Colunas
Através da propriedade `grid-template-columns` podemos definir o tamanho das colunas, ou seja, alterar a largura ([Doc](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-columns)), por exemplo:

```css
body {
	display: grid;
	grid-template-areas:
		"header header"
		"main aside"
		"footer footer";
	grid-template-rows: 30px 1fr 40px;
	grid-template-columns: 1fr 80px;
}
```

# Fração
Através do `fr` podemos definir a quantidade de frações do espaço disponível que tal elemento ira ocupar, por exemplo.

```css
.container {
	display: grid;
	grid-template-rows: 1fr 2fr 1fr;
}
```

O primeiro elemento ira ocupar uma fração, o segundo elemento duas frações e o terceiro uma.

# Tamanho Máximo do Conteúdo
Através do valor `max-content` podemos definir que os elementos terão o tamanho máximo do conteúdo.

>[!example] Diferença com fração
>Fração é em relação ao tamanho total disponível, `max-content` é relacionado ao tamanho do conteúdo.

```css
.container {
	display: grid;
	grid-template-rows: max-content max-content max-content;
}
```

# Eliminando Repetições
Através do `repeat`. função  CSS que podemos utilizar para encurtar nossas declarações, evitando reescrita e facilitando por consequência a manutenção, podendo haver mais de uma em apenas uma declaração.

```css
#calculator {
	display: grid;
	grid-template-columns: repeat(4, 1f);
}
```

Ou seja repetira `1fr` quatro vezes.

# Gap
Assim como no [[Flexbox#gap|flexbox]] podemos definir espaçamento entre os elementos através da propriedade `gap`, sendo a mesma um [[Introdução ao CSS#Shorthand|shorthand]] das seguintes propriedades.
- `row-gap` - Distancia dos elementos em linha.
- `column-gap` - Distantes dos elementos em colunas.

```css
#calculator {
	display: grid;
	grid-template-columns: repeat(4, 1f);
	gap: 2rem;
	column-gap: 2rem;
	row-gap: 2rem;
}
```

# Alinhando Conteúdo
Existem diversas propriedades que podemos utilizar para poder acomodar da melhor forma o conteúdo do nosso elemento com _display_ grid e  o conteúdo dos filhos do seu conteúdo.

## Eixos
Podemos definir que em relação ao _display_ grid
- `justify` - Eixo por padrão principal no [[Flexbox]], no grid controla o Horizontal
- `align` - Eixo cruzado por padrão no [[Flexbox]], no grid controla o Vertical
## Justify Content
Através da propriedade `justify-content` que tem seu uso no [[Grid]] e no [[Flexbox]] (Porem com impactos diferentes), tem como objetivo ==alinhar e distribuir os elementos internos do grid== em relação ao [[#Eixos|eixo]] principal, alguns valores aceitos são:
- `start` - Valor Padrão , inicio do eixo principal
- `end` - Final do eixo principal
- `center` - Centraliza no eixo principal
- `space-between` - Espaço entre os elementos, mantendo a proporção responsiva.
- `space-around` - Espaço ao redor igual
- `space-evenly` - Espaço por igual
- Entre outros...

>[!attention] Diferença
>Pode trazer um resultado diferente com o grid, pois ,o grid respeita as colunas e linhas definidas, por exemplo.
>![[Desenho_CSS_GridXFlexbox_JustifyContent]]

## Justify Items
Através da propriedade `justify-items` podemos controlar todos os [[#Justify Self]] dos nossos elementos filhos de uma só vez.

>[!fail] Sobre Flexbox
>Essa propriedade é ignorado quando usado com Flexbox.

## Justify Self
Através da propriedade `justify-self` podemos controlar o alinhamento no [[#Eixos|eixo]] principal do conteúdo dos elementos filhos, essa propriedade é exclusiva de elementos filhos de elementos do display  [[Grid]] ([Doc](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-self))
- `scretch` - Se expande, preenche o espaço em todas direções
- `center` - Conteúdo no centro, ocupando e espaço do conteúdo exatamente.
- `start` - Conteúdo colado no inicio (padrão esquerda), ocupando e espaço do conteúdo exatamente.
- `end` - Conteúdo colado no final (padrão direita), ocupando e espaço do conteúdo exatamente.

>[!fail] Sobre Flexbox
>Essa propriedade é ignorado quando usado com Flexbox.

## Diferença Content e Items
Basicamente o `content` controla em relação ao lado de fora do elemento, ou seja, ao _container_ do Grid, já o `items` controle em relação ao espaço interno, definido pelo `grid-template-columns`
![[Desenho_CSS_GridXFlexbox_ContentItems]]

## Align Content
Através da propriedade `align-content` podemos controlar o alinhamento de todo de todo o _grid_ do nosso elemento em relação ao [[#Eixos|eixo]] cruzado, aceita valores como.
- `start`
- `end`
- `center`
- Entre outros..

## Align Items
Através da propriedade `align-items` podemos definir um [[#Align Self]] para todos os elementos filhos do grid de uma só vez.

```css
.container {
	display: grid;
	align-items: center;
}
```

## Align Self
Através da propriedade `align-self` que é uma propriedade disponível para os filhos dos elementos com _display_ [[Grid]] ou [[Flexbox]], podemos alinhar o conteúdo em relação ao espaço disponível dentro do _grid_ (no caso de _display_ grid) que ele se encontra, caso o espaço do _grid_ for maior que o elemento, na direção do [[#Eixos|eixo]] contrario (cross).
- `start`
- `end`
- `center`
- Entre outros.

## Place Content
Através da propriedade `place-content` que é um [[Introdução ao CSS#Shorthand|shorthand]] para `justify-content` e `align-content` podemos definir valores para os mesmo com apenas uma declaração

```css
body {
	place-content: center end; /* align-content justify-cotent */
	place-content: center;
}
```

## Place Items
Através da propriedade `place-items` que é um [[Introdução ao CSS#Shorthand|shorthand]] para `justify-items` e `align-items` podemos definir valores para os mesmo com apenas uma declaração

```css
body {
	place-items: center end; /* align-items justify-items */
	place-items: center;
}
```