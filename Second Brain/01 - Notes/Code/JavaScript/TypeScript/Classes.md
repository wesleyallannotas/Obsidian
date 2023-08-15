---
title: Classes
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [typescript]
description: Criando e utilizando classes com typescript
---
# 🚀 Introdução
Basicamente criamos uma [[01 - Notes/Code/JavaScript/Classes|classes igual ao JavaScript]] porem adicionamos tipagem e podemos controlar seu nível de acesso.

# 🔐 Nível de Acesso
Possuímos nível de acesso para as nossas propriedades e métodos 
- `public` - Visível para fora.
- `privado` - Visível apenas dentro da classe.
- `protected` - Visível apenas dentro da classe e das que a estenderem.
- `readonly` - Funciona somente para propriedades apenas leitura (Pode ser usado em conjunto com os anteriores)

> [!attention] Atenção com `readonly` com _Arrays_
> Adicionando antes da propriedade a propriedade não podera ser altera, adicionando antes da tipagem da _array_, a _array_ não poderá ser alterada.
> ```ts
> class Person {
> 	private readonly colaboradores =  readonly Colaboradores[];
> }
>```

>[!fail] Propriedades privadas
>Mesmo criar propriedades privadas quando passa pelo _webpack_ normalmente deixa passar tal erro, para resolver basta instalar a seguinte biblioteca
>```bash
>npm install -D fork-ts-checker-webpack-plugin
>```
>Em seguida basta adicionar o arquivo de configuração do _webpack_
>```js
>const ForkTsCheckerWebpackPlugin = require('fork-ts-checker-webpack-plugin');
>{...}
>plugins: [new ForkTsCheckerWebpackPlugin()],
>{...}
>```
