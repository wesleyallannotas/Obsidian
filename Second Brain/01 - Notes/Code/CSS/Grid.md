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

# `grid-template-areas`
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

# `grid-template-rows`
Podemos definir o tamanho das linhas, ou seja, alterar a altura ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/grid-template-rows)), por exemplo:
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

# `grid-template-columns`
Podemos definir o tamanho das colunas, ou seja, alterar a largura ([Doc](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-columns)), por exemplo:
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