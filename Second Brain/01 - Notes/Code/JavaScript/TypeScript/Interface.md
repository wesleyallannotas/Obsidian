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
Assim como a [[Tipagem#Criando Tipo|criação de tipos]] com ambos podemos utilizar para desenvolver tipagens para objetos, normalmente o `interface` e mais utilizado no contexto de orientação a objeto, além de outras peculiaridades e diferenças na sintaxe.

```typescript
interface User {
	id: number;
	name: string;
	isAdmin?: boolean;
	sleep(): void;
	sleep: () => void; // Não recomendado
}
```

>[!tip] Dizem
>Dizem que Type é mais recomendado por ser mais simples e mais fácil de lidar com tipos primitivos e também por ser mais flexível.

# Propriedades opcionais
Durante o nosso desenvolvimento iremos nos deparar com objetos que possuem propriedades que não são obrigatórias, assim podemos definir uma propriedade como opcional através do operador `?`, basta adicionar ao final do nome da propriedade.

```typescript
interface User = {
	name: string;
	email: string;
	age: number;
	isAdmin?: boolean;
}

let darkness: User = {
	name: 'Wesley',
	email: 'wesley.allansilva@gmail.com',
	age: 24
}
```

# Declaration Merging
Ao contrario de [[Type]] que não aceita "redeclarar", ou seja, não são **abertas**, Utilizando `interface` podemos, e quando é feito na realidade é realidade uma mescla das interfaces com mesmo nome.

```typescript
interface Car {
	ano: number;
}

interface Car {
	model: string;
}

let saveiro: car {
	ano: 2007,
	model: 'G4'
}
```

# Extensão de Interfaces
Assim como existe a [[Type#Intersecção de Tipos|intersecçâo de tipos]] para [[Type]] existem a extensão de `interface` porem sua sintaxe e diferente e sua ideia se baseia em passar o nome da outro interface, utilizar o operador `extends` e listar uma ou mais interfaces que ira estender, ou seja, receber sua estrutura.

```typescript
interface User {
	id: number;
	name: string;
}

interface Char {
	nickname: string;
	level: number;
}

interface PlayerInfo extends User, Char {
	playTime: Date;
};
```

Ao contrario da intersecção de tipos que utilizamos o operador `&` e o sinal de igual antes de realizar a intersecção, com interface utilizamos o operador `extends` e listamos as interfaces que ele estende e terminados com chaves `{}`, ou seja, que trará as propriedades.

# Implementada por Classes
Interfaces estão mais ligados com a orientação a objeto, assim podemos utilizar uma interface para implementar um classe, basicamente utilizando a ideia de [[Abstração]].

```typescript
interface Car {
	ano: number;
	model: string;
}

class Sedan implements Car {
	// Código da Classe
}
```