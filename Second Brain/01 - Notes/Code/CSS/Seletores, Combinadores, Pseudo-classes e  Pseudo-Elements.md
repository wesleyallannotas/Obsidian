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
- [[#Pseudo-Classes|Pseudo-class selector]]
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

section.left {
  /* Todos os elementos section, com classe left */
}

[title] {
  /* Todos os elementos que contenham um atributo title, independente do valor */
}

input[type=number] {
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
Ao contrario de [[#Descendandt Combinator]] ele é mais especifico assim ==não aceitando elementos intermediários==, ou seja, apenas filhos direto, ele é identificado pelo sinal de maior `>`
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

# Pseudo-Classes
É um tipo de seletor que traz muito poder para o nosso CSS possibilitando que selecionamos elementos em estados específicos, por exemplo o primeiro elemento dentro de uma caixa, o ponteiro do mouse esta repousando sobre o elemento, entre outros...
Pseudo-Classes começam com dois ponto `:` seguido do nome da pseudo-classe `:pseudo-class-name` ([Doc](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes))
```css
button:hover {
	color: tomato;
}
```

## Selecionando com Pseudo-Classes
Também podemos utilizar pseudo-classes para selecionar elementos específicos.

>[!attention] Atenção
>Estou usando o seletor pelo **elemento**, poremos nada impedi de usarmos outros seletor por exemplo `.class:nth-child(2)`, ou especificar mais ainda com atributos, ` input[type="text"]:nth-child(6)`

### `:first-child`
Através da *Pseudo-class* `:first-child` podemos ==selecionar o primeiro filho de um elemento exigindo que bata o seletor==
```css
ul li:first-child {
	color: tomato;
	font-weight: bold;
}
```
Será aplicado os estilos apenas no primeiro `<li>` dentro de uma `<ul>`

>[!attention] Atenção
>Porem ele precisa mesmo ser o primeiro filho, caso adicionarmos um elemento `<h3>` antes por exemplo, `<li>` deixa de ser o primeiro filho e perde seu estilo, é como se fizesse uma validação ante verificando se o elemento é mesmo o primeiro filho e depois adiciona o estilo no primeiro filho

### `:nth-of-type()`
Através da *Pseudo-class* `:nth-of-type()` podemos ==selecionar qual desejarmos daquele tipo que  satisfaça o seletor, inicia a contagem do 1==
```css
article p:nth-of-type(1) {
	color: white;
}
```
Nesse caso como passamos o valor 1 será aplicado os estilos apenas no primeiro `<p>` dentro de um `<article>` independente de qualquer ou quantos elementos irmãos anteriores existirem de outros tipos

### `:nth-child()`
Através da *Pseudo-class* `:nth-child()` podemos ==selecionar qual filho desejamos selecionar que satisfaça o seletor, inicia a contagem do 1== 
```css
article p:nth-child(1) {
	color: tomato;
}
```
Nesse caso como passamos o valor 1 será aplicado os estilos apenas no primeiro filho do `<article>` se ele for um `<p>`, ele respeita a ordem do filho, por exemplo se um elemento `<p>` for apenas o 4 filho, para aplicar efeito a ele seria necessário passar sua ordem como filho `p:nth-child(4)`

### Impares ou Pares
Utilizando como valor `even` ( Para pares) ou `odd` (Para impares) também podemos selecionar aplicando de forma alternada.
```css
ul li:nth-child(odd) {
	color: gray;
}
```
Assim nos filhos de um `<ul>` será aplicado esse estilo nos `<li>` nas posições de filhos impares.

## Ações do Usuário
Desrespeito a *pseudo-class* que são utilizadas com ações direta do usuário, por exemplo `:hover` que necessita que repouso o mouse sobre o elemento, existem diversos sendo os mais conhecidos.
- `:hover` - Ponteiro do mouse sobre o elemento.
- `:focus` - Muito utilizado por `<input />` quando o elemento esta em foco.
```css
a:hover {
	color: red;
}

input:focus {
	border: red 2px solid;
}
```

## Por Atributos
Através de *Pseudo-class* também podemos selecionar através de alguns atributos especificos.
- `:disabled` - Elementos que possuem o atributo booleano `disabled`
- `:required` - Elementos que possuem o atributo booleano `required`
```css
form input:required {
	background-color: tomato;
}

form input:disabled {
	background-color: gray;
}
```

# Pseudo-Elements
Através dos *Pseudo-Elements* podemos adicionar elementos HTML pelo próprio CSS.
*Pseudo-Elements* começa com dois pontos duas vezes `::` ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/Pseudo-elements))
- `::before` - Antes do elemento
- `::after` - Depois do elemento
- `::first-line` - Primeira linha de um texto
==É obrigatório o `content` mesmo que vazio, para que funcione==
```css
li {
	position: relative; /* Pois absolute vai no ancetral com position */
}
li::after {
	content: "";
	width: 10px;
	height: 1px;
	background-color: blue;
	position: absolute;
	bottom: 0px;
}
```
Lembre podemos misturar a fim de uma seleção mais especifica se necessário
```css
p:nth-of-type(2)::first-line {
	font-weight: bold;
}
```