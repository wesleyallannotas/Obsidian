---
title: Global
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [typescript]
description: Como adicionar tipagem ao global.
---
# 🚀 Introdução
É importante adicionar a tipagem ao global para que possarmos passar valor para o ambiente global e poder acessar em qualquer lugar da nossa aplicação e tipar evita a tipagem `any` e utilizar de todo poder do TypeScript.

# 🏗️ Tipando
Basicamente criamos um com o nome `global.d.ts` ou `index.d.ts` e declaramos o Global onde dentro do mesmo passamos a tipagem através do `var`, podemos utilizar um var antes de cada tipagem ou separar por virgula, no final basta realizar o `export`.
Para pegarmos a tipagem de uma biblioteca é necessário realizar a tipagem _inline_.

```ts
declare global {
  var connection: import('mysql2').PromisePool<
      import('mysql2').PromiseConnection
    >,
    numConnections: number,
    prefixes: string[];
}
export {};
```
