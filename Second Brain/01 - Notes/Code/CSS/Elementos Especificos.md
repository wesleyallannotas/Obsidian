---
title:
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Como estilizar elementos especificos do HTML
---
# Select
Como sabemos o elemento [[Formulário#Entrada de Dados com `<select>`|<select>]] possui um ícone para colapsar as opções que são definidas com `<option>`, normalmente para seguir o designer definida para a página, é necessário alterar esse ícone, podendo ser feito de diferentes formas.

## Removendo CSS
Podemos remover o CSS padrão injetado pelo _browser_ através da propriedade [[Introdução ao CSS#Eliminando todo CSS do Browser|all]] e adicionar uma imagem ao lado no HTML.

```css
select {
	all: unset;
}
```

```html
<fieldset>
	<select>
		<!-- Opções -->
	</select>
	<img src="icone" />
</fieldset>
```

## Alterando o ícone
Podemos remover o ícone através da propriedade `appearance`, e adicionar uma imagem que não deve se repetir e posicionar onde quiser, normalmente posicionado na direita.

```css
select {
	appearance: none;
	background: url(src/assets/svg/chevron-down.svg) no-repeat right center;
}
```

## Adicionando um Pseudo-Element
Utilizando a ideia de [[Seletores, Combinadores, Pseudo-classes e  Pseudo-Elements#Pseudo-Elements|Pseudo-Elements]] temos mais flexibilidade do que [[#Alterando o ícone]] através e um _background_ dentro do próprio `<fildset>` ou elemento pai, pois `<select>` e `<input>` não aceita pseudo-elements.

```css
fildset::after {
	content: '';
	background: url(src/assets/svg/chevron-down.svg) no-repeat center;
}

fieldset:hover::after {
	rotate: 90deg;
}
```