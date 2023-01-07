---
title: Controle de Fluxo
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Controle de fluxo com javascript
---
# Introdução
Toda aplicação possui um fluxo padrão segundo as instrução de cima para baixo da esquerda para direita, porem podemos controlar esse fluxo ou no inglês *control flow* para tomar caminhos diferentes, ou seja, desviar do fluxo padrão a partir de resultados booleanos recebidos, normalmente por condicionais.

# If...else
Se (*if*), senão (*else*), basicamente a partir de um booleano ele toma um caminho, sendo definido um para verdadeiro e um para falso.

>[!tip] Sobre `else`
>O uso do `else` é facultativo, podemos aninhar `if` utilizando `else if` sem a obrigatoriedade de existir um `else`

## If Simples
Executa um bloco de código quando recebe um booleano *true* normalmente recebido através de uma condicional.

```js
let nota = 8

if (nota > 7) {
	console.log("Aprovado!")
}

console.log("Fim")
```

## If Composto
Executa um bloco de código quando recebe um booleano *true* normalmente recebido através de uma condicional ou outro bloco quando recebi falso.

```js
let nota = 8

if (nota > 7) {
	console.log("Aprovado")
} else {
	console.log("Reprovado")
}

console.log("Fim")
```

## Aninhando Ifs
Podemos aninhar de condicionais com `else if` a fim de realizar diversas verificações em sequencia.

```js
let nota > 5

if (nota < 3) {
	console.log("Reprovado")
} else if (nota < 7) {
	console.log("Recuperação")
} else {
	console.log("Aprovado!")
}

console.log("Fim")
```

>[!attention] Atenção sobre declaração do bloco
>Com nosso `if` contem apenas uma linha de código, não é necessário a declaração do bloco `{ }`, porem não e recomendando, pois, pode trazer algum bug futuro, por exemplo quando adicionarmos algo e esquecermos de declarar o bloco.
>```js
>let x = 8;
>
>if (x > 7)
>	console.log("Aprovado!")
>```

