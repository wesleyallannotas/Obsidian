---
title: Requisições com JavaScript
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Diferentes forma de trabalhar com requisições com Javascript
---
# XMLHttpRequest
[Tutorial de Fetch API em JavaScript – exemplos de Post e cabeçalho (freecodecamp.org)](https://www.freecodecamp.org/portuguese/news/tutorial-de-fetch-api-em-javascript-exemplos-de-post-e-cabecalho/)
[06/10 Fetch - JavaScript Antes do Framework (React ou Vue.js) - YouTube](https://www.youtube.com/watch?v=fhIDgAfuJZ8)
[Introdução às Web APIs - Aprendendo desenvolvimento web | MDN (mozilla.org)](https://developer.mozilla.org/pt-BR/docs/Learn/JavaScript/Client-side_web_APIs/Introduction)
[APRENDA FETCH API DE JAVASCRIPT COM PROJETO - YouTube](https://www.youtube.com/watch?v=qIGYM4S8x50)

# Fetch
_Fetch_ em português seria buscar, pegar. Dentro das Web API temos acesso a função `fetch()` para realizar [[HTTP#Request|requests HTTP]], onde enviando apenas a [[HTTP#Locator (Localização)|URL]] realizamos o método [[HTTP#Methods|GET]], onde recebe como um primeiro argumento/parâmetro a URL para realizar a ação. Será retornado uma [[Assíncronismo#Promise|promise]], onde podemos utilizar os métodos comuns de um objeto do tipo _Promise_ para executar [[Funções#*Callback Function*|callback functions]] que possuíram como parâmetro um `JSON` que precisa ser convertido através do método `.json()`, assim gerando outra _Promise_, criando essa sequencia de `fetch()`

>[!tip] Formas de Utilizar
>Podemos utilizar o `fetch()` através de  [[Assíncronismo#Promise|Promise]] ou Async/Await

```js
fetch('https://api.github.com/users/wesleyallan')
  .then( response => {
    response.json()
      .then( data => {
        fetch(data.repos_url)
          .then( res => res.json().then( d => console.log(d)))
      })
  } )
```

Para melhorar nosso código podemos utilizar das varias omissões possíveis de um [[Funções#*Arrow Function*|Arrow Function]] como a de manter o código todo em uma linha, onde conseguimos definir o retorno mesmo omitindo o `return`, conseguimos navegar pela API, ficando da seguinte forma.

```js
fetch('https://api.github.com/users/wesleyallan')
  .then( response => response.json())
  .then( data => fetch(data.repos_url))
  .then( res => res.json())
  .then( d => console.log(d))
  .catch( err => console.log(err))
  .finally( () => console.log('Chegou ao fim'));
```

Utilizamos o encadeamento de promessas criando um código mais limpo, vale ressaltar que o método `catch()` é  executado ==independe de onde for o erro.==
