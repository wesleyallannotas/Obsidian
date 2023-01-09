---
title: Manipulando Dados com JavaScript
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Como manipular dados para extrair o maximo de informações
---
# Prototype
*Prototype* em tradução livre para o português é protótipo, ou seja, em outras palavras aquilo que foi criado antes, podemos encontrar referencias que dizem que o JavaScript é um *prototype-based language* ou seja, uma linguagem baseada em protótipos, pois ele contem a **_Prototype chain_** a cadeia de protótipos, podemos observar por exemplo quando criamos um objeto e dentro dele contem um objeto com o nome `__proto__`  (Criado a partir de um objeto protótipo), onde é herdado todas as propriedades e métodos o que podemos chamar de protótipo ascendente .

Em JavaScript a ==maioria dos tipos de dados são encapsulados por um objeto==, com todos possuindo seu `__proto__` herdando sua *Prototype chain*, podendo existir um *prototype* dentro do outro. 

![[Excalidraw/Desenho_JS_Prototype|center]]

# Type Conversion Coersion
*Type Conversion* (*typecasting*) e *Type Coersion* tem como funcionalidade a realização da alteração de um tipo de dado, porem seu funcionamento ocorre de maneira diferente, resumidamente:
- _Type Conversoin (typecasting)_ - Explicitamente altera um tipo de dado para o outro
- _Type Coersion_ - O JavaScript implicitamente realiza a troca. Acontece algo parecido com booleano através do [[Falsy e Truthy|falsy e truthy]]

## Type Coersion
```js
console.log('9' + 5)  // Resultado: '95'
```
Realizamos a soma de um `String` com o valor `'9'` e um `Number` com valor `5`, onde **implicitamente** o JavaScript realizou a troca do tipo `Number` para `String` e realizou a concatenação de `Strings` resultando em um `String` com valor `95`

## Type Conversion (typecasting)
```js
console.log(Number('9') + 5)  // Resultado: 14
```
Realizamos a soma de um `String` com valor `'9'` que **explicitamente** recebeu um *typecasting* para o tipo `Number` com um tipo `Number` com valor `5`, resultando um `Number` com o valor `14`

### Exemplo de Funcionamento
A *typecasting* ocorre localmente não alterando realmente o tipo (*type*) original da variável ou constante.
```js
let x = '10'
console.log(typeof x)  //Resultado: String
Number(x)
console.log(typeof x)  //Resultado: String
console.log(typeof Number(x))  //Resultado: Number
console.log(typeof x)  //Resultado: String
```

>[!note] Quantidade de caracteres de um tipo `number`
>O tipo de dados `number` não possui em seu *Prototype chain* o método `length`, onde a técnica utilizada para obter a quantidade de caracteres de um tipo `number` é realizar o *typecasting* para `string` e utilizar o método `length`
>```js
>let x = 1020
>console.log(String(x).length)
>```

# Formatando Números
Utilizamos o método do tipo `Number` para manipular as casas decimais e realizamos o *typecasting* em `String` obtendo o acesso ao método `replace` onde podemos alterar caracteres (*chars*) da `String`
```js
let x = 103.22234234234
console.log(String(x.toFixed(2)).replace('.', ','))  // Resultado: 103,22
```

# Alterando Separador de uma `String`
Quebramos a `String` utilizando o `split` informando qual o separador utilizado, depois concatenamos as `Strings` informando um separador para utilização
```js
let frase = 'Eu amo programar';
let separado = frase.split(' ');
let fraseUpdate = separado.join('_');
console.log(frase);
console.log(separado);
console.log(fraseUpdate);
```

# Pesquisando *String*
Através do método `includes` podemos verificar se um *sub-string* existe dentro de uma *Stirng*, onde o método retorna um booleano informando se encontrou ou não
```js
let phrase = "Eu aMo programar"
console.log(phrase.includes("amo"))  // Resultado: False
console.log(phrase.includes("aMo"))  // Resultado: True
```

# String para Array
Podemos quebrar um `String` em uma `array` através do método `from` para o objeto `Array`, separando cada caractere da `string` para um espaço na `array`
```js
let word = 'Corra'
console.log(Array.from(word))  // Resultad0: ['C', 'o', 'r', 'r', 'a']
```

# Manipulando Array
Alguns exemplo de manipulação que conseguimos executar com `Arrays`
```js
let techs = ["html", "css", "js"]

// Adicionar no fim
techs.push("nodejs")

// Adicionar no começo
techs.unshift("sql")

// Remover fo fim
techs.pop()

// Remover do começo
techs.shift()

// Pegar somenta alguns elementos do array
console.log(techs.slice(1, 3))  // Posição inicial, QQuantidade

// Remover 1 ou mais items em qualquer posição do array
techs.splice(1, 1)  // Posição inicial, Quantidade que vai remover

// Encontrar a posição de um elemento do array
let index = techs.indexOf('js')  // Retorna o index do elento
```