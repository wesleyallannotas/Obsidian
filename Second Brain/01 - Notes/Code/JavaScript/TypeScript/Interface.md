---
title: Interaces
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [typescript]
description: Criando itnerfaces com TypeScript
---
# Introdução
Assim como a [[Tipagem#Criando Tipo|criação de tipos]] com ambos podemos utilizar para desenvolver tipagens para objetos, normalmente o `interface` e mais utilizado no contexto de orientação a objeto.

```typescript
interface User {
	id: number;
	name: string;
	isAdmin?: boolean;
}
```

>[!tip] Dizem
>Dizem que Type é mais recomendado por ser mais simples e mais fácil de lidar com tipos primitivos e também por ser mais flexível.

# Intersecção de Interfaces
Assim como existe a [[Tipagem#Intersecção de Tipos|intersecçào de tipos]] também existem a interseção de `interface` porem sua sintaxe e diferente.

```typescript
interface User {
	id: number;
	name: string;
}

interface Char {
	nickname: string;
	level: number;
}

interface PlayerInfo extends User, Char {};
```

Ao contrario da intersecção de tipos que utilizamos o operador `&` e o sinal de igual antes de realizar a intersecção, com interface utilizamos o operador `extends` e listamos as interfaces que ele estende e terminados com chaves `{}`, ou seja, que trará as propriedades.