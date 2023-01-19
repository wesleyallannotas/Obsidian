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
Quando informamos o tipo da variável, possui disponível os mesmo tipos dos [[Introdução ao JavaScript#Primitivos (*Primitive*)|JavaScript]].

```typescript
let info: string = 'Vire a esquerda'
let info: string;
function sum(a: number, b:number) {}
```

De forma explicita informamos que `info` é do tipo [[Introdução ao JavaScript#String|String]], assim não aceitando valores diferentes e trazendo a informação para os desenvolvedores quando bate o olho e para a "IDE" informar o erro caso especificado outro tipo de valor.

# Tipos Primitivos
São os tipos de dados mais simples e sem uma estrutura.

```typescript
let text: string;
let num: number;
let loading: boolean;
```

# Tipos Estruturais
São estrutura de dados que buscam armazenar mais que um dado apenas.

```typescript
let numeros: number[];       // Array/Vetor de Number
let numeros: Array<number>;  // Array/Vetor de Number
const [students, setStudents] = useState<CardProps[]>([]) // Misturando
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

# Inferência de Tipo
Nada mais é do que o TypeScritp **inferir** o tipo da variável em relação ao seu valor atribuído na declaração, ocorre o mesmo com funções onde a inferência ocorre baseado no retorno.

```typescript
let info = 'Ola mundo!';
info = 10; // Informa Erro

function sum(n1: number, n2: number) {  // Infere o tipo baseado no retorno, neses caso number
  return n1 + n2;
}

// Exemplo no React
const [user, setUser] = useState({name: '', avatar_url: ''}); 
// Inferi user com esssas propriedades do tipo String
```

Será informado erro, pois, na declaração da variável atribuímos um valor do tipo _[[Introdução ao JavaScript#String|String]]_, assim o TypeScript **inferiu** que nossa variável `info` é do tipo _string_, sendo o mesmo que `let info: string = 'Ola mundo!'`

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

