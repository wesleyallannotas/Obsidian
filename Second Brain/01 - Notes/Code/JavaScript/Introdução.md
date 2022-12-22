---
title: Introdução a JavaScript 
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: javascript
description: Iniciando no javascript
---
# Introdução
JavaScript é uma linguagem de programação que roda nativamente nos navegadores Web no lado do cliente, ou seja, no computador do usuário conhecido como *front-end*, onde sua função é trazer dinamismo a página, posteriormente foi se criado soluções para o JavaScript rodar localmente nos servidores, se tornando uma linguagem também muito usada para o *back-end*, algumas tecnologias baseadas na linguagem JavaScript
- **Back-End** - Node.js, Deno
- **Front-End** - React, React-Native
- **Desktop** - Electron

# Sintaxe
Toda linguagem possui uma sintaxe e com o javascript não é diferente, assim possuindo uma forma correta de ser escrever, são regras que devemos seguir para o nosso código funcionar corretamente
```js
// Erro 
consolelog("Bem vindo ao Starter"); 

// Erro 
console.log("
Bem vindo ao Starter"); 

// Correto
console.log("Bem vindo ao Starter");
```

>[!attention] Atenção
>Utilizar o ponto e virgula "**;**" no fim de cada comando não é obrigatório no JavaScript, é recomendado seguir um padrão dentro do projeto, se for utilizar sempre uso, se não for nunca uso

# Comentários
Assim como toda linguagem de programação, JavaScript também tem comentários
```js
// Comentario em linha

/*
Comentário em bloco
*/
```

# Tipos de Dados
Quanto mais vocabulário tivermos dentro da linguagem mais ferramentas teremos a nossa disposição para solucionar os problemas, tipos de dados são importantíssimos para que possamos manipular e utilizar nossos dados corretamente para gerar informação==, conforme o ECMAScript standard temos 9 tipos de dados==, separados nas categorias ou mais corretamente **Data Types**:
- Primitive / Primitive value
- Structural
- Structural Primitive

>[!note] Descobrindo Tipo
>Através do comando `typeof` podemos descobrir o tipo da nossa variável
>```js
>	let clime = "Quente";
>	console.log(typeof clime)
>```

## Primitivos (*Primitive*)
Não é um objeto, ou seja, não possui uma estrutura, e tem seu valor imutável
- String
- Number
- Boolean
- Undefined
- Symbol
- BigInt

## Estuturais (*Structural*)
Dentro da categoria de estruturais temos dois, **objetos** (*Object*) e **funções** (*function*).
- Object
	- Array
	- map
	- Set
	- Date
	- Entre outros...
- Function

## Primitivos Estrutural (*Structural Primitive*)
- Null

## String
O tipo de dado `string` nada mais é do que uma cadeia de caracteres (`char`), cada letra é um caractere (`char`) que é numerado a partir do 0, são declaras utilizando:
```js
let nome = 'Wesley'; /* Aspas SImples */
nome = "Wesley"; /* Aspas Duplas */
nome = `Wesley`; /* Template Strings */
```

### Template Strings
São *strings* mais poderosas que permitem expressões embutidas, Você pode _utilizar string_ multi-linhas e interpolação de _string_ com elas. ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Template_literals))
Template Strings são envolvidas pelo sinal de acentos graves
```js
let name, age

name = 'Wesley'
age = 24

console.log(`Ola ${name}, você tem ${age} anos de idade?`)
```

## Number
 O tipo de dado `number` nada mais é do que um número, sendo ele com ponto flutuante ou não, em JavaScript não existe a separação
```js
let idade = 25;
idade = 18.5;
idade = NaN; // Not a number
idade = Infinity;
```

## Boolean
O tipo de dado `boolean` é o responsável por armazenar o valor Verdadeiro `true` ou Falso `false`
```javascript
let homem = true;
mulher = false;
```

## Undefined
Tipo de dado `undefined` em tradução livre indefinido, é encontrado quando declaramos a variável, porem não atribuímos nenhum valor.
```js
let idade;
console.log(idade); // Resultado: Undefined
```

## Null
Tipo de dado `null` é considerado no JavaScript um ==objeto que não tem nada dentro==, ou seja, diferente de `undefined`
```js
let casa = null;
console.log(null);
```

## Object
Tipo de dado `object` é um ==tipo de dado estrutural==, pois, ele cria uma estrutura que possui ==propriedades (atributos) e funcionalidades (métodos)==, também chamado de relação chave (*key*) valor (*value*), possui a estrutura `{propriedade: "valor}`
```js
let pessoa = {
	nome: "Wesley",
	sobrenome: "Silva",
	idade: 24,
	andar: function() {
		console.log("andou");
	}
};
```
Para chamar um item do nosso objeto, basta especificar o caminho por exemplo `pessoa.nome` trará o valor da propriedade/chave `nome` no objeto (*Object*) `pessoa`

## Array
Tipo de dado `array` também chamado de vetores é um ==tipo de dado estrutural==, pois, ele cria uma estrutura que lista valores a partir de um *index* que se inicia em `0`, é uma lista heterogênea que aceita qualquer tipo de dado podem assim mistura-los
```js
let pessoa = [
	"Wesley", 
	"Silva", 
	24,
	function() {
		console.log("andou")
	},
	{
		father: "Antionio",
		mother: "Cazemira"
	}
]
```
Para chamar um item da nossa *Array* basta especificar qual o nome da *Array* e entre colchetes o *index* do item a ser acessado, por exemplo `pessoa[3]()`, `pessoa[0]`, `pessoa[4].mother`

# Variáveis e Constante
Variáveis são ==espações alocados na memoria que são nomeados para guardar valor==, no caso de ==variáveis possibilitando a variação== do seu valor durante a execução já ==constantes impossibilitando a alteração== após seu valor ser atribuído, podemos armazenar nas mesmas algum valor, atalhos de código ou identificadores, possuem as seguintes formas de declaração
- **Variável**
	- `let` - Local no escopo do bloco atual, disponível apenas no bloco, diferente do `var` não possui *hoisting*
	- `var` - Escopo global, possibilitando ser acessado em qualquer lugar mesmo sendo criado dentro de um bloco, quando utilizamos `var` por baixos dos panos é como se o JavaScript coloca todas as declarações de `var` no inicio sem atribuir valor, ou seja, caso tente acessar antes da atribuição de valor retornara `undefined`, esse conceito e chamado de **_hoisting_**
```js
console.log(x); // Resultado: Undefined

{
	var x = 0
	console.log(x); // Resultado 0
}

console.log(x); // Resultado 0
```
- **Constante**
	- `const` -Local no escopo do bloco atual, diferente de `var` não possui _hoisting_
JavaScript é uma linguagem de ==tipagem fraca e dinâmica==, tipagem fraca pois não existe a necessidade de especificar o tipo da nossa variável, ele é identificada automaticamente, contrario por exemplo do Java `int idade = 30`, e dinâmica, pois, podemos mudar o tipo da nossa variável a qualquer momento, ocorrendo automaticamente ao mudar o valor

# Escopo (*Scope*)
O escopo determina a visibilidade da variável, onde ela ira existir possibilitando que seja acessada.

## Block Statement
*Block Statement* em português "Declaração de Bloco", o bloco cria um novo escopo (*scope*) chamado de *block-scoped* ou em português escopo de bloco.
```js
{ // Inicia o Bloco

// Bloco

} // Fechamento do Bloco
```

# Declaração Conjunta
Podemos agrupar declarações das variáveis
```js
let name, age, isHuman

name = 'Wesley'
age = 25
isHuman = true
```