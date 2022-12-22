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
Funções são um tipo de dado estrutural que armazena pedaços de código os nomeado, ou seja, possibilita que possamos agrupar e reutilizar código por consequência dando um significa ao pedaço de código através da nomeação
- *Function statement* - Declaração da função
- *run, call, execute, invoke* - Executar função
```js
function soma() {  // Function statement
	x = y;  // Bloco de código
}

soma();  // Executar função
```

>[!attention] Atenção
>Não declarar variável dentro de funções sem utilizar comando `var`, `let` ou `const`, pode ocorrer da variável se tornar global para toda aplicação, podendo causar erros graves.
> - `var` - Respeita o [[#Escopo da Função (*Function Scope*)|function-scoped]]

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

# Declarando Funções Dentro de Variáveis
Podemos declarar funções dentro de uma variável técnica que se da o nome de ***function anonymous*** ou ***function expression***
```js
const sum = function(x, y) {
	return x + y
}

console.log(sum(5, 2))
```

# Escopo da Função
Escopo da função ou no mais conhecido em inglês **_Function Scope_** esta ligado com o código dentro de uma função e o funcionamento do escope das variáveis que ele interage
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
Assim como vimos o funcionamento do *hoisting* para a [[01 - Notes/Code/JavaScript/Introdução#Variáveis e Constante|declaração de variável]] utilizando o comando `var`, existem o *function hoisting* para funções onde mesmo chamando a função antes de criara ele funcionara normalmente, pois, ocorre o *function hoisting* que é como se joga-se as declarações de funções para o inicio do código, independente de onde tenha escrito.
```js
sayMyName();  // Resultado: 'Wesley'

function sayMyName() {
	console.log('Wesley');
};
```

>[!attention] Atenção
>*Function Hoisting* só ocorre quando declaramos a função através do comando `function`, caso a declaramos de forma anônima, apresentara erro, mesmo utilizando `var`, pois como visto sobre [[01 - Notes/Code/JavaScript/Introdução#Variáveis e Constante|declaração de variável]] o *hoisting* do `var` eleva somente a declaração e não a atribuição de valor
>```js
>sayMyName() // Resultado: ERRO!
>
>var sayMyName = function() {
>	console.log('Wesley')
>}
>```

# *Arrow Function*
Forma mais moderna e compacta de escrever funções, onde omitimos o comando `function` e após a definição dos parâmetros criamos uma espécie de flecha utilizando os caracteres igual e maior, em seguida abrindo para o bloco de código da função
```js
const sayMyName = (name) => {
	console.log(name)
}
```
Utilizando apenas um parâmetro, podemos omitir os parênteses, ficando da seguinte forma
```js
const sayMyName = name => {
	console.log(name)
}
```

# *Callback Function*
Callback do inglês chamar de volta, Se recapitularmos o que vimos sobre [[01 - Notes/Code/JavaScript/Introdução#Variáveis e Constante|declaração de variável]], foi estabelecido que funções são um tipo de dado, sento um tipo de dado, podemos passar como argumento/parâmetro de uma função, criando a ideia de uma função chamar outra função.
```js
function sayMyName(name) {
	console.log('Antes de executar a função callback')
	name()
	console.log('Depois de executar a função callback')
}

sayMyName(() => {
	console.log('Estou em um callback')
})
```

>[!note]- Estudo com Testes
>```js
>function a(arg) {
  console.log('before')
  console.log(arg)
>	console.log(arg())
  arg()
  console.log('after')
}
>
console.log('-------------Primeiro Teste---------------')
a(() => {
  console.log('Executando a função')
  return 'Retorno da arrow function'
})
>/* [Function (anonymous)]
>Executando a função
>Retorno de arrow function
>Executando a função*/
console.log('------------------------------------------')
>
console.log('-------------Segundo Teste---------------')
a(() => {
  return 'Retorno da arrow function'
  console.log('Executando a função')
})
>/* [Function (anonymous)]
>Retorno da arrow function */
console.log('------------------------------------------')
>
console.log('-------------Terceiro Teste---------------')
function b() {
  console.log('Executando a função')
  return 'Retorno da função'
}
a(b()) 
/* Retorno da função
ERRO! "arg" não é uma função */
console.log('------------------------------------------')  
>
console.log('-------------Quarto Teste---------------')
const c = function() {
  console.log('Executando a função')
  return 'Retorno da função'
}
a(c)
a(c())
>/* [Function: c]
>Executando a função
>Retorno da função
>Executando a função
>Executando a função
>Retorno da função
>ERRO! "arg" não é uma função */
console.log('------------------------------------------')
>
console.log('-------------Quinto Teste---------------')
const d = () => {
  console.log('Executando a função')
  return 'Retorno da função'
}  
a(d)
a(d())
>/* [Funciton: d]
>Executando a função
>Retorno da Função
>Executando a função
>Executando a função
>Retorno função
>ERRO! "arg" não é um função */
console.log('------------------------------------------')
>
console.log('-------------Sexto Teste---------------');
function z(arg) {
  let x = ' Testando';
  console.log('before');
  console.log(arg(x));
  console.log('after');
}
>
z(x => {
  return 'Teste' + x;
});
// Teste testando
console.log('------------------------------------------');
>```

# *Function Constructor*
*Function Constructor* ou do português função construtora, é quando utilizamos do comando `new` e criamos um novo objeto a partir de uma função, utilizando esse método temos acesso ao `this` que esta se referenciando a si mesmo
- Funções construtoras por convenção se inicia com um caractere maiúsculo
- Lembre-se não é um objeto e sim uma função que instancia objetos, por isso o sinal de igual e a não separação por virgula
```js
function Person(name) {
	this.name = name
	this.walk = function() {
		return this.name + " está andando"
	}
}

const wesley = new Person("Wesley"); // Instanciando um objeto wesley do tipo "Person"
console.log(wesley.name) // Resultado: 'Wesley'
console.log(wesley.walk()) // Resultado: 'Wesley está andando'
```