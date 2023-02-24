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
Conhecido como _route params_, Podemos enviar parâmetros para o nosso `express` ou para qualquer outro solução que use os padrões do [[HTTP]], através da [[HTTP#Locator (Localização)|URL]], utilizando os dois pontos (`:`), onde podemos receber o valor da seguinte forma.

> [!info] Como usar
>Comumente utilizado para passar um dado que é requisitado, por exemplo, uma rota de `post` ter a possibilidade de passar o _id_ de um _post_ via URL e a página já ser carregada em determinado _post_, ou a [[Dicionario do Programador#API|API Rest]] devolver determinado _post_ através de um [[HTTP#Methods	|Método]] _get_.
>```bash
>https://localhost:3001/post/1
>``` 

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

>[!info] Como usar
>Comummente utilizado em pesquisas e ou parametrização do conteúdo, por exemplo se deve ser visível ou não tal dados.
>```bash
>https://localhost://3000/?showStock=true
>https://localhost://3000/?name=wesley+silva&state=SP
>```

```js
app.route('/').get( (req, res) => res.send(req.query.name))
```

Nesse caso coletamos o valor que o usuário pesquisou para `name`, ou seja, na URL, deve estar da seguinte forma.

```
http://localhost:3000/?name=wesley
http://localhost:3000/?name=wesley&age=28
```
