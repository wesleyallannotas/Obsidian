---
title: Introdução ao Express
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [express]
description: Entendo o que é e o que faz a biblioteca Express.
---
_Express_ é uma biblioteca muito famosa e utilizada para construção de [[Dicionario do Programador#API|APIs REST]].

# Iniciando
Para que possamos iniciar a contrução da nossa API é necessário instalar o modulo `express` no nosso projeto a partir do NPM.

```bash
npm install express
```

Em seguida dentro do arquivo que conterá o código da nossa API, importamos o modulo.

```js
// Moderno (não suportado atualmente, precisa de babbel)
import express from 'express';

// Antigo (Suportado)
const express = require('express');
```

Criamos uma inicialização do nosso modulo `express`.

```js
const app = express();
```

# Definindo Porta
É necessário que definimos a porta que será utilizada para a conexão com a nossa API, isso é feito através do método `listen()` que recebe como valor uma [[Introdução ao JavaScript#String|String]] contendo o número da porta.

```js
app.listen('3000');
```

# Criando Rotas e Definindo Métodos
Criamos a rodas definindo o `path` na [[HTTP#Locator (Localização)|URL]] e o [[HTTP#Methods|Método]] utilizado, a rota base da página inicial é `/`, para criarmos uma rota utilizando `express`, utilizamos o método `route()`, e o encadeamos com o método por exemplo `get()` esse método recebe uma referencia ou uma função anônima, possuindo os parâmetros para o _request_ e o _response_, ficando de seguinte forma.

```js
app.route('/').get( (req, res) => res.send('Hello!'));
```

Omitimos o `return` através das possibilidades da [[Funções#*Arrow Function*|Arrow Function]] de que quando possui apenas uma [[Expressões e Operadores#Expressão|Expressão]], o valor será retornado sem a necessidade do operador, e utilizamos um método do objeto que receberemos contendo a resposta, enviando uma mensagem.

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

# Transformando em JSON
Será necessário utilizar o modulo não instanciado do `express` e utilizar seu método `json()`, ficando da seguinte forma.

```js
const express = require('express');

const app = express();

app.use(express.json());
```

# Parâmetro Pela URL
Conhecido como _route params_, Podemos enviar parâmetros para o nosso `express` através da [[HTTP#Locator (Localização)|URL]], utilizando os dois pontos (`:`), onde podemos receber o valor da seguinte forma.

```js
let data = {
	nome: "Wesley",
	sobrenome: "Silva",
	idade: 24
}

app.route('/:identificador').delete( (req, res) => {
	data[identificador] = ""
	res.send(req.params.identificador)
})
```

# Configurando Busca
Conhecido como _query params_, Podemos criar uma busca pela [[HTTP#Locator (Localização)|URL]] utilizando a interrogação, e para implementar devemos acessar o que o usuário esta buscando pela requisição, por exemplo

```js
app.route('/').get( (req, res) => res.send(req.query.name))
```

Nesse caso coletamos o valor que o usuário pesquisou para `name`, ou seja, na URL, deve estar da seguinte forma.

```
http://localhost:3000/?name=wesley
http://localhost:3000/?name=wesley&age=28
```