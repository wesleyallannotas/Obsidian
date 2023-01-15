---
title: Enviando Dados pela URL
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [express]
description: Capturando dados via URL com express.
---
# Parâmetro
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

# Query
Conhecido como _query params_, Podemos criar uma busca pela [[HTTP#Locator (Localização)|URL]] utilizando a interrogação, e para implementar devemos acessar o que o usuário esta buscando pela requisição, por exemplo

```js
app.route('/').get( (req, res) => res.send(req.query.name))
```

Nesse caso coletamos o valor que o usuário pesquisou para `name`, ou seja, na URL, deve estar da seguinte forma.

```
http://localhost:3000/?name=wesley
http://localhost:3000/?name=wesley&age=28
```
