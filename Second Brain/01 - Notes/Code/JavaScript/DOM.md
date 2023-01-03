---
title: Manipulando o DOM
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
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
>[!note] Performance
>Alguns estudos mostram que pelo ID é um pouco mais rápido do que os outros métodos, porem por ser uma diferença muito pequena é algo a se atentar apenas em grandes projetos.
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
A diferença mais perceptível no inicio é que `NodeList` aceita realizar um `forEach` já `HTMLCollection` não.
```js
elements.forEach(el => console.log(el))
```
Olhando mais a fundo podemos perceber que `NodeList` traz uma lista de [[#Diferença entre `Node` e `Element`|Nodes]] e o `HTMLCollection` traz um coleção de [[#Diferença entre `Node` e `Element`|Elements]]

# Diferença entre `Node` e `Element`
`Node` é uma *interface* e o `Element` é apenas uma implementação desta *interface* assim possuindo todas suas propriedades e métodos herdadas, porem `Node` não se limita apenas a Elementos HTML assim existindo, ([NodeTypes](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType)) `text_node`, `document_type_note` (*doctype html*), até mesmo os comentários e o próprio `document`, ou seja, podemos perceber que `node` engloba mais coisas que o `element` que por sua vez é um implementação do `node` ([Node](https://developer.mozilla.org/pt-BR/docs/Web/API/Node)), ([Element](https://developer.mozilla.org/pt-BR/docs/Web/API/Element))
==**Importante aprimorar**==

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
Podemos navegar entre os elementos através da API do DOM (*Document object Model*) nos disponibiliza

## Elementos Pais
Através do  `parentNode` podemos **acessar o nó pai** ([[#Diferença entre `Node` e `Element`|Node]]) do nosso elemento selecionado, já através do  `parentElement` podemos **acessar o elemento pai** ([[#Diferença entre `Node` e `Element`|Element]]) do nosso elemento selecionado.
>[!note] Diferenças
>Parent Element retorna `null` se o pai não for um nó de elemento, que é a principal diferença entre parentElement e parentNode. Em muitos casos, pode-se usar qualquer um deles; na maioria dos casos, são iguais. Por exemplo:
>```js
>// Retorna o nó do documento
>document.documentElement.parentNode; 
>// Retorna nulo
>document.documentElement.parentElement; 
>```
>O elemento HTML (document.documentElement) não tem um pai que é um elemento, é um nó, portanto, o elemento pai é nulo.

## Elementos Filhos
Através de um elemento podemos navegar para os seus filhos das seguintes formas

### `childNodes`
Através do  `childNodes` ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/API/Node/childNodes)) podemos **acessar todos os nós filhos** retornando em formato de [[#Diferença Entre `HTMLCollection` e `NodeList`|NodeList]]
```js
const el = document.querySelector('body');
console.log(el.childNodes);
```
>[!attention] Atenção
>Ele é sensível a espaços, os trazendo na *NodeList*

### `children`
Através do `children` ([Doc](https://developer.mozilla.org/en-US/docs/Web/API/Element/children)) podemos **acessar todos os elementos filhos** retornando em formato de [[#Diferença Entre `HTMLCollection` e `NodeList`|HTMLCollection]], onde ao contrario do anterior ==já elimina os espaços==
```js
const el = document.querySelector('body');
console.log(el.children);
```

### `firstChild` e `firstElementChild`
Através de `firstChild` ([[#Diferença entre `Node` e `Element`|Node]]) ou `firstElementChild` ([[#Diferença entre `Node` e `Element`|Element]]) podemos acessar o primeiro filho do nosso elemento, porem utilizando `firstChild` ele é sensível a espaços como o [[#`childNodes`|childNodes]] por sé tratar de um [[#Diferença entre `Node` e `Element`|Node]].
```js
const el = document.querySelector('body');
console.log(el.firstChild);
console.log(el.fristElementChild);
```
Obviamente ==existe as mesma versões para o *last*, ou seja, ultimo==
```js
const el = document.querySelector('body');
console.log(el.lastChild);
console.log(el.lastElementChild);
```

## Elementos Irmãos
Através de `nextSibling` ([[#Diferença entre `Node` e `Element`|Node]]) ou `nextElementSibling` ([[#Diferença entre `Node` e `Element`|Element]]) podemos ==acessar o próximo irmão== do nosso elemento, porem utilizando `nextSibling` ele é sensível a espaços por sé tratar de um [[#Diferença entre `Node` e `Element`|Node]].
```js
const el = document.querySelector('body');
console.log(el.nextSibling);
console.log(el.nextElementSibling);
```
Obviamente podemos ==acessar o irmão anterior== do nosso elemento através de `previousSibling` ([[#Diferença entre `Node` e `Element`|Node]]) ou `previousElementSibling` ([[#Diferença entre `Node` e `Element`|Element]])
```js
const el = document.querySelector('body');
console.log(el.previousSibling);
console.log(el.previousElementSibling);
```