# Switch
`Switch...Case` passaremos uma [[Expressões e Operadores#Expressão|expressão]] onde a partir do seu resultado terá casos (*case*) com execuções especificar para cada tipo de resultado, caso nenhuma satisfeita podemos utilizar o `default` que criara uma espécie de execução *default* caso não seja satisfeito nenhum *case* executara o `defautl`, como expressão podemos usar uma variável, uma operação, entre outros.

```js
switch (phrase.lenght) {
	case 1: 
		phrase.unshift("000")
		break
	case 2: 
		phrase.unshift("00")
		break
	case 3: 
		phrase.unshift("0")
		break
	default
		console.log("Valor ja formatado")
		break
}
```

>[!attention] Atenção
>- Uso do `break` é opcional, porem é uma boa pratica utiliza-lo e evita possíveis bugs, o `break` serve para quebrar a execução do bloco de código, quando não utilizado ele executa o bloco do `case`satisfeito e todos abaixo dele também, mesmo não satisfazendo o caso
>- Uso do `default` assim como o `else` para [[Controle de Fluxo#If...else|if..else]] é facultativo

# Throw e try...catch
Iniciando pela tradução livre, *throw* significa "Lançar", *Catch* significa "Pegar" e *try* significa "Tentar", basicamente temos a ideia que podemos **tentar** um bloco de código onde podemos **lançar** caso ocorra um erro que podemos **pegar**

>[!tip] Boa Pratica
>Podemos disparar qualquer coisa com o `throw` como uma mensagem
>```js
>function sayMyName(name = '') {
>	if (name === "") {
>		throw 'Nome é obrigatorio'
>	}
>}
>```
>Porem é uma boa pratica criar um novo objeto `Error` e passar como parâmetro para o [[Funções#*Function Constructor*|function constructor]]
>```js
>function sayMyName(name = '') {
>	if (name === "") {
>		throw new Error('Nome é obrigatorio')
>	}
>
>```

Senso assim o `catch` **através de um parâmetro** pega esse lançamento (*trhow*) onde podemos manipula-lo ou exibi-lo, importante se atentar que o ==`throw` quebra a execução do bloco de código==, podemos usar o `throw` sem um `try...catch` porem ele exibi o erro e também informa que ele não foi pego *Uncaught*

```js
function sayMyName(name = "") {
	if (name === "") {
		throw new Error('Nome é obrigatorio')
	}
	console.log(`Ola! ${name}`)
}

sayMyName()

console.log("Após a função com erro")
```

![[throw_sem_catch.png|]]

Utilizando corretamente e aproveitando da boa pratica o erro será capturado pelo `try...catch` podendo ser tratado ou utilizado como desejarmos.

```js
function sayMyName(name = "") {
	if (name === "") {
		throw new Error("Nome é obrigatorio")
	}
	console.log(`Ola! ${name}`)
}

try {
	sayMyName()
} catch(e) {
	console.error(e)
}

console.log("Após a função com erro")
```

![[throw_com_catch.png]]

Podemos observar que sem o `try...catch` é encerrado a aplicação, com o uso do mesmo ela continua.

# For
**Estrutura de repetição** `for` tem a função de controlar a iteração, normalmente sendo repetida ate um booleano com o valor `false` ser informado, no caso do for, será através da condição de parada, assim quebrando o fluxo de iteração, deve ser usadas com cuidado, pois, pode ocorrer por má programação a criação de *loops* infinitos. a sintaxe do `for` se baseia no comando `for` seguido da criação de uma variável de controle, uma condição de parada e pro ultimo a atualização da variável de controle.

```js
for (let i = 0; i <= 10; i++) {
	console.log(`Contagem: ${i}`)
}
```

Normalmente utilizamos `for` ==quando sabemos o fim==, assim podendo definir a parada do fluxo de repetição

# While
**Estrutura de repetição** `while` tem a função de controlar a iteração, normalmente sendo repetida ate um booleano com o valor `false` ser informado, assim quebrando o fluxo de iteração, deve ser usadas com cuidado, pois, pode ocorrer por má programação a criação de *loops* infinitos sendo ainda mais comuns em *loops* do tipo `while`. a sintaxe do `while` se baseia no comando `while` e entra parênteses, se espera um booleano que será verificado a cada iteração, sendo quebrado quando encontrar `false` como valor.
```js
let i = 0;

while (i <= 10) {
	console.log(`Contagem: ${i++}`)
	// i++
}
```

Normalmente utilizamos a estrutura repetição `while` ==quando não sabemos o fim==

>[!tip] Dica de incremento com exibição
>A linha de código do incremento esta **comentada**, pois, pode se observar que estou realizando o incremento desta variável que estamos utilizando como controle dentro do próprio `console.log` que informa seu valor, e utilizando o [[Expressões e Operadores#*Unary*|operador unário]] de incremento após o valor, para que **seja exibido e depois incrementado**

# For...of

**Estrutura de repetição** `for...of` tem a função de controlar a iteração, utilizando variáveis previamente criadas onde podemos **percorre-las**. a sintaxe do `for...of` se baseia no comando `for` e entra parênteses, se espera uma variável que será preenchida com cada pedaço capturado de outra variável, sendo quebrado quando percorre-la totalmente.

```js
let myName = 'Wesley'
let names = ['Andressa', 'Adria', 'Leonildo']

for (let char of myName) {
	console.log(char)
}

for (let name of names) {
	console.log(name)
}
```

Normalmente utilizamos a estrutura de repetição `for...of` para ==percorrer *Strings* e *Arrays*==
# For...in
**Estrutura de repetição** `for...in` tem a função de controlar a iteração, utilizando variáveis do tipo objeto previamente criadas onde podemos **percorre-las** pegando a propriedade/chave (*Property/key*). a sintaxe do `for...in` se baseia no comando `for` e entra parênteses, se espera uma variável que será preenchida com cada propriedade/chave (*property/key*) capturado de outra variável que contem o objeto, sendo quebrado quando percorre-la totalmente.

```js
let person = {
	name: "Wesley",
	age: 24,
	height: 1.90,
}

for (let property in person) {
	console.log(`${property} --> ${person[property]}`)
}
```

Utilizamos a estrutura de repetição `for...in` para ==percorrer *Object*==

>[!tip] Dica de como acessar valores de um objeto
>Como vimos sobre [[Introdução ao JavaScript#Object|objetos]] podemos acessar o valor de uma propriedade através da sintaxe `objeto.propriedade` ou também utilizando colchetes `objeto.["propriedade"]`

# Controles de Repetições
Dentro de um bloco de código de um *loop* podemos utilizar comandos para o controle, sendo eles:
- `break` - Quebra o repetição, independente da condição de parada tendo sido satisfeita ou não.
- `continue` - Pula para a próxima iteração, quebrando apenas a execução da repetição atual.

```js
for (let i = 10; i > 1; i--) {
	if (i === 7) {
		continue
	}
	if (i === 5) {
		break
	}
	console.log(`Contagem: ${i}`)
}
```