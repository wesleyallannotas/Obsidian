---
title: Expressões e Operadores com JavaScript 
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Aprenda expressões e operadores no javascript
---
# Expressão
Expressões são qualquer linha de código que resolve algo por exemplo `let number` uma expressão que declara uma variável com o nome `number`, um expressão pode ou não terminar com ponto e virugla "*;*", pois no JavaScript não é obrigatório

# Operadores
Operadores ou no inglês **_Operators_** são os responsáveis por realizar operações com valores, sendo assim ele possui classes de operadores sendo elas, *binary*, *unary* e *ternary*, o mais conhecido são os operadores binários que como o nome já induz necessita de dois valores por exemplo `2 + 2`.

## *Binary*
Operadores binários ou do inglês *binary* necessitam de dois valores para realizar a operação, por exemplo operações aritméticas.

```js
let number = 1;

console.log(number + 1)
console.log(number / 2)
```

![[Desenho_JS_Operador_Binary|center]]

## *Unary*
Operadores unários o  do inglês *unary* necessitam de um valor apenas para realizar a operação, por exemplo operações de incremento, outros operadores
- `typeof` - Tipo do dado
- `delete` - Deletar

```js
let number = 1;

console.log(++number) 
console.log(typeof number)

const person = {
	name: "Wesley",
	age: 24,
};

delete person.age;
```

![[Desenho_JS_Operador_Unary|center]]

>[!attention] Atenção
>O incremento `++number` e diferente de `number++`, no caso ambos possui o mesmo fim adicionando mais 1 ao valor da variável, porem da primeira forma ele realizada o incremento primeiro depois mostra valor, segundo forma mostra valor e depois realiza o incremento, tomar cuidado, pois, esse comportamento pode causar bugs

## Ternary
Operadores ternários ou do inglês *ternary* necessita de 3 valores, sendo eles uma expressão, e em seguida duas possíveis caminhos sendo um realizado caso seja verdadeiro e outro para o falso

```js
let age = 18;
console.log(age > 17 ? `Maior de idade, possui ${age} anos` : `Menor de idade, possui ${age} anos`)

let x = 1
console.log(1 > 0 ? 'Maior' : 'Menor')
```

![[Desenho_JS_Operador_Ternary|center]]

# Operador *new*
A expressão `new` é classificada como uma *left-hand-side expression*, basicamente é uma expressão que serve para criar/instanciar uma objeto

```js
let name = new String('Wesley');
let num = new Number(24);
let date = new Date('2022-12-22');
```

# Operador de Encadeamento Opcional
O operador de encadeamentos opcional (_Optional Chaining_), verifica se existe o encadeamento interno, caso não encontre retorna um `undefined` em vez de causar um erro, também funciona para métodos.

```js
const wesley = {
	name: 'Wesley',
	lastname: 'Silva',
	age: 24,
	properties: {
		cars: {
			saveiro: {
				model: 'G4',
				year: 2007
			}
		}
	},
	getMoney: () -> {};
}

console.log(wesley.pets.cat); // Retorna erro de referencia
console.log(wesley.pets?.cat) // Retorna `undefined`
console.log(wesley.getSaldo?.()) // Retorna `undefines`
console.log(wesley.getSaldo()) // retorna erro de referencia
```

# Operadores Aritméticos
Os operadores aritméticos tem como função realizar operação para manipulação de valor

| Operador | Operação               |
| -------- | ---------------------- |
| +        | Soma, Concatenação     |
| -        | Subtração              |
| *        | Multiplicação          |
| /        | Divisão                |
| %        | Modulo (Resto divisão) |
| **       | Exponencial            |
| Value++  | Incremento apos        |
| ++Valur  | Incremento antes       |
| Value--  | Decremento apos        |
| --Value  | Decremento antes       |

# Operador de Agrupamento
Através do operador de *grouping operator* que é o parênteses `( )`, podemos agrupar operadores, podemos modificar a ordem de precedência nas nossas expressões, funciona desde realização de operações aritméticas ate para expressões condicionais.

