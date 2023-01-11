---
title: Assíncronismo no JavaScript
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Como escrever códigos assincronos.
---
# Introdução
Códigos simples e que normalmente criamos quando estramos aprendendo a programar são **síncronos (_Synchronous_)**, ou seja, com uma tarefa sendo executada após a conclusão da outra, porem terá aplicações que se faz necessário continuar o fluxo do código, enquanto espera o termino da execução de uma tarefa, neste caso usaremos do **assincronismo (_asynchronous_)**.

```js
const https = requite('https');
const API = 'https://jsonplacehold.typicode.com/users?_limit=2';
https.get(API, res -> {
	console.log(res.statusCode);
});
console.log('Conectando API')
```

Por se tratar de uma [[Funções#*Callback Function*|Callback Function]] que será executado após um determinado tempo dentro do método `get()`, o `console.log` de fora será impresso primeiro no console.

# Promise
Basicamente é uma promessa de que algo irá acontecer no futuro, é um objeto JavaScript usado para operações assíncronas, por exemplo, Carregar um arquivo, leitura de dados de uma API.

```js
let aceitar = true;

console.log('Pedir UBER');

const promessa = new Promise((resolve, reject) => {
  if (aceitar) {
    return resolve('Carro chegou!');
  } 
  return reject('Pedido Negado!');
});

promessa
  .then(result => console.log(result))
  .catch(erro => console.log(erro))
  .finally(() => console.log('Finalizada'));

console.log('Aguardando');
```

Instanciamos um objeto _promise_ passando como parâmetro um [[Funções#*Callback Function*|callback function]], onde passamos como parâmetro o _resolve_ caso de certo, e o _reject_ caso de errado, onde essa função deve retornar através de um destes métodos o resultado, onde criamos a partir do método ==`then()` uma resposta para caso de certo==, ou seja atinja o estagio _fulfilled_, a partir do método ==`catch()` uma resposta para caso de errado==, ou seja atinja o estagio _Reject_, e o método ==`finally()` executara quando atingir o estagio _settled_== que é quando chega ao fim do ciclo de vida da _promise_. 
Utilizamos `console.log` para exemplificar, porem podemos executar o que desejarmos.

## Estagios
Uma _promise_ possui estágios durante seu ciclo de vida sendo eles.
- _Pending_ - Estado inicial, assim que o Objeto da promessa é iniciado
- _Fulfilled_ - A promessa foi concluída com sucesso
- _Rejected_ - A promessa foi rejeitada, houve um erro
- _Settled_ - Seja com sucesso ou com erro, ela foi finalmente concluída

# Fetch
_Fetch_ em português seria buscar, pegar. Dentro das Web API temos acesso a função `fetch()`, onde recebe como um primeiro argumento/parâmetro a URL para realizar a ação. Será retornado uma [[#Promise]], onde podemos utilizar os métodos comuns de um objeto do tipo _Promise_ para executar [[Funções#*Callback Function*|callback functions]] que possuíram como parâmetro um `JSON` que precisa ser convertido através do método `.json()`, assim gerando outra _Promise_, criando essa sequencia de `fetch()`

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