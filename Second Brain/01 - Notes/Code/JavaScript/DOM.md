---
title: Manipulando o DOM
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [js]
description: Como manipular o DOM com o JavaScript 
---
# Introdução
DOM é uma sigla para *Document Object Model*, basicamente é um **HTML convertido** para um **objeto JavaScript**. É uma **API** (Ajuda você a interagir com alguma pessoa) que **representa e interage** com o HTML, **Estrutura de dados** do tipo **Árvore**, criada pelo browser, por se tratar de um objeto obviamente contem propriedades e métodos.
Diante disse concluímos que JavaScript usa o DOM para se conectar e manipular o HTML, assim sendo o grande responsável pela possibilitando da programação Web.
```html
<!DOCTYPE html>
<html lang="pt-BR">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Exemplo de DOM</title>
	</head>
	<body>
		<h1>DOM</h1>
	</body>
</html>
```
![[Desenho_JS_DOM|500center]]
Ocorre a relação de pai e filho, por exemplo `document` sendo pai de `body` e assim sucessivamente,  importante ressaltar que `document` é filho `window` que tem o controle de todo a tela do browser, assim o documento HTML sendo uma parte desse todo.

# Acessando Elementos
Através do DOM (*Document Object Model*) conseguimos acessar e manipular nosso documento HTML, existem diversas formas de encontrar e acessar o elemento, sendo elas

## Pelo ID
Através do método `getElementById()` podemos acessar o nosso elemento através do ID que ele possui.
```html
<body>
	<div id="cart"></div>
</body>
```
```js
document.getElementById('cart');
```

## Pela Classe
Através do método `getElementsByClassName()` podemos acessar o nosso(s) elemento através da classe que ele possui, `Elements` se encontra no ==plural pois espera-se que a classe possa se repetir==, onde caso exista mais de um traz um objeto do tipo `HTMLCollection` contendo todos os elementos com a classe requerida.
```html
<body>
	<div class="container"></div>
	<div class="container"></div>
</body>
```
```js
document.getElementsByClassName('container');
```

## Pela Tag
Através do método `getElementsByTagName()` podemos acessar o nosso(s) elementos através do nome da *tag*, `Elements` se encontra no ==plural pois espera-se que a tag possa se repetir==, onde caso exista mais de um traz um objeto do tipo `HTMLCollection` contendo todos os elementos com a *tag* requerida 
```html
<body>
	<div></div>
	<div></div>
</body>
```
```js
document.getElementsByClassName('div');
```

## Pelo Seletor
Através do método `querySelector()` podemos acessar o nosso elemento através do seletor CSS, ==retorna o primeiro que encontrar==.
```html
<body>
	<div id="cart"></div>
	<div class="container"></div>
	<input required />
	<div></div>
</body>
```
```js
document.querySelector('#cart');
document.querySelector('.container');
document.querySelector('[required]');
document.querySelector('div');
document.querySelector('body div:nth-child(2)');
```
Podemos utilizar o `querySelectorAll` para trazer todos correspondendo com o seletor especificado retornando uma `NodeList` contendo todos.
```html
<body>
	<div></div>
	<div></div>
</body>
```
```js
document.querySelectorAll('div');
```

## Diferença Entre `HTMLCollection` e `NodeList`
Uma da diferença mais perceptível é que `NodeList` aceita realizar um `forEach` já `HTMLCollection` não.
```js
elements.forEach(el => console.log(el))
```

# Manipulando Conteúdo
Através do DOM (*Document Object Model*) podemos manipular o conteúdo dos nossos elementos, sendo possível realizar através das seguintes formas.

## Conteúdo Texto
Podemos **alterar e visualizar** o texto do conteúdo do nosso elemento através do `textContent`, que retorna o texto **com** formatação, incluindo o texto oculto pelo CSS, bem como as quebras de linha (`\n`) e **sem** elementos HTML
```js
const element = document.getElementById('title');
element.textContent = "Adicionar elemento por aqui não funciona <br/> viu";
console.log(element.textContent);
```
Vale ressaltar que tudo que atribuímos ao `textContent` será tratado única e exclusivamente como texto, ou seja, se inserirmos elementos HTML será tratado como texto.