```js
console.log(1 + 2 * 5);   // Resultado: 11
console.log((1 + 2) * 5); // Resultado: 15
```

# Operadores de Comparação
Compara valores e retorna um booleano com o resultado obtido.

| Operador | Comparação             |
| -------- | ---------------------- |
| !=       | Diferente              |
| !==      | Estritamente diferente |
| ==       | Igual                  |
| ===      | Idêntico               |
| >        | Maior                  |
| <        | Menor                  |
| >=       | Maior igual a           |
| <=       | Menor igual a           |

```js
let x, y;

x = 1;
y = '1';

console.log(x == y)   // Resultado: True
console.log(x === y)  // Resultado: False
console.log(x != y)   // Resultado: False
console.log(x !== y)  // Resultado: True
```

# Operadores de Atribuição (Assignment)
Operadores de  atribuição ou do inglês *assignment*, responsáveis por atribuir valor

| Operador | Operação                                                |
| -------- | ------------------------------------------------------- |
| =        | Atribuição (Assignment)                                 |
| +=       | Atribuição de soma (addition assignment)                |
| -=       | Atribuição de subtração (subtraction assignment)        |
| \*=      | Atribuição de multiplicação (multiplicaiton assignment) |
| /=       | Atribuição de divisão (division assignment)             |
| %=       | Atribuição de resto (remainder assignment)              |
| \*\*=    | Atribuição de Exponenciação (exponettation assignment)  |

# Operadores Lógicos (Logical Operators)
Operadores que permitem a comparação de dois operadores booleanos que retornam um booleano

| Operador | Operação  |
| -------- | --------- |
| &&       | E (and)   |
| \|\|     | OU (or)   |
| !        | Não (not) |
| ??       | Coalescência Nula          |

- `&&` - Todas verdadeira para retornar verdadeiro
- `||` - Um verdadeira para retornar verdadeiro
- `!` - Negar (Inverter), verdadeiro vira falso
- `??` - O operador de coalescência nula (_Nullish Coalescing Operator_) é um operador lógico que retorna o seu operando do lado direito quando o seu operador do lado esquerdo é `null` ou `undefined`. Caso contrário, ele retorna o seu operando do lado esquerdo. Foi pensado, pois, quando usado o operador OU (`||`), pode ocorrer o [[Falsy e Truthy|Falsy]] assim mesmo possuindo valor pegando o operando direito.

# Operador Condicional (Ternário)
Operadores que permitem a partir de uma condição atribuir um valor ou outro.

![[Desenho_JS_Operador_Ternary|center]]

```javascript
let age = 16;
console.log(age > 17 ? "Maior de Idade" : "Menor de Idade");

let pao = true;
let queijo = false;
let niceBreakfast = pao && queijo ? 'Cafe top' : 'Cafe ruim';
console.log(niceBreakfast); // Resultado: Cafe ruim
niceBreakfast = pao || queijo ? 'Cafe top' : 'Cafe ruim';
console.log(niceBreakfast); // Resultado: Cafe top
niceBreakfast = !(pao || queijo) ? 'Cafe top' : 'Cafe ruim';
console.log(niceBreakfast); // Resultado: Cafe ruim
```

# Precedência de Operadores
Precedência de operadores ou no inglês *Operator precedence* é a ordem de execução das operações através do peso do operador, por exemplo na operação `2 + 1 * 3` não é lido e realizado da esquerda para direita, é analisado a precedência onde a multiplicação tem mais peso, assim sendo executado primeiro resultando em `2 + 3` em seguida é realizado a soma resultando em `5`, se fosse lido e executado da esquerda pra direita o resultado seria `9`. Segui a ordem de precedência.
1. Grouping - `( )`
2. Negação e incremento - `! ++ --`
3. Exponencial - `**`
4. Multiplicação e divisão - `* /`
5. Adição e subtração - `+ -`
6. Relacional - `< <= > >=`
7. Igualdade - == != === !\=\=
8. E (*and*) - `&&` 
8. OU (*or*) - `||`
9. Condicional - `?:`
10. Atribuição (*Assignment*) - = += -= *= /= %= **=

