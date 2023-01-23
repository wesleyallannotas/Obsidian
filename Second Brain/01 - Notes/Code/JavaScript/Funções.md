---
title: Funções JavaScript
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Como criar e utilizar funções
---
# Introdução
Funções são um tipo de ==dado estrutural== que armazena pedaços de código os nomeado, ou seja, possibilita que possamos agrupar e reutilizar código por consequência dando um significa ao pedaço de código através da nomeação
- *Function statement* - Declaração da função
- *run, call, execute, invoke* - Executar função
```js
function soma(x, y) {  // Function statement
	return x + y;  // Bloco de código
}

const somaAnonima = function(x, y) {  // Função anonima
	return x + y;
}

const somaArrow = (x, y) => x + y;  // Arrow Function, omitindo return

soma(2, 5);  // Executar função
somaAnonima(2, 5);
somaArrow(2, 5)
```

>[!attention] Atenção
>Não declarar variável dentro de funções sem utilizar comando `var`, `let` ou `const`, pode ocorrer da variável se tornar global para toda aplicação, podendo causar erros graves.
> - `var` - Respeita o [[Funções#Escopo da Função|function-scoped]]

# Parâmetros
Nossa função pode conter parâmetros que podem ser atribuídos durante a chama da função, onde a função terá acesso a esses valores para utilizar no seu bloco de código.
```js
var total;

function soma(x, y) {
	total = x + y;
}

soma(2, 5);
console.log(total);
```

# Retorno
Funções retornam valor através do uso do comando `return` caso não possua retornara `undefined`, assim quando chamarmos uma função ela executara o seu bloco de código e "cospe" o retorno podendo ser capturado, por uma variável, ser usado como parâmetro para outra função, entre outros
```js
function soma(x, y) {
	return x + y;
}

let total = soma(2, 5);
console.log(total);

console.log(soma(3, 4));

console.log(soma(soma(1, 2), 5));
```

>[!attention] Atenção
>Quando usamos o comando `return` é interrompido a execução da função, e executando o retorno, esse comportamento pode ser inteligentemente utilizado para simplificar o código

# Escopo da Função
Escopo da função ou no mais conhecido em inglês **_Function Scope_** esta ligado com o código dentro de uma função e o funcionamento do escope das variáveis que ele interage
>[!attention] Atenção
>Não é recomendável declarar variável sem um operador.
>```js
>teste = 'Teste';
>```
```js
// Mesma identificador, esopo diferente
let name = 'Wesley'

function repeat(name) {
	name = 'Andressa'
	return name
}

console.log(repeat(name))  // Resultado: 'Andressa'
console.log(name)  // Resultado: 'Wesley'

// Mesmo identificador, mesmo escopo
let name = 'Wesley'

function alter() {
	name = 'Andressa'
	return name
}

console.log(reat(name))  // Resultado: 'Andressa'
console.log(name)  // Resultado: 'Andressa'

// OU

let name = 'Wesley'

function alter(seila) {
	name = 'Andressa' + seila
	return name + seila
}

console.log(reat(name))  // Resultado: 'AndressaWesley'
console.log(name)  // Resultado: 'AndressaWesley'
```
Basicamente ele ==prioriza o parâmetro==, se tiver um parâmetro com o mesmo nome de variável interno ele utiliza o parâmetro, ==caso não exista, busca no escopo anterior==, e em ==ultimo caso cria a variável==

# *Function Hoisting*
Assim como vimos o funcionamento do *hoisting* para a [[Introdução ao JavaScript#Variáveis e Constante|declaração de variável]] utilizando o comando `var`, existem o *function hoisting* para funções onde mesmo chamando a função antes de cria-la ele funcionara normalmente, pois, ocorre o *function hoisting* que é como se joga-se as declarações de funções para o inicio do código, independente de onde tenha escrito.
```js
sayMyName();  // Resultado: 'Wesley'

function sayMyName() {
	console.log('Wesley');
};
```

>[!attention] Atenção
>*Function Hoisting* só ocorre quando declaramos a função através do comando `function`, caso a declaramos de forma anônima, apresentara erro, mesmo utilizando `var`, pois como visto sobre [[Introdução ao JavaScript#Variáveis e Constante|declaração de variável]] o *hoisting* do `var` eleva somente a declaração e não a atribuição de valor
>```js
>sayMyName() // Resultado: ERRO!
>
>var sayMyName = function() {
>	console.log('Wesley')
>}
>```

# *Arrow Function*
Forma mais moderna e compacta de escrever funções, onde omitimos o comando `function` e após a definição dos parâmetros criamos uma espécie de flecha utilizando os caracteres igual e maior, em seguida abrindo para o bloco de código da função

>[!attention] Atenção
>_Arrow Function_ não tem seu próprio _[this](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/this)_, _[arguments](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Functions/arguments)_, _[super](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/super)_ ou _[new.target](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/new.target)_, nem mesmo a propriedade [[Manipulando Dados#Prototype|prototype]], sendo assim, não é recomendado essa expressão para construção de métodos e _contructors_

```js
const sayMyName = (name) => {
	console.log(name)
}
```
Utilizando apenas um parâmetro, podemos omitir os parênteses, ficando da seguinte forma, mas caso não aja nenhum parâmetro é necessário adicionar os parênteses vazios.
```js
const sayMyName = name => {
	console.log(name)
}
```
Quando possui apenas uma linha retorna automaticamente, sem a necessidade do `return`.
```js
const square = n => n * n;
```

# *Callback Function*
Callback do inglês chamar de volta, Se recapitularmos o que vimos sobre [[Introdução ao JavaScript#Tipos de Dados|tipos de dados]], foi estabelecido que funções são um tipo de dado estrutural, sento um tipo de dado, podemos passar como argumento/parâmetro de uma função, assim sendo passado sua referencia na memoria, onde a função pode utiliza-la, criando a ideia de uma função chamar outra função de volta após um certo tempo.

```js
function say(name) {
	console.log('Antes de executar a função callback')
	console.log(name())
	console.log('Depois de executar a função callback')
}

function fn() {
	return 'Estou em um callback'
}

say(fn)

say(() => {
	return 'Estou em um callback'
})
```

# *Function Constructor*
*Function Constructor* ou do português função construtora tem como objetivo conter instruções para a instanciação de objetos, é quando utilizamos o **operador `new`** cria uma instancia de um tipo de objeto definido pelo usuário ou de um dos tipos nativos (_built-in_) que possuem uma função construtora, utilizando esse método temos acesso ao `this` que esta se referenciando a si mesmo
- Funções construtoras por convenção se inicia com um caractere maiúsculo
- Lembre-se não é um objeto e sim uma função que instancia objetos, por isso o sinal de igual e a não separação por virgula

```js
function Person(name) {
	this.name = name;
	this.walk = function() {
		return this.name + " está andando"
	};
};

const wesley = new Person("Wesley"); // Instanciando um objeto wesley do tipo "Person"
console.log(wesley.name); // Resultado: 'Wesley'
console.log(wesley.walk()) // Resultado: 'Wesley está andando'
```

# Parâmetro Rest
A sintaxe do _rest parameter_ nos permite representar um número indefinido de parâmetros/argumentos como uma _array_, possuímos a liberdade de possuir apenas um parâmetro _rest_, ou outros parâmetros e depois o parâmetro _rest_. De certa forma é usada para desestruturar arrays e objetos, a _sintaxe rest_ é o oposto da _sintaxe de espalhamento_ [[Expressões e Operadores#Operador Spread|Spread]]. A _sintaxe de espalhamento (spread)_ 'expande' um array em vários elementos, enquanto a _sintaxe rest_ coleta múltiplos elementos e 'condensa' eles em um único elemento. 

```js
function sum(...values) {
	return values.reduce((total, value) => total + value);
}

function operacao(op, ...values) {
	switch (op) {
		case 'add':
			return values.reduce((total, value) => total + value);
		case 'sub':
			return values.reduce((total, value) => total - value);
		case 'mult':
			return values.reduce((total, value) => total * value);
		case 'div':
			return values.reduce((total, value) => total / value);
	}

}

console.log(sum(2, 5, 8, 9, 10, 15, 17));
console.log(operacao('add', 2, 5, 8, 9, 10, 15, 17));
console.log(operacao('sub', 2, 5, 8, 9, 10, 15, 17));
console.log(operacao('mult', 2, 5, 8, 9, 10, 15, 17));
console.log(operacao('div', 2, 5, 8, 9, 10, 15, 17));
```