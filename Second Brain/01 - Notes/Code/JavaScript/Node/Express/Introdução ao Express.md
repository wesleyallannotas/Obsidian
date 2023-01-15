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

# Transformando em JSON
Será necessário utilizar o modulo não instanciado do `express` e utilizar seu método `json()`, ficando da seguinte forma.

```js
const express = require('express');

const app = express();

app.use(express.json());
```