## Texto Interno
Podemos **alterar e visualizar** o texto interno do nosso elemento através do `innerText` que retorna o texto **sem** formatação e elementos HTML
```js
const element = document.getElementById('title');
element.innerText = "Adicionar elemento por aqui não funciona <br/> viu";
console.log(element.innerText);
```
Vale ressaltar que tudo que atribuímos ao `innerText` será tratado única e exclusivamente como texto, ou seja, se inserirmos elementos HTML será tratado como texto.

## HTML Interno
Podemos **alterar e visualizar** o HTML interno do nosso elemento através do `innerHMTL` que retorna o texto **com** formatação e elementos HTML
```js
const element = document.getElementById('title');
element.innerHTML = "Adicionar elemento por aqui FUNCIONA </br> quebrou a linha";
console.log(element.innerHTML)
```
Vale ressaltar que elementos HTML atribuídos pelo `innerHTML` terão efeitos e serão intendidos como elementos HTML.

## Valor do Elemento Input
podemos **alterar e visualizar** o valor de um elemento vazio `<input />` através do `value`.
```js
const element = document.getElementById('tel');
element.value = "18997386518";
console.log(element.value);
```

# Manipulando Atributos
Através do DOM (*Document Object Model*) podemos manipular os atributos dos nossos elementos, sendo possível realizar através das seguintes formas.

## Atribuir ou Alterar
Podemos **alterar ou adicionar** um atributo através do método `setAttribute(atributo, valor)`.
```html
<body>
	<input type="number" required />
</body>
```
```js
const element = document.querySelector('input');
element.setAttribute('class', 'input-weight'); // Adicionando Classe
element.setAtribute('type', 'text'); // Alterando
```

## Pegando Valor
Podemos **visualizar** o valor de um atributo através do método `getAttribute()`.
```html
<body>
	<input type="number" >
<body>
```
```js
const element = document.querySelector('input');
console.log(element.getAttribute('type')); // Retorno: number
```

## Remover
Podemos **remover** um atributo através do método `removeAttribute()`.
```html
<body>
	<div class="title" >
<body>
```
```js
const element = document.querySelector('div');
console.log(element.removeAttribute('class'));
```

# Alterando Estilos
Através do DOM (*Document Object Model*) podemos manipular o estilo dos nossos elementos, sendo possível realizar através das seguintes formas.

## Em linha
Através do propriedade `style` podemos **visualizar, adicionar e alterar** o CSS em linha, ou seja, adicionar CSS em um atributo `style` que ficara no nosso elemento, podendo adicionar direto um `string` contendo o CSS, ou o **mais recomendado** a partir de propriedades.
```js
const element = document.querySelector('.div');
element.style = 'background-color: black;'; // Não é recomendado
element.style.backgroundColor = 'red';
console.log(element.style.backgorundColor);
```

## Manipulando Classes
Através do método `classList` podemos **visualizar, adicionar, alterar, entre outras diversas funções presente no seu [[Manipulando Dados#Prototype|prototype]]** para manipulação de classes, assim por consequência conseguimos manipular seu estilo, retorna um objeto do tipo  `DOMTokenList`

### Adicionando
Através do método `add()` podemos adicionar classes ao nosso elemento, caso necessita adicionar mais de uma basta separar por virgula.
```js
const element = document.querySelector('div');
element.classList.add('title', 'main');
```

### Removendo
Através do método `remove()` podemos remover classes do nosso elemento, caso necessita remover mais de uma basta separar por virgula.
```js
const element = document.querySelector('div');
element.classList.remove('title', 'main');
```

### Alterar
Através do método `toggle()` podemos alterar a existência da classes no nosso elemento, caso já exista no atributo `class` **remove**, caso não esteja **adiciona**, caso necessário podemos realizar a ação com mais basta separar por virgula.
```js
const element = document.querySelector('div');
element.classList.toggle('title', 'main');
```

# Navegando Pelas Elementos