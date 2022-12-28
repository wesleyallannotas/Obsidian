---
title: Trabalhando com seletores no CSS
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Como utilziar seletores da melhor forma no CSS
---

# Introdução

Seletores são as formas que temos de referenciar e adicionar CSS, adicionando os estilos nos elementos selecionados através do seletor especificado, podemos combinar seletores adicionando mais força e maior especificação em quais elementos queremos atingir, utilizando pseudo-classes podemos alterar alguns comportamentos do nosso elemento um muito conhecido é o `:hover` responsável por adicionar uma estilização especifica quando repousado o mouse sobre o elemento, E através dos pseudo-elements podemos criar elementos via CSS que adiciona apenas estilo, não alterando o documento HTML e nem trazendo dificuldades para a semântica.

# Seletores

Em inglês _selectors_, Conecta o elemento HTML com o CSS a fim de alterar o elemento

## Tipos

Temos diversas formas de selecionar nossos elementos que receberam o estilo CSS, senso eles

- Element Selector
- ID Selector
- Class Selector
- Attribute Selector
- Pseudo-class selector

```css
h1 {
  /* Todos os elementos HTML, nesse caso os <h1> */
}

#id {
  /* Um elemento que tenha o atributo id com o valor "id" */
  /* Cada id deve ser único */
}

.classe {
  /* elementos que tenha o atributo class com o valor "classe" */
  /* Classe pode se repetir nos elementos */
}

[title] {
  /* Todos os elementos que contenham um atributo title, independente do valor */
}

input[type='number'] {
  /* Elemento com atributo especifco, nesse caso elemento <input> com atributo type valor number */
}

p:hover {
  /* Pseudo-class, quando passa o mouse em cima */
}
```

## Múltiplos

Podemos agrupar múltiplos seleções as separando por virgula.

```css
h1, /* Pode ser tudo em uma linha, essa é a identação mais usada */
p,
a {
  color: tomato;
}
```

# Combinadores

Em inglês _combinators_, **buscar e combinar** seletores a fim de aplicar uma estilização.

## Descendandt Combinator

==Identificado por um espaço entre os seletores== busca um elemento dentro de outro, ou seja, buscando de maneira descendente.

```css
body article h2 {
  color: tomato;
}
```

No exemplo acima ira aplicar o estilo em todos os elementos `<h2>` que se encontram dentro de um `<article>` que por usa vez se encontra dentro de um `<body>`

```html
<body>
	<article>
		<h2>Ira aplicar!</h2>
	</article>

	<h2>Não ira aplicar!</h2>

	<article>
		<h2>Também ira aplicar!</h2>
	</article>

	<div>
		<article>
			<p>
				<h2>Também ira aplicar!</h2>
			</p>
		</article>
	</div>
</body>
```

Mesmo havendo elementos no meio do caminho também ira funcionar, só precisa seguir a ordem do combinador.

## Child Combinator

Ao contrario do _descendant combinator_ ele é mais especifico assim ==não aceitando elementos intermediários==, ou seja, apenas filhos direto, ele é identificado pelo sinal de maior `>`

```css
body > article > h2 {
  color: tomato;
}
```

Assim aplicando o estilo apenas nos `<h2>` filho direto de um `<article>` que por sua vez seja filho direto de um `<body>`

```html
<body>
	<article>
		<h2>Vai funcionar!</h2>
	</article>

	<h2>Não vai funcionar!</h2>

	<div>
		<article>
			<p>
				<h2>Não vai funcionar!</h2>
			</p>
		</article>
	</div>
```

## Adjacent Sibling Combinator

Identificado pelo sinal de `+`, tem seu funcionamento adicionando estilo ao do lado direito que for irmão direto do que se encontra do lado esquerdo, ou seja, um abaixo do outro no documento HTML

```css
div + p {
  color: tomato;
}
```

Assim selecionado o elementos `p` que é irmão direto de um elemento `div`

```html
<div>Não vai funcionar!</div>
<p>Vai funcionar!</p>
<p>Não vai funcionar!</p>
<button>Teste</button>
<p>Não vai funcionar!</p>
```

> [!tip] Dica Espaço entre botões
> Técnica muito utilizada para adicionar espaço entre botões por exemplo.
>
> ```css
> button + button {
>   margin-left: 20px;
> }
> ```

## General Sibling Combinator

Identificado pelo sinal de `~`, tem seu funcionamento diferente do [[#Adjacent Sibling Combinator]] adicionando o estilo a todos os elemento do lado direito que são irmão do que se encontra ao lado esquerdo.

```css
div ~ p {
  color: tomato;
}
```

Assim selecionado os elementos `p` que tem como irmão um elemento `div`

```html
<div>Não vai funcionar!</div>
<p>Vai funcionar!</p>
<p>Vai funcionar!</p>
<button>Teste</button>
<p>Vai funcionar!</p>
```

## Utilizando
Podemos combinar nossos combinadores com os seletores a fim de obter o resultado esperado.
```css
h2 ~ p[class="red"] {
	color: tomato;
}
```
Porem devemos tomar cuidado e usar com cautela, pois, regras muito especificas podem dificultar a reutilização