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
	return x + y;
}

soma(2, 5);
console.log(total);
```

## Valor Padrão
Podemos adicionar valor padrão aos nossos argumentos/parâmetro, assim não os tornando obrigatório, e caso não informado assumira tal valor.

```js
var total;

function soma(x, y=0) {
    total = x + y;
}

soma(2);
console.log(total);
```

```ts
// React TypeScript
export function({title = 'Title', descripton}: CardProps) {};
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

# Function Hoisting
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

# Função Anônima
Leva esse nome por não possui um nome relacionado em sua criação, podemos criar função anônimas, quando é necessário uma referencia de função, ou apenas para assinar uma variável com determina função, muito usado para criação de _[[Assíncronismo#Callback Function|Callbacks]]_

```js
// Assinando
const soma = function(x, y) {
  return x + y;
};

// Callback
fs.readFile('./arq1.txt', function(error, response) {
  if (error) return console.log('Deu Ruim!' + error.stack);
  console.log('Resposta = ', response);
});
```

# Arrow Function
Forma mais moderna e compacta de escrever funções, onde omitimos o comando `function` e após a definição dos parâmetros criamos uma espécie de flecha utilizando os caracteres igual e maior, em seguida abrindo para o bloco de código da função, é uma espécie de [[#Função Anônima]], não havendo nomeação em sua declaração.

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

Quando possui apenas uma linha e omitimos as chaves,  retorna automaticamente, sem a necessidade do `return`.

>[!attention] Atenção
>Para funcionar é necessário omitir as chaves, caso as adicione o retorno será `undefined`

```js
const square = n => n * n;
```

Muito usada em [[Assíncronismo#Callback Function|Callbacks]]

```js
fs.readFile('./arq1.txt', (error, response) => {
  if (error) return console.log('Deu Ruim!' + error.stack);
  console.log('Resposta = ', response);
});
```

# Referencia de Função
Podemos realizar a referencia a uma função basicamente passando seu nome invés de executa-la, tem o mesmo efeito de declara uma função anônima ou [[#Arrow Function]]

```js
function respostaLeituraArq(err, resp) {
  if (err) return console.log('Erro!', err.stack);
  console.log('Respota =', resp.message);
}
  
fs.readFile('./arq1.txt', respostaLeituraArq);
```

# Composição de Funções
Basicamente é um encadeamento de funções onde, uma função retorna um dado que vai para outra função, isso se repetindo quantas vezes for necessário.

```js
const people = ['Rafa', 'Diego', 'Dani', 'Rod'];
const upperCasePeopleThatStartsWithD = people
                                       .filter(person => person.startsWith('D'))
                                       .map(dperson => dperson.ToUpperCase())
```

Método de _arrays_ `filter()`, pega a _array_ e monta outra através do que for retornar pela função passada como parâmetro (_Higher-Order Function_), onde, o método de _array_ `map()` percorre essa _array_ executando executando uma função que é passada como parâmetro (_Higher-Order Function_).
Vale lembrar que por ser uma [[Funções#*Arrow Function*|Arrow Function]] de uma linha, já esta retornando o valor, mesmo com o comando `return` omitido.

# Function Constructor
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
# this
A palavra-chave **`this`** comporta-se um pouco diferente em Javascript se comparado com outras linguagens, Em muitos casos, o valor `this` é determinado pela forma como a função é chamada. Ele não pode ser assinado durante a execução.

```js
obj = {
  nome: 'Wesley',
  getNome() {
    return this.nome
  },
  getNomeArrow: () => this.nome
}
  
console.log(nome)  
// {nome: 'Wesley', getNome: [Function: getNome], getNomeArrow: [Function: getNomeArrow]}
console.log(obj.nome);
// 'Wesley'
console.log(obj.getNome());
// 'Wesley'
console.log(obj.getNomeArrow());
// undefined
```

## Vinculação Padrão
Quando chamamos uma função no escopo global nossa função estará associada ao objeto global, no [[Introdução ao Node|Node]] o nosso `this` referenciara ao Objeto Global, já no navegador nosso `this` referenciara o `window`.

```js
function mostraThis() {
 console.log(this);
}
mostraThis(); // Objeto Global
```

## Vinculação Implícita
Quando criamos um método, ou seja, uma função dentro de um objeto, nossa `this` terá como referencia o ambiente onde reside, ou seja, o próprio objeto.

```js
const obj = {
	nome: 'Wesley',
	mostraThis() {
		console.log(this);
	}
}

obj.mostrThis();
```

## Vinculação de Eventos
Quando disparamos um evento, na nossa função de [[Assíncronismo#Callback Function|Callback]], podemos pegar o elementos que realizou o disparo.

```js
const botao = document.getElementById('botao');

botao.addEventListener('click', () => {  // Errado!
  console.log(this);
})
  
botao.addEventListener('click', function() {
  console.log(this);
})
```

[[#Arrow Function]] não possui a ideia de `this`, assim de forma erronia será referenciado o objeto global `window`, agora utilizando a [[#Função Anônima|Função Anônima Padrão]] ou [[#Referencia de Função]] teremos acesso ao `this` referenciando ao objeto que gerou o evento. 

## (call, apply) Vinculação Explicita
Podemos criar vinculações do `this`, ou seja, definir o `this` através o método `call` ou `apply`.
- `call` - Podemos vincular um `this` explicitamente e passamos argumentos/parâmetros em sequencia
- `apply` - Podemos vincular um `this` explicitamente e passar uma [[Introdução ao JavaScript#Array|Array]] com os argumentos/parâmetros.

```js
const jogo = {
  nome: 'GTA',
  ano: 2013
}

const carro = {
  nome: 'Saveiro',
  ano: 2007,
  mostraNome() {
    console.log(this.nome);
  },
  trocaAno(ano) {
    this.ano = ano;
  },
  trocaTudo(nome, ano) {
    this.nome = nome,
    this.ano = ano
  }
}

carro.mostraNome();           // Resultado: 'Saveiro'
carro.mostraNome.call(jogo);  // Resultado: 'GTA'
  
carro.trocaAno.call(jogo, 2014);
console.log(jogo.ano);
carro.trocaAno.apply(jogo, [2015])
console.log(jogo.ano);
  
carro.trocaTudo.apply(jogo, ['Teste', 2009]);
console.log(jogo)
carro.trocaTudo.call(jogo, 'Teste2', 2010);
console.log(jogo);
```

## (bind) Criando Funções com Vinculação
Podemos criar novas funções ou métodos utilizando o `bind` para especificar o `this` dessa função ou método.

```js
const obj = {
  nome: 'Wesley',
  ano: 2007,
  mostraThis() {
    console.log(this);
  },
  trocaAno(ano) {
    this.ano = ano;
  }
}
  
const obj2 = {
  ano: 2015
}
  
obj.mostraThis();
  
const mostraThis2 = obj.mostraThis.bind(obj2);
mostraThis2();
  
const trocaAno2 = obj.trocaAno.bind(obj2);
trocaAno2(2020);
console.log(obj2);
  
const trocaAno2023 = obj.trocaAno.bind(obj2, 2023);
trocaAno2023();
console.log(obj2);
```

## Vinculação com Função Construtora
Ao utilizarmos o `this` em [[Funções#Function Constructor|Function Constructor]] ou em um construtor de [[01 - Notes/Code/JavaScript/Classes|Classe]]. Quando utilizarmos o [[Expressões e Operadores#Operador *new*|Operador New]] será vinculado o `this` a variável ou constante que estada recebendo referencia da instanciação.

```js
class Person {
	constructor(name, age) {
		this.name = name,
		this.age = age
	}
}

const obj = new Person('Wesley', 24);
console.log(obj);
// {name: 'Wesley', age: 24}
```

## Vinculação com Callbacks
Normalmente as _callback_ utilizando [[#Função Anônima]] ou uma função comum terá seu `this` vinculado ao contexto onde reside, ou seja, dentro da função, por exemplo no caso abaixo o `this` ira referenciar ao `mostraJogosArrow`, assim sendo necessário realizar ações para contornar esse possível problema em determinadas situações.
- Armazenando a referencia do `this` em uma variável
- Nessa caso com `forEach` temos como segundo parâmetro opcional passar uma referencia para `this`, onde podemos passar o nome do objeto, ou nesse caso como já estamos dentro de um contexto com o `this` correto, basta passar o `this`

>[!note] Arrow Function
>Nesse caso o uso de [[#Arrow Function]] na [[Assíncronismo#Callback Function|Callback]] do `forEach` já trouxe o `this` correto, pois, o `this` em uma _arrow function_ é definido pelo **contexto de execução** onde ele está sendo chamado. Em outras palavras, o `this` da _arrow function_ irá se referir ao `this` do método `mostrarJogosArrow()` que  nada mais é do que o objeto.

```js
const pessoa = {
  nome: 'Wesley',
  games: ['GTA', 'The Witcher 3', 'Cyberpunk'],
  mostrarJogosAno() {
    this.games.forEach( function(game) {console.log(`${this.nome} - ${game}`)} );
  },
  mostrarJogosArrow() {
    this.games.forEach( game => console.log(`${this.nome} - ${game}`) );
  }
}
  
pessoa.mostrarJogosAno();
pessoa.mostrarJogosArrow();
  
// Solução 1
const pessoa2 = {
  nome: 'Wesley',
  games: ['GTA', 'The Witcher 3', 'Cyberpunk'],
  mostrarJogosAno() {
    let that = this;
    this.games.forEach( function(game) {console.log(`${that.nome} - ${game}`)} );
  }
}
  
pessoa2.mostrarJogosAno();
  
// Solução 2
const pessoa3 = {
  nome: 'Wesley',
  games: ['GTA', 'The Witcher 3', 'Cyberpunk'],
  mostrarJogosAno() {
    this.games.forEach( function(game) {console.log(`${this.nome} - ${game}`)}, this );
  }
}
  
pessoa3.mostrarJogosAno();
```

# Early Return
Sabemos que em uma função quando usamos o operador `return` podemos retornar um valor, ou caso não especificado nada, retornara [[Introdução ao JavaScript#Undefined|Undefined]], é quando uma função chega no `return`, o valor será retornado e a função terá seu funcionamento encerrado, ignorando qualquer código subsequente, isso pode ser usado para melhorar a legibilidade do código, ideia base do funcionamento de funções recursivas.

```js
function Like(liked) {
	if (liked) {
		return "Você gostou!"
	}
	return "Você nào gostou!"
}
```

# Closure
Podemos com JavaScript retornar uma função através de uma função

```js
const teste = () => () => console.log('Closure');

teste()();
```

# Currying
**Currying** é o processo de transformar uma função que espera vários argumentos em uma função que espera um único argumento e retorna outra função _curried_. Por exemplo, uma função que recebe três argumentos, ao sofrer currying, resulta em uma função que recebe um argumento e retorna uma função que recebe um argumento, que por sua vez retorna uma função que recebe um argumento e retorna o resultado da função original.

```js
const pause = wait => fn => setTimeout(fn, wait);

pause(600)(() => console.log('Waiting 600ms'))  // Executando tudo de uma vez

const wait200 = pause(200);  // Currying
const wait1000 = pause(100);  // Currying

wait200(() => console.log('waiting 200ms'));
wait1000(() => console.log('Waiting 1s'));
```