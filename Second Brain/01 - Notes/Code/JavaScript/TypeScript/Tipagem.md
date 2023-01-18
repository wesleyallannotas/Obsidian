---
title: Tipagem
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [typescript]
description: Adicionando tipos ao nosso javascript
---
# Tipagem Explicita
Quando informamos o tipo da variável, possui os mesmo tipos dos JavaScript.

```typescript
let info: string = 'Vire a esquerda'
let info: string;
function sum(a: number, b:number) {}
```

De forma explicita informamos que `info` é do tipo [[Introdução ao JavaScript#String|String]], assim não aceitando valores diferentes e trazendo a informação para os desenvolvedores quando bate o olho e para a "IDE" informar o erro caso especificado outro tipo de valor.

# Tipos Primitivos
São os tipos de dados mais simples e sem uma estrutura, os mesmo do [[Introdução ao JavaScript#Primitivos (*Primitive*)|JavaScript]]

```typescript
let text: string;
let num: number;
let loading: boolean;
```

# Tipos Estruturais
São estrutura de dados que buscam armazenar mais que um dado apenas, os mesmo do [[Introdução ao JavaScript#Estuturais (*Structural*)|JavaScript]]

```typescript
let numeros: number[];       // Array/Vetor de Numbers
let numeros: Array<number>;  // Array/Vetor de Number
```

# Tipagem em Funções
Adicionamos tipagem em uma função, informando os tipos dos parâmetros/argumentos e o tipo de seu retorno, ficando da seguinte forma.

```typescript
function showMessaages(message: string): void{
	console.log(message);
}


function sum(x: number, y:number): number {
  return x + y;
}

function sum(x: number, y:number) { // Inferi como retorno do tipo number.
	return x + y;
}
```

O valor `void` é vazio, ou seja, informamos que essa função não tem retorno, assim a "IDE" já consegui nos informar erro caso utilizarmos o `return` dentro da função.

>[!attention] Caso omitido
>Caso não informarmos o tipo de retorno, [[Introdução ao TypeSript#Inferência de Tipo|TypeScript o inferi]] baseado no retorno.

# Tipo `any`
Quando declaramos uma variável sem informar seu tipo, ela recebe a tipagem com `any`, nada mais é do que uma variável sem tipo especifico, assim aceitando qualquer tipo de valor, ou seja, possuindo o funcionamento normal do JavaScript de tipagem dinâmica.

```typescript
let info;    // Tipo any
let age any; // Tipo any
```

# Operador Union
O operador _union_ nada mais é do que `|` na declaração do tipo, o utilizamos quando queremos informar que um variável aceita mais do que um tipo de dado.

```typescript
function printUserId(id: number | string): void {
	console.log(`O ID do usuário é: ${id}`);
}
```

Assim informamos que nosso parâmetro/argumento `id` aceita um valor do tipo `number` ou `string`, podemos encadear quantos operadores _union_ for necessário, por exemplo.

```typescript
function printUserId(id: number | string | boolean): void {
	console.log(`O ID do usuário é: ${id}`);
}
```

# Criando Tipo
Podemos criar tipos através do operador `type`,  por exemplo

```typescript
type IdType = string | number | undefined;

let userId: IdType;
let adminId: IdType;
```

Assim economizando na escrita, e facilitando a manutenção, pois, todos compartilham o mesmo tipo, com uma alteração impactando em todos.

## Criando Tipo para Objetos
Também podemos utilizar o operador `type` para criar tipos para objetos.

```typescript
type Point = {
  x: number;
  y: number;
};
  
let points2: Point = {
  x: 105,
  y: 106,
};
  
function printCoord(points: Point) {
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

