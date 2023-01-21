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
| ++Value  | Incremento antes       |
| Value--  | Decremento apos        |
| --Value  | Decremento antes       |

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

## Decidir Valores
Operador de **OU** (`||`) e **Coalescência Nula** (`??`), são muito utilizados para atribuir valor também, a difernaça base entre elas é que **coalescência nula** não sobre com [[Falsy e Truthy|Falsy]],  assim adicionando o valor a esquerda apenas quando for `Null` ou `Undefined` por exemplo.

```js
let age = 0;

console.log(`Ele tem ${age || 1} ano de idade`);  // Exibira 1
console.log(`Ele tem ${age ?? 1} ano de idade`);  // Exibira 0
```

# Operador de Agrupamento
Através do operador de *grouping operator* que é o parênteses `( )`, podemos agrupar operadores, podemos modificar a ordem de precedência nas nossas expressões, funciona desde realização de operações aritméticas ate para expressões condicionais.

```js
console.log(1 + 2 * 5);   // Resultado: 11
console.log((1 + 2) * 5); // Resultado: 15
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

# Operador *new*
A expressão `new` é classificada como uma *left-hand-side expression*, basicamente é uma expressão que serve para criar/instanciar uma objeto.

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

# Operador Spread
_Spread_ ou espalhamento permite que um objeto iterável, como uma [[Array]], [[Introdução ao JavaScript#String|String]], sejam **expandidas** para serem usadas como argumentos de funções, elementos para uma _array_, ou no caso de [[Introdução ao JavaScript#Object|Objetos]], para elementos de um novo objeto, até mesmo possibilitando a troca de valores de propriedades. A _sintaxe de espalhamento (spread)_ **expande** um _array_ em vários elementos, enquanto a _sintaxe [[Funções#Parâmetro Rest|Rest]]_ coleta múltiplos elementos e **condensa** eles em um único elemento.

```js
// Novas Arrays e Parâmetro
function sum(a, b, c=0, d=0, e=0) {
  return a + b + c + d + e;
}

const values = [5, 10, 15];          // 5, 10, 15
const values2 = [...values, 20];     // 5, 10, 15, 20
const values3 = [1, ...values, 20];  // 1, 5, 10, 15, 20

console.log(sum(...values));   // 30
console.log(sum(...values2));  // 50
console.log(sum(...values3));  // 51

// Junto com New
var dataField = [1970, 0, 1];
var d = new Date(...dataField);
console.log(d);

// Objetos
let obj1 = { foo: 'bar', x: 42 };
let obj2 = { foo: 'baz', y: 13 };
const clonedObj = { ...obj1 };            // { foo: "bar", x: 42 }
const mergedObj = { ...obj1, ...obj2 };  // { foo: "baz", x: 42, y: 13 }
console.log(clonedObj, mergedObj);
```

>[!attention] Atenção com essa característica
>Quando utilizamos o operador _spread_ para clonar objetos é feito o que é chamado de **_Shallow Cloning_ (Clonagem Rasa)**, onde o que ocorre é que é clonado de fato apenas o objeto raiz, ou seja, caso possua sub-objetos, a _Spread_ não ira clonar, e sim criar uma referencia (Apontamento para o mesmo endereço).

```js
// Shallow Cloning
let obj = {
	foo: 'bar',
	x: 42,
	bar: 'foo',
	// Sub-objeto não será clonado e sim referenciado
	object: {
		subFoo: 'bar',
		subX: 42,
		subBar: 'foo'
	}
}

let obj1 = {...obj}
obj1.foo = 'Mudei';
obj1.bar = 'Mudei também';
obj1.object.foo = 'Mudei';        // Alterando aqui, altera os dois, pois, é uma referencia
obj1.object.bar = 'Mudei também';
console.log(obj);
console.log(obj1);
```

# Operadores de Desestruturação
Operadores de atribuição via desestruturação ou do inglês _destructuring assignment_ São operadores que permitem extrair dados de [[Introdução ao JavaScript#Array|Arrays]] ou [[Introdução ao JavaScript#Object|Objetos]].

## Array
Para desestrutura uma _array_ basta usarmos o mesmo sinal para criação de uma, porem dessa vez do lada da declaração das variáveis, ficando da seguinte forma.
Temos liberdade para utilização do [[#Operador Spread]]

```js
// array
let array = [1, 2, 3, 4, 5];

// desestruturação
let [n1, n2, n3, n4, n5] = array;

// com Spread
let [n1, ...resto] = array;

// Valor padrão
let [n1=0, n2=0, n3=0, n4=0, n5=0] = array;
```

A _array_ será desestruturada em outras varias variáveis independentes.

## Object
A desestruturação de objetos é mais complexa por se tratar de uma estrutura com valores nomeados, ou seja, chaves que contem valores, para realizarmos a desestruturação é necessário utilizar o mesmo sinal para criar objetos porem do lada da atribuição, onde caso queiramos manter o mesmo dome da chave, basta utiliza-la, mas caso desejar renomear, podemos utilizar o nome da propriedade, dois pontos, novo nome.
Podemos passar valor padrão para caso não exista a propriedade/chave no objeto.

```js
metadata = {
    title: "Scratchpad",
    translations: [
       {
        locale: "de",
        localization_tags: [ ],
        last_edit: "2014-04-14T08:43:37",
        url: "/de/docs/Tools/Scratchpad",
        title: "JavaScript-Umgebung"
       }
    ],
    url: "/pt-BR/docs/Tools/Scratchpad"
};
// Mantendo
let {title, translation, url} = person;

// Alterando
let {title: tituloIngles, translations: tradução, url: localizacao} = person;

// Aninhando e Ignorando uma propriedade
let {title: tituloIngles, translations: [{title: titulo}]} = person;
```