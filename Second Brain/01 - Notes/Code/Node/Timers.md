---
title: Timers no node
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript, node]
description: Como trabalhar com tempo no node.js
---
# Introdução
Maneiras de trabalhar com tempo dentro do NodeJS, utilizando de _Timers_, sendo eles:
- `setTimeout()` - Espera um tempo e depois roda a função
- `clearTimeout()` - Cancela _Timeout_
- `setInterval()` - De tempo em tempo executa uma função
- `clearInterval()` - Cancela _Interval_

# Timeout
Através da função `setTimeout` podemos atribuir um tempo em milissegundos, onde, **ao fim executara** uma função que será referenciada (atalho de função, função anônima).

>[!note] Atente-se ao retorno
>Função `setTimeout()` retorna um objeto `Timeout` com informações do mesmo, onde esse objeto pode ser passada como parâmetro para `clearTimeout()`

```js
const timeOut = 3000;
const fineshed = () => {
	console.log('Done!');
};

const timer = setTimeout(fineshed, timeOut);
console.log('Mostrar');
clearTimeout(timer);
```

Assíncrono, pois, é executado primeiro o `console.log` com o valor `mostrar`, enquanto `setTimeout()` esta na _Worker threads_, que chegando ao fim devolve a Função _callback_ para a _Event queue_ onde será executada.

# Interval
Através da função `setInterval` podemos atribuir um tempo em milissegundos, onde, entra em um _loop_ que a cada fim de contagem executa a função referenciada (atalho de função, função anônima).

>[!note] Atente-se ao retorno
>Função `setInterval()` retorna um objeto `Interval` com informações do mesmo, onde esse objeto pode ser passada como parâmetro para `clearInterval()`

```js
const interval = 3000;
const checking = () => {
	console.log('checking!');
};

const timer = setInterval(checking, timeOut);
console.log('Mostrar');
clearInterval(timer);
```

Assíncrono, pois, é executado primeiro o `console.log` com o valor `mostrar`, enquanto `setInterval()` esta na _Worker threads_, que chegando ao fim de cada contagem devolve a Função _callback_ para a _Event queue_ onde será executada.