---
title: Funcionamento do Falsy e Truthy
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Funcionando do Falsy e Truthy na necessidade de booleano
---
# Introdução
Tem-se a mesma ideia do [[Manipulando Dados#Type Conversion Coersion|type coersion]] realizado implicitamente pelo JavaScript, onde ==através de um interpretação do dado e a necessidade de um booleano== ele pode assumir verdadeiro (*true*) ou falso (*false*), normalmente acontece em condicionais e repetições (*loops*), podemos forçar essa necessidade de um booleado e a aplicação do _falsy_ e _truthy_ utilizando o operador de negação duas vezes `!!`.

```js
let value = -1;
console.log(!!value);  // True

// Negação + Falsy-Truthy
console.log(!(!!value));
```

## Falsy
Considerando o valor como falso (*false*) através do contexto onde um booleano é obrigatório e se encontra um dos seguintes valores
- `false`
- `0`
- `-0`
- `""`
- `null`
- `undefined`
- `Nan`

## Truthy
Considerando o valor como verdadeiro (*true*) através do contexto onde um booleano é obrigatório e se encontra um dos seguintes valores
- `true`
- `{}`
- `[]`
- `1`
- `3.23`
- `"0"`
- `"false"`
- `-1`
- `Infinity`
- `-Infinity`