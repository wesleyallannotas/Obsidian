---
title: Modulos
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Trabalhando com modulos no JavaScirpt
---
# Importando Módulos
Podemos importar módulos externos através das seguintes expressões.

## Antiga
Através da função global `require()` podemos importar módulos nativos ou externos, seja criados por nós ou baixados via `npm` (*Node Package Manager*).
```js
const path = require('path');
console.log(path.basename(__filename));
```

### Importando item especifico
Podemos importar um item especifico de um modulo adicionando o nome entre chaves, basicamente estamos utilizando [[Expressões e Operadores#Operadores de Desestruturação|desestruturação]], assim possibilitando renomear.

```js
const { EventEmitter } = require('events');

const { EventEmitter: Renomeando } = require('events');
```

Neste caso estamos importando apenas a classe _EventEmitter_ que existe dentro do modulo `events`

## Moderna
Através dos operadores `import` e `from` podemos importar módulos nativos ou externos do Node, seja criados por nós ou baixados via `npm` (Node Package Manager)

>[!attention] Não suportada atualmente
>Apesar do operador `import` estar definido na sintaxe do JavaScript, o motor do NodeJS, o [[#Motor V8|V8]], ainda não o implementou atualmente (12/01/2023), ou seja, de forma nativa temos acesso somente a forma [[#Antiga]]. Caso deseje utilizar o `import` é necessário utilizar um compilador que converta da sintaxe moderna para antiga que é compatível com o NodeJS, o mais conhecido e usado para esse e diversos outros problemas de incompatibilidade é o _Babel_

```js
import path from 'path';
console.log(path.basename(__filename));
```

```js
import { Eventemitter } from 'events';
```

# Criando Módulo
Podemos exportar módulos da seguinte forma.

## Antiga
Através do objeto global  `module` podemos utilizar o método `exports` onde podemos atribuir o que desejarmos Array, Object, String, Number...

```js
// Arquivo que realizara a exportação
module.exports = "Testando exportação";
```

```js
const myModule = require('./path/arquivo.js');
const myModule = require('./path/arquivo'); // Pode omitir o ".js"
```

## Moderna
Através dos operadores `export` que podemos definir para diferentes itens assim os possibilitando de ser importando individualmente através da sintaxe entre chaves `{ }` e `export default` onde podemos definir uma exportação padrão que quando não especificado, será utilizada.

```js
function main() {}

export default main;
```

```js
export function main() {}
```