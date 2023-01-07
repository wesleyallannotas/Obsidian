---
title: Eventos no NodeJS
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [node]
description: Disprando eventos com node, base apra muitos modulos importantes
---
# Introdução
Mecanismo para disparar eventos, onde podemos "Ouvi-los" e executando algo como resposta.

# Importando
O modulo de eventos já faz parte do _core_ do node, ou seja, já vem junto quando instalamos, só temos o trabalho de importa.

```js
const events = requise('events');
```

Dessa forma importamos toda o modulo, porem é muito comum importamos uma [[Introdução ao Node#Importando item especifico|item especifico do modulo]], que no caso é `EventEmitter`, então importaremos da seguintes forma.

```js
cosnt EventEmitter = require('events');
```

# Instanciando Classe
Após realizar a importação da classe `EventEmitter` que faz parte do modulo interno `events`, [[Expressões e Operadores#Operador *new*|realizamos a instanciação da classe]], para então podermos utilizar o que disponibiliza

```js
const ev = new EventEmitter();
```


# Emitindo Evento
Através do método `emit` podemos emitir um evento atribuindo um nome a ele, e caso desejado pode ser passado algo para ir como parâmetro para a função que será executada do "[[#Ouvindo Eventos|ouvinte de eventos]]"

```js
ev.emit('saySomething', 'Parâmetro para ouvinte');
```

# Ouvindo Eventos
Não adiantes [[#Emitindo Evento|emitir um evento]] sem que no nosso código "Esteja ligado o ouvidor de eventos para o mesmo" 

## Executa sempre
Através do método `on`, podemos criar um escutador de evento que será disparado **sempre** que o evento for emitido.

```js
ev.on('saySomething', (name) => {
	console.log(`Evento ouvido! ${name}`)
})

en.emit('saySomething', 'Wesley');
en.emit('saySomething', 'Andressa');
```

## Execução única
Através do método `once`, podemos criar um escutador de evento que será disparado **apenas uma vez** quando o evento for emitido.

```js
ev.once('saySomething', (name) => {
	console.log(`Evento ouvido! ${name}`)
})

en.emit('saySomething', 'Wesley');
en.emit('saySomething', 'Andressa');
```

Segunda emissão de evento não disparara nenhuma execução, pois, `once` só executara uma vez.