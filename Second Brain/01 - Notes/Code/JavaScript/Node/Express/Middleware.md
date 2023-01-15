---
title: Middleware
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [express]
description: Entendo o funcionamento dos middlewares no Express.
---
# Middleware no Express
Express possui seu fluxo de _request_ e _reponse_ totalmente baseado em _Middlewares_, onde nada mais são que funções que tratam o ciclo de vida da informação, onde são passadas por elas e no fim ocorre o envia da response.

![[Desenho_Express_Exemplo_Middleware|600center]]

No exemplo a cima a _request_ chega e bata no `express`, que possui a responsabilidade de conter tudo relacionado ao serviços Web e seus protocolos e métodos, onde essa informação é passada por uma fila de _middlewares_ criadas por nós onde podemos tratar dados, testar permissões, entre outros.
O fluxo é encerrado quando ocorre um `res.render`, `res.send` ou  `res.end`, pois, esses métodos emitem o cabeçalho de resposta do protocolo [[HTTP]].

```js
const express = require('express'); 

const app = express(); 

// Middleware #1 
app.get('/', (req, res, next) => { 
	res.locals.hello = 'Hello World'; 
	next(); 
});

// Middleware #2
app.get('/', (req, res) => {
	return res.send(res.locals.hello);
});

// Middleware #3
app.get('/', (req, res) => {
	res.send('Eu nunca serei chamado! T.T');
});

app.listen(3000);
```

O primeiro _middleware_ grava uma informação e usa a função `next` recebida por meio de parâmetros, para passar para o próximo _middleware_, porem no segundo _middleware_, existem um `res.send()`, ou seja, ocorre a construção do cabeçalho HTTP e ele não pode ser reescrito, assim já ocorrendo a finalização de toda essa pilha de _middleware_ criada para o método `GET` na rota `"/"`, utilizamos `return` para finalizar a execução e retornar o cabeçalho para que ele possa ser enviado.

## Middleware Genéricos
`express` separa os _middlewares_ por métodos, rotas e sub-rotas, ou seja, um método `POST` não esta na mesma pilha do método `PUT` da mesma rota e o mesmo ocorre para as rotas com métodos diferentes, para que possamos definir um middleware para todas as rodas ou para todas sub-rotas ou utilizada por vários métodos diferentes, utilizamos _middlewares_ genéricas, no `express` sendo representada pelo `use`.

```js
app.use( (req, res, next) => {
	res.locals.hello = 'Hello World';
});

app.get('/', (req, res) => {
	return res.send(res.locals.hello);
});
```

Neste exemplo, todo e qualquer dado que entrar, passara pela _middleware_ genérica e depois seguira para sua rota e método especifico.
_Middlewares_ genéricas são muito utilizadas por exemplo para autenticação.

```js
app.use('/app', (req, res, next) => {
	if (!usuarioLogado) res.redirect();
	next();
})
```

Nesse caso ocorrera a verificação no _path_ `/app` e em todos _sub-path_ como por exemplo `/app/dashboard`.