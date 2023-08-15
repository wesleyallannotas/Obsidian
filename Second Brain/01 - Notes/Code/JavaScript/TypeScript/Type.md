---
title: Note
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [typescript]
description: 
---
# Criando Tipo
Podemos criar tipos através do operador `type`, desde tipos primitivos, tipos de [[Introdução ao JavaScript#Array|Arrays]] e tipos de objetos, podemos criar tipos primitivos flexíveis utilizando o [[Tipagem#Operador Union|Operador Union]] 
```typescript
// Alias com operador union
type IdType = string | number | undefined;
type Nullish = null | undefined;
type Fruit = 'apple' | 'pear' | 'orange';

let userId: IdType;
let adminId: IdType;
```

Assim economizando na escrita, e facilitando a manutenção, pois, todos compartilham o mesmo tipo, com uma alteração impactando em todos.

## Criando Tuplas
Através do operador `type` podemos criar tuplas, que são [[Introdução ao JavaScript#Array|Arrays]] com tamanho especifico e tipos de dados específicos, podemos nomear os dados, porem resultara em uma _array_ da mesma forma.

```ts
type Tupla = [col: number, row: number];
const tabela: Tupla = [20, 20];
```

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

# Criando Tipo para Referencia Função
Também podemos criar tipos para referencias de função.

```typescript
// Tipando função
type setValue = (newValue: IdType) => void;

// Tipando com referencia de função criada
function returnSet(fn: setValue): string { /* Corpo Função */ }

// Criando com Arrow Function
const setId: setValue = (newValue) => userId = newValue;
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

// Exemplo no React
type User = {
  name: string;
  avatar: string;
}

const [user, setUser] = useState<User>({} as User);
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

Caso utilizamos o operador de `|` teremos a possibilidade de satisfazer ==um dos tipos especificados ou todos.==

```typescript
type User = {
	id: number;
	name: string;
}

type Char = {
	nickname: string;
	level: number;
}

type PlayerInfo = User | Char;

let user1: User;
let char1: Char;
let player1: PlayerInfo;

const player1: PlayerInfo = {
	id: 2,
	name: 'Wesley'
}
```

# Implementada por Classes
Types também podem implementar um classe, basicamente utilizando a ideia de [[Abstração]].

>[!attention] Atenção
>Não é a melhor opção, é mais recomendado o uso de interface. E por `class` e `interface` serem _static blueprints_ não aceita o uso de [[Tipagem#Operador Union|operador union.]]

```typescript
type Car = {
	ano: number;
	model: string;
}

class PartialPoint = { x: number; } | { y: number; }

class Sedan implements Car {
	// Código da Classe
}

// Erro!
class SomePartialPoint implements ParialPoint {
	x = 1;
	y = 2;
}
```

# Mapped Types
Um uso muito comum é quando uma ou mais propriedades pudessem ser opcionais, temos como criar [[#Propriedades opcionais]] através do operador `?`, porem o mesmo cria uma espécie de furo na nossa tipagem, a deixando de ser _Type safety_, assim sendo recomendado o uso de `Mapped Types`, TypeScript já trans alguns _Mapped Types_ por padrão
- `Partial<Generics>` -  O tipo informado pelo [[Generics]], pode ter suas propriedades informadas parcialmente.
- `Readonly<Generics>` -  O tipo informado [[Generics]], após ter seus valores atribuídos não poderá ser alterado.
- `Pick<tipo, propriedade>` - Através do tipo informando podemos selecionar uma propriedade dela, gerando um tipo com apenas as propriedades informadas.
- `Omit<tipo, propriedade>` - Através do tipo informado podemos selecionar uma propriedade que será omitida, assim gerando um tipo sem determinada propriedade.
- `Record<propriedades, tipo>` - Através das propriedades informadas podemos definir um tipo a todas elas de uma vez.

```typescript
interface Person {
	id: number;
	name: string;
	age: number;
	isAdmin: boolean;
}

const personPartial: Partial<Person> = {
	id: 15,
	name: 'Wesley',
	age: 24,
}

const personReadonly: Readonly<Person> = {
	id: 15,
	name: 'Wesley',
	age: 24,
	isAdmin: false
}

personReadonly.name = ''  // Erro!

const PersonId: Pick<Person, 'id'> = {
	id: 225
}

type PersonIdAndCpf = {
	cpf: number
} & Pick<Person, 'id'>

const PersonCommon: Omit<Person, 'isAdmin'> = {
    id: 23,
    name: 'Wesley',
    age: 24
}

const ButtonProps: Record<'name' | 'color', string> = {
    name: 'Clique',
    color: ' red'
}
```

Tipos mapeados são uma maneira de criar tipos baseados em outros tipos. É praticamente um tipo transformacional.

## Criando Mapped Types
Além de usar os já disponibilizados pela linguagem também podemos criar os nosso tipos mapeados.

```typescript
// Simples Mapped Types
type Fruit = 'melao' | 'abacaxi' | 'uva';

type FruitCount = {
  [key in Fruit]: number;
};

const fruits: FruitCount = {
  melao: 2,
  abacaxi: 3,
  uva: 4,
};
```

### Com Generics
Tipo mapeado com utilização de [[Generics]] que muda a funcionalidade do tipo informado a através da mesma.
```typescript
interface Person {
	id: number;
	name: string;
	age: number;
	isAdmin: boolean;
}

// Mapped Types com Generics
type Stringify<T> = {
	[P in keyof T]: string;	
}

type Stringify<T> = {
	readonly [P in keyof T]: string | number;	
}
```

Nessa expressão `[P in keyof T]: string;` informamos que para cada propriedade desse meu tipo `<T>`(_Generics_), eu quero que ela se torne _String_.

```typescript
interface Person {
	id: number;
	name: string;
	age: number;
	isAdmin: boolean;
}

type PersonPartial<Tipo> = {
	[Propriedade in keyof Tipo]?: Tipo[Propriedade] 
} & { id: number }  // Forço o ID ser preenchido.

const wesley: PersonPartial<Person> = {
	id: 25;
}
```

Criamos um _mapped type_ que transforma todas propriedades opcionais através do operador `?` mantendo os tipos originais através de `Tipo[Propriedade]`, porem realizamos uma [[#Intersecção de Tipos]] com um tipo que tem `id` como obrigatório, assim trazendo essa única propriedade como obrigatória.