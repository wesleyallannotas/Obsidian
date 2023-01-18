---
title: Note
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags:
description: 
---
# Criando Tipo
Podemos criar tipos através do operador `type`, podemos criar tipos primitivos flexíveis utilizando o [[Tipagem#Operador Union|Operador Union]] 
```typescript
type IdType = string | number | undefined;

let userId: IdType;
let adminId: IdType;
```

Assim economizando na escrita, e facilitando a manutenção, pois, todos compartilham o mesmo tipo, com uma alteração impactando em todos.

## Criando Tipo para Objetos
Também podemos utilizar o operador `type` para criar tipos para objetos.

```typescript
type Point = {  // Criando tipo
  x: number;
  y: number;
};
  
let points2: Point = {  // Utilizando tipo 
  x: 105,
  y: 106,
};
  
function printCoord(points: Point) {  // Utilizando tipo como parâmetro
  console.log(`O eixo x é: ${points.x}`);
  console.log(`O eixo y é: ${points.y}`);
}
  
printCoord({ x: 105, y: 107 });
printCoord(points2);
```

### Propriedades opcionais
Durante o nosso desenvolvimento iremos nos deparar com objetos que possuem propriedades que não são obrigatórias, assim podemos definir uma propriedade como opcional através do operador `?`, basta adicionar ao final do nome da propriedade.

```typescript
type User = {
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

# Type Assertions
Através do uso do operador `as` realizamos o _Type Assetions_ ou em português asserção de tipo. Que é Utilizamos quando o TypeScript não sabe a tipagem de determinado objeto, porem forçamos que ele aceite e confie, é muito utilizado para consumir [[Dicionario do Programador#API|APIs]], assim utilizamos a _Assestions_ para dizer qual é o tipo.

```typescript
type userResponse = {
	id: number;
	name: string;
	avatar;
}

let userResponse = {} as UserResponse;
```

O objeto `userResponse`, o TypeScript não sabe o que tem dentro, por exemplo em uma API, não sabe o que viria, assim utilizamos o operador `as` para informar que ==ele é conforme== o [[#Criando Tipo|tipo que criamos]], assim forçando a interpretar a nosso objeto como contendo aqueles dados.

# Intersecção de Tipos
Podemos realizar a intersecção e dois tipos diferentes através do operador `&`

```typescript
type User = {
	id: number;
	name: string;
}

type Char = {
	nickname: string;
	level: number;
}

type PlayerInfo = User & Char;

let user1: User;
let char1: Char;
let player1: PlayerInfo;
```

Criamos o _type_ `PlayerInfo` que realiza a intersecção dos tipos `User` e `Char`, assim somando as propriedades de ambos, finalizando com três tipos criados e disponíveis.

>[!tip] Também pode
>Podemos também invés de criar um tipo para realizar a intersecção, informa-lo diretamente.
>```typescript
>type PlayerInfo = User & {
>	nickname: string;
>	level: number;
>}
>
>let player1: PlayerInfo;
>```

