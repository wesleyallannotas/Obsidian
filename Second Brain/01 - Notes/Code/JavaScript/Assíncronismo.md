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
Quando estamos aprender a programar criamos códigos simples e que normalmente são **síncronos (_Synchronous_)**, ou seja, com uma tarefa sendo executada após a conclusão da outra, porem terá aplicações que se faz necessário continuar o fluxo do código, enquanto espera o termino da execução de uma tarefa, neste caso usaremos do **assincronismo (_asynchronous_)**.

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

