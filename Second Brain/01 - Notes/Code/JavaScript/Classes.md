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
# 🚀 Introdução
Para aplicarmos o [[Introdução a POO|paradigma de programação orientado a objetos]] necessitamos de classes que são basicamente os modelos para instanciar objetos, em JavaScript nada mais é do que um _Syntatic Sugar_ ou seja, uma maneira mais bonita para escrever, que provêm uma maneira mais simples e clara de criar objetos e lidar com herança, basicamente para ser considerado uma orientação a objetos pura, os objetos criados, não deviam herdar nada além do que nos especificarmos, porem em JavaScript toda objeto instanciado por uma classe ainda herda toda a [[01 - Notes/Code/JavaScript/Manipulando Dados#Prototype|prototype chain]].

# 🏗️ Criando
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

# 🔒 Métodos Privada
Podemos criar métodos privados que só serão acessados internamente pela classe, através do operador `#`

```js
class Person {
  constructor(nome, peso, altura) {
    this.nome = nome;
    this.peso = peso;
    this.altura = altura;
  };
  
  #calculaImc() {
    return (this.peso / this.altura ** 2).toFixed(2);
  };
  
  get imc() {
    return `O Imc de ${this.nome} é ${this.#calculaImc()}`;
  };
};
  
const wesley = new Person('Wesley', 120, 1.90);
  
console.log(wesley.imc);  
wesley.#calculaImc();  // Propriedade não acessivel, método privado
```

Foi criado uma método privada chamada `calculaImc` que retorna o calculo do imc com o tratamento de 2 casas decimais, em seguida criamos um [[Introdução ao JavaScript#Métodos Assessores|Método Assessor]] `get` com uma [[Introdução ao JavaScript#Propriedade Calculada|propriedade calculada]] `imc` que retorna uma _[[Introdução ao JavaScript#String|string]]_.

# 🆘 Métodos Helpers
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

# 🖐️ Propriedade estática
Tem o mesmo funcionamento do [[#🆘 Métodos Helpers|método helper]], porem para propriedade, da mesma forma não temos acesso com o `this` e nem no objeto instanciado.

```ts
class Person {
	static myName: string = 'wesley';
	
	info(): string {
		return `Meu nome é ${Person.myName}`;
	}
}
```

## Ambos estáticos
Quando ambos são estáticos temos acesso ao `this` entre eles.

```ts
class Person {
	static myName:string = 'Wesley';
	
	static info(): string {
		return `Meu nome é ${this.myName}`;
	}
}
```
# 🫴 Getter e Setter
Podemos utilizar o Getter para pegar um valor passando através de uma alteração, e com  o _Setter_ podemos atribuir valor para uma propriedade, podendo usar o mesmo para realizar alguma alteração ou validação no meio do percurso, no final das contas é uma função.

```ts
class Person {
	private _name: string;
	public age: number;
	
	constructor(name: string, age: number) {
		this.name = name;
		this.age = number;
	}
	
	get name() {
		return this._name.toUpperCase();
	}
	
	set name(value: string) {
		if (value.length < 3) throw new Error('Nome inferior a 4 caracteres');
		this._name = value.toLowerCase();
	}
}
```

Assim utilizando o `get` e o `set` podemos ler e escrever como uma propriedade e na realida estaremos passando por eles.

```ts
const wesley = new Person('Wesley', 24);
console.log(wesley.name); // WESLEY
wesley.name = 'Teste'    // Gravado: teste
wesley.name = 'Ts'       // ERRO!
```

# 🧮 Propriedade Calculada
Podemos criar propriedades calculadas que seu valor não esta armazenado em uma propriedade da classe e sim será gerado quando requisitado.

```typescript
class Person {
	public name: string;
	public lastname: string;
	public age: number;
	
	constructor(name: string, lastname: string, age: number) {
		this.name = name;
		this.lastname = lastname;
		this.age: age;
	};
	
	get fullName() {
		return `${name} ${lastname}`; 
	}
}
```

Assim podemos acessar como uma propriedade calculada como uma propriedade comum.

```ts
const wesley = new Person('Wesley', 'Silva', 24);
console.log(wesley.fullName);
```