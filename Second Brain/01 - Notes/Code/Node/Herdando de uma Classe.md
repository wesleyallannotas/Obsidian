---
title: Herdando propriedades e métodos de uma classee
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [node]
description: Utilizando função do modulo utils para herdar de uma classe para outra
---
# Introdução
O modulo `util` é interno ao Node, e traz consigo diversas funcionalidades interessantes, uma delas é a função onde conseguimos passar objetos onde um herda as propriedades de métodos do outro, por exemplo.

```js
const { inherits } = require('util');
const { EventEmitter } = require('events');

function Character(name) {
	this.name = name;
}

inherits(Character, EventEmitter);

const chapolin = new Character('Chapolin');
chapolin.on('help', () => console.log(`Eu! o ${chapolin.name} colorado!`));

console.log('Oh! E agora, quem poderá me defender?');
chapolin.emit('help');
```
