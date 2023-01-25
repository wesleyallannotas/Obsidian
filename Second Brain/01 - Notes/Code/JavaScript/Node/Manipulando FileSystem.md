---
title: Manipulando Arquivos
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [note]
description: Manipulando arquivos nativamente 
---
# Introdução
Recorrentemente teremos que lidar com o _filesystem_ durante a execução da nossa aplicação, assim sendo de extrema importância saber manipula-lo, podemos atingir essa objetivo através de um modulo/biblioteca interna do Node, que possua a capacidade de lidar com o `fileSystem`, possuindo o mesmo nome, é sendo importada através da sigla `fs`.

# Importando
Basicamente importaremos o modelo interno `fs`, ou seja, por se tratar de um modulo interno não é necessário especificar caminho, basta adicionar o nome.

```js
const fs = require('fs');
```

# Possibilidades
Através do modulo `fs`, podemos realizar diversas manipulações no nosso `filesystem`, sendo algumas delas.

## Manipulando Arquivos
Podemos ler e manipular arquivos facilmente através dos métodos encontrados no modulo `fs`

```js
fs.readFile('./arq.txt' (err, resp) => {
	if (err) return console.log('Erro!', err.stack);
	console.log(resp.toString());
})
```

## Criando Diretório
Podemos diretórios facilmente através dos métodos encontrados no modulo `fs`.

```js
fs.mkdir('./teste', (err, resp) => {
	if (err) return console.log(err.stack);
	console.log(resp.message);
})
```

Através do método podemos criar um diretório facilmente, e em seguida passamos uma [[Funções#Arrow Function|Arrow Function]], [[Funções#Função Anônima|Função anônima]] ou até mesmo uma [[Funções#Referencia de Função|Referencia de função]].
