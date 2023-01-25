---
title: Assíncronismo no JavaScript
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Como escrever códigos assincronos.
---
# Introdução
Quando estamos aprender a programar criamos códigos simples e que normalmente são **síncronos (_Synchronous_)**, ou seja, com uma tarefa sendo executada após a conclusão da outra, porem terá aplicações que se faz necessário continuar o fluxo do código, enquanto espera o termino da execução de uma tarefa, neste caso usaremos do **assincronismo (_asynchronous_)**.

```js
const https = require('https');
const API = 'https://jsonplacehold.typicode.com/users?_limit=2';
https.get(API, res -> {
	console.log(res.statusCode);
});
console.log('Conectando API')
```

Por se tratar de uma [[Funções#*Callback Function*|Callback Function]] que será executado após um determinado tempo dentro do método `get()`, o `console.log` de fora será impresso primeiro no console.

# Callback Function
Callback do inglês chamar de volta, Se recapitularmos o que vimos sobre [[Introdução ao JavaScript#Tipos de Dados|tipos de dados]], foi estabelecido que funções são um tipo de dado estrutural, sento um tipo de dado, podemos passar como argumento/parâmetro de uma função, assim sendo passado sua referencia na memoria, onde a função pode utiliza-la, criando a ideia de uma função chamar outra função de volta após o termino da execução

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

## Boas Praticas
Por convenção os _callbacks_ devem possuir 2 parâmetros, sendo um para erro e outro com o resultado consecutivamente, normalmente o erro é tratado primeira mente e em sequencia o que será feito com o resultado.

```js
const callback = function(error, result) {
	if(error) return console.log(error);
	return console.log(result);
};

fs.readFile("arquivo.txt", callback);
```

## Problema Teste
Mesmo problema utilizando todos os métodos de resolução.

```js
// Callbacks
terminal.question('Seu nome?\n', (res1) => {
  terminal.question('Seu Idade?\n', (res2) => {
    console.log(`Ola ${res1}, Parabens pelos seus ${res2} anos de idade!`)
    terminal.close();
  })
})
```

# Promise
Basicamente é uma promessa de que algo irá acontecer no futuro, é um objeto JavaScript usado para operações assíncronas, por exemplo, Carregar um arquivo, leitura de dados de uma API.
Para criarmos uma _Promise_ é necessário instanciar `const promessa = new Promise()` passando como parêmetro/argumento uma referencia de função.

>[!tip] Sobre then
>Toda vez que um `.then()` é executado, ele devolve uma promise por padrão.

```js
let aceitar = true;

console.log('Pedir UBER');

const promessa = new Promise((resolve, reject) => {
  if (aceitar) {
    return resolve('Carro chegou!');
  } 
  return reject('Pedido Negado!');
});

promessa
  .then(result => console.log(result))
  .catch(erro => console.log(erro))
  .finally(() => console.log('Finalizada'));

console.log('Aguardando');
```

Instanciamos um objeto _promise_ passando como parâmetro um [[Funções#*Callback Function*|callback function]], onde passamos como parâmetro o _resolve_ caso de certo, e o _reject_ caso de errado, onde essa função deve retornar através de um destes métodos o resultado.

Onde criamos a partir do método ==`then()` uma resposta para caso de certo==, ou seja atinja o estagio _fulfilled_.
A partir do método ==`catch()` uma resposta para caso de errado==, ou seja atinja o estagio _Reject_ ou execute um [[Controle de Fluxo#Throw|Throw]].

E o método ==`finally()` executara quando atingir o estagio _settled_== que é quando chega ao fim do ciclo de vida da _promise_.

## Estagios
Uma _promise_ possui estágios durante seu ciclo de vida sendo eles.
- _Pending_ - Estado inicial, assim que o Objeto da promessa é iniciado
- _Fulfilled_ - A promessa foi concluída com sucesso
- _Rejected_ - A promessa foi rejeitada, houve um erro
- _Settled_ - Seja com sucesso ou com erro, ela foi finalmente concluída

## Promise em concorrência (Paralelo) 
Através do objeto `Promise` podemos executar mais de uma _promise_ ao mesmo tempo utilizando o método `.all()`, ou seja, agrupando as execuções, como parâmetros passamos as _promises_ que suas respostas serão retornadas em uma _array_.

>[!tip] Desestruturação
>Comum utilizar desestruturação quando usado por meio do Async/Awaint

```js
// import axios from 'axios';
const axios = require('axios');

// Exemplo 1
Promise.all([
  axios.get('https://api.github.com/users/wesleyallan'),
  axios.get('https://api.github.com/users/wesleyallan/repos')
])
.then( responses => {
  console.log(responses[0].data.login);
  console.log(responses[1].data.length);
});

// Exemplo 2
async function getUserPosts(userName) {
  const api = `https://api.github.com/users/${userName}`

  const [user, repos] = await Promise.all([
    axios.get(api),
    axios.get(api+`/repos`)
  ])

  console.log(user.data);
  console.log(repos.data);
}

getUserPosts('wesleyallan');
```

## Problema Teste
Mesmo problema utilizando todos os métodos de resolução.
![[referenciaInteligente.png]]
```js
const questionAsync = question => new Promise((resolve, reject) => {
  terminal.question(`${question}\n`, resolve);
})
  
let name, age;

questionAsync('Seu nome?')
  .then(res => {
    if(!res) throw new Error('Campo Vazio!');
    name = res;
  })
  .then(() => questionAsync('Sua Idade?'))
  .then(res => {
    if(!res) throw Error('Campo Vazio!');
    age = res;
  })
  .then(() => console.log(`Ola ${name}, Parabens pelos seus ${age} anos de idade!`))
  .catch(err => console.log(err))
  .finally(() => terminal.close())
```

# Async/Await
Basicamente é uma _Syntatic Sugar_, ou seja, uma maneira mais bonita de escrever _[[#Promise]]_, é necessário criar uma função com o prefixo `async`, onde a partir dessa definição conseguimos utilizar o `await` (espera) dentro dela.

```js
const promese = new Promise(function(resolve, reject) {
	return resolve('OK!');
});

async function start() {
	const result = await promese;
	console.log(result);
};

start();
```

## Respondendo a Estados
Através da sintaxe base da [[#Promise]], podemos tratar os [[#Respondendo a Estados|estados da promise]] através dos métodos `.then()`, `.catch()` e `.finally()`, para conseguirmos o mesmo resultado utilizando [[#Async/Await]], devemos recorrer ao controle de fluxo [[Controle de Fluxo#Try|Try]].

```js
const promese = new Promise(function(resolve, reject) {
	return resolve('OK!');
});

async function start() {
	try {
		const result = await promese;
		console.log(result);
	} catch(err) {
		console.log(err);
	} finally {  // Não é obrigatorio
		console.log('Execução Finalizada!')
	}
};

start();
```

A ==função assíncrona devolve uma [[#Promise]]==, ou seja, temos aceso ao métodos da mesmo forma, podemos se desejar executar coisas como.

```js
const promese = new Promise(function(resolve, reject) {
	return resolve('OK!');
});

async function start() {
		const result = await promese;
		console.log(result);
};

start()
	.catch( err => console.log(err))
	.finally( () => console.log('Execução Finalizada!'));
```

>[!tip] Liberdade
>Temos a liberdade de capturar e tratar o erro usando a sintaxe padrão das [[#Promise]], após a execução da função assíncrona, ou tratar dentro da função utilizando o [[Controle de Fluxo#Try|Try]], porem o mais utilizado é a sintaxe com o _try_.

Temos a liberdade de misturar a vontade o uso da sintaxe base da [[#Promise]] com a criação de funções assíncronas, ate mesmo dentro da própria função.

```js
async function showUserAndRepos(userName) {
	const baseUrl = `https://api.github.com/users/${userName}`;
	
	try {
		const [user, repos] = await Promise.all([
			fetch(baseUrl).then( resp => resp.json()),
			fetch(baseUrl+'/repos').then( resp => resp.json())
		])
		console.log(user);
		console.log(repos);
	} catch(err) {
		console.log(err.message);
	}
}

showUserAndRepos('wesleyallan').finally('Execução encerrada!');
```

## Problema Teste
Mesmo problema utilizando todos os métodos de resolução.

```js
function questionAsyncAwait(question) {
  return new Promise((resolve, reject) => {
    terminal.question(`${question}\n`, msg => {
      !!msg ? resolve(msg) : reject(new Error('O campo não pode estar vazio!'))
    })
  })
};

async function main() {
  try {
    let name = await questionAsyncAwait('Seu nome?');
    let age = await questionAsyncAwait('Sua idade?');
    console.log(`Ola ${name}, Parabens pelos seus ${age} anos de idade!`);
  } catch(err) {
    console.log('Deu Ruim!', err.stack);
  } finally {
    terminal.close();
  }
};
  
main();
```