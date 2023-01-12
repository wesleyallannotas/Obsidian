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
Antes do amplo uso do `JSON` o formato principal de troca de dados era o `XML`, através dessa função `XMLHttpRequest()` nativa do JavaScript foi possível obter os dados das APIs que retornavam `XML`, assim possibilitando buscar dados do Back-End sem recarregar toda a página, hoje em dia da suporte a outros formatos como `JSON` e até mesmo texto simples.

>[!attention] Atenção
>`fetch()` e `XMLHttpRequest` possuem muitas diferenças, uma delas é no objeto de resposta, temos que atentar ao uso para não confundir

```js
function success() {
    console.log(this.responseText);
    let data = JSON.parse(this.responseText);
    console.log(data);
};
  
function fail(err) {
    console.log('Erro', err)
};
  
const req = new XMLHttpRequest();
req.onload = success;
req.onerror = fail;
req.open('GET', 'https://ap.github.com/users/wesleyallan');
req.send();
```

[06/10 Fetch - JavaScript Antes do Framework (React ou Vue.js) - YouTube](https://www.youtube.com/watch?v=fhIDgAfuJZ8)
[Introdução às Web APIs - Aprendendo desenvolvimento web | MDN (mozilla.org)](https://developer.mozilla.org/pt-BR/docs/Learn/JavaScript/Client-side_web_APIs/Introduction)

# Fetch
_Fetch_ em português seria buscar, pegar. Dentro das Web API temos acesso a função `fetch()` para realizar [[HTTP#Request|requests HTTP]], onde enviando apenas a [[HTTP#Locator (Localização)|URL]] realizamos o método [[HTTP#Methods|GET]], onde recebe como um primeiro argumento/parâmetro a URL para realizar a ação. Foi criado para consumir [[HTTP#Resource (Recurso)|recursos]] de modo [[Assíncronismo|assíncrona]]. Será retornado uma [[Assíncronismo#Promise|promise]], onde podemos utilizar os métodos comuns de um objeto do tipo _Promise_ para executar [[Funções#*Callback Function*|callback functions]] que possuíram como parâmetro um `JSON` que precisa ser convertido através do método `.json()`, assim gerando outra _Promise_, criando essa sequencia de `fetch()`.
`fetch()` não lança um erro quando recebe o [[HTTP#Status Code|status code]] 400 ou 500, ou seja, passara para a função `.then()`, só lança erro se a própria solicitação for interrompida por problemas de conexão, será necessário criar um lógica para tratar os _status code_, que pode ser obtido através de `reponse.status`

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

## Manipulando Request
Utilizando `fetch()` podemos enviar um objeto como parâmetro contendo dados da nossa requisição.

```js
fetch('https://api.github.com/users/wesleyallan', {
	method: 'GET',
	headers: '{"content-type": "application/json;charset=UTF-8"}'
})
.then( res => res.json())
.then( json => console.log(json))
.catch(err => console.log(err));
```

### Enviando Body
Para uma solicitação POST, é possível usar a propriedade _body_ para passar uma _string_ de JSON como entrada. Observe, no entanto, que o corpo da solicitação deve ser uma _string_ de JSON, enquanto os cabeçalhos devem ser um objeto JSON.

```js
let _data = {
  title: "foo",
  body: "bar", 
  userId:1
}

fetch('https://jsonplaceholder.typicode.com/posts', {
  method: "POST",
  body: JSON.stringify(_data),
  headers: {"Content-type": "application/json; charset=UTF-8"}
})
.then(response => response.json()) 
.then(json => console.log(json))
.catch(err => console.log(err));
```