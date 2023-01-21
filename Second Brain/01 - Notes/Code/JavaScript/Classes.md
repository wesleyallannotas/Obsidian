---
title: Classes
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Dominando Classes no JavaScript
---
# Introdução
Para aplicarmos o [[Introdução a POO|paradigma de programação orientado a objetos]] necessitamos de classes que são basicamente os modelos para instanciar objetos, em JavaScript nada mais é do que um _Syntatic Sugar_ ou seja, uma maneira mais bonita para escrever, que provêm uma maneira mais simples e clara de criar objetos e lidar com herança, basicamente para ser considerado uma orientação a objetos pura, os objetos criados, não deviam herdar nada além do que nos especificarmos, porem em JavaScript toda objeto instanciado por uma classe ainda herda toda a [[Manipulando Dados#Prototype|prototype chain]].

# Criando
Podemos criar uma classe através do operador `class` e em seguida informando o nome da classe, onde em seu corpo é criado, normalmente iniciamos pelo _constructor_ que é executado quando instanciamos uma classe, através dele podemos definir os dados necessários para construir nossa classe.

>[!tip] Boa Pratica
>Por convenção e entendido como uma boa pratica a nomeação de classes se iniciando com letras maiúsculas.

```js
class Piloto {
	 constructor(nome, dataNascimento, tempoDeVoo, temPermissaoParaVoar) {
		this.nome = nome;
		this.dataNascimento = dataNascimento;
		this.tempoDeVoo = tempoDeVoo;
		this.temPermissaoParaVoar = temPermissaoParaVoar;
	}
	
	dormir() {
		console.log(`${this.nome} esta dormindo`);
	}
}
  
const wesley = new Piloto('Wesley', new Date(1998, 5, 29), 50, true);
wesley.dormir();
```

Utilizamos o `this` para referenciar o objeto que esta sendo instanciado, ou seja, no caso acima, quando utilizado o [[Expressões e Operadores#Operador *new*|Operador New]] e instanciamos nossa classe, é chamado o _constructor_ que identifica o `this` como a constante `wesley`, assim o _constructor_ cria as propriedades dentro da constante `welsey`.

>[!attention] Atenção
>No contexto de classes não utilizamos `function` para declarar os métodos.

# Funções Helpers
Através do operador `static` podemos criar métodos que serão uteis externo a classes, ou seja, estarão disponíveis sem a necessidade de instanciar em alguma variável importante se atentar que quando utilizamos o `static`, não possuímos acesso  ao `this`.

```js
class Piloto {
	 constructor(nome, dataNascimento, tempoDeVoo, temPermissaoParaVoar) {
		this.nome = nome;
		this.dataNascimento = dataNascimento;
		this.tempoDeVoo = tempoDeVoo;
		this.temPermissaoParaVoar = temPermissaoParaVoar;
	}
	
	dormir() {
		console.log(`${this.nome} esta dormindo`);
	}
	
	static saudacao() {
		console.log('Bom dia a todos!');
	}
}

Piloto.saudacao();
```

