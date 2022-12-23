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
>>function sayMyName(name = '') {
>	if (name === "") {
>		throw new Error('Nome é obrigatorio')
>	}
>
>```

# 2min e verificar se os arquivos estão corretor