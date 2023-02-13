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
Basicamente o quanto o motor do JavaScript, realiza uma conversão de tipo **implicitamente**, baseado em sua interpretação.
```js
console.log('9' + 5)  // Resultado: '95'
```
Realizamos a soma de um `String` com o valor `'9'` e um `Number` com valor `5`, onde **implicitamente** o JavaScript realizou a troca do tipo `Number` para `String` e realizou a concatenação de `Strings` resultando em um `String` com valor `95`

## Type Conversion (typecasting)
Basicamente o quanto realizamos uma conversão **explicitamente**, vale lembrar que a conversão vem como retorno, assim quando não reatribuir será mudado apenas naquela estancia.
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

### Formatando Números
Utilizamos o método do tipo `Number` para manipular as casas decimais e realizamos o *typecasting* em `String` obtendo o acesso ao método `replace` onde podemos alterar caracteres (*chars*) da `String`
```js
let x = 103.22234234234
console.log(String(x.toFixed(2)).replace('.', ','))  // Resultado: 103,22
```
Porem não a necessidade do uso do TypeCasting para _string_, pois, `toFixed()` retorna uma _string_

# Testando Tipos
Podemos testar um dado a fim de receber um [[Introdução ao JavaScript#Boolean|boolean]] o identificando, se sé encontra ou não.
- `isFinite()` - Testa se o dado é **não** é um valor `infity`
- `isNaN()` - Testa se o dado é um valor `NaN` (_Not A Number_)
- `Array.isArray()` - Testa se o dado é uma _array_

```js
let a = '1';
let b = '1a';
let c = 4 / []; // Infinity
let array = [];
  
console.log(isFinite(a));  // true
console.log(isFinite(c));  // false
  
console.log(isNaN(Number(a)));  // false
console.log(isNaN(Number(b)));  // true
console.log(Array.isArray(array)); // true
```

# Number
Agora que conhecemos o que é uma [[Introdução ao JavaScript#Number|Number]], podemos realizar operações com ela afim de extrair e manipular dados, utilizando funcionalidades provinda de [[#Prototype]] é as especificas do tipo de dado _Array_.

## Formatando Casas Decimais
Pode se mostrar necessário a formatação de tipos _number_ para determinado número de casas decimais, tendo o uso amplo para o mesmo o método `toFixed()`, onde informamos como parâmetro um _number_ contendo  o numero de casas decimais desejado, assim retornando uma _string_ com o resultado.
```js
let value = 214.5446

console.log(`Valor total de ${value.toFixed(2)}`)
```
Outra forma amplamente utilizada é através de uma biblioteca `Int1.NumberFormat` é uma biblioteca do JavaScript que permite formatar números com base nas preferências regionais do usuário. Isso significa que você pode usá-lo para exibir números com os formatos apropriados para a localidade do usuário, como separadores de milhares, casas decimais e símbolos de moeda.
```js
const formatter = new Intl.NumberFormat('default', {
  style: 'currency',
  currency: 'USD',
  minimumFractionDigits: 2,
});

const formattedNumber = formatter.format(123456.789);
console.log(formattedNumber);
// Output: "$123,456.79" (assuming US locale)
```
No exemplo acima, passamos a string `'default'` como primeiro argumento para o construtor `Intl.NumberFormat`, indicando que queremos usar as preferências regionais do usuário, podemos por exemplo especificar um local diretamente como `fr-FR` especificando a França como localidade. Em seguida, passamos um objeto de opções que especifica que queremos usar o estilo `currency`, que a moeda é o dólar americano (`USD`) e que queremos duas casas decimais.
Ao chamar o método `format()` passando o número que desejamos formatar, o `Intl.NumberFormat` retornará uma string formatada de acordo com as preferências regionais do usuário. No exemplo acima, se o usuário estiver usando uma localidade dos Estados Unidos, o resultado seria "$123,456.79".

# String
Agora que conhecemos o que é uma [[Introdução ao JavaScript#String|String]], podemos realizar operações com ela afim de extrair e manipular dados, utilizando funcionalidades provinda de [[#Prototype]] é as especificas do tipo de dado _String_.

>[!tip]- Alterando Separador de uma `String`
Quebramos a `String` utilizando o `split` informando qual o separador utilizado, depois concatenamos as `Strings` informando um separador para utilização
>```js
>let frase = 'Eu amo programar';
>let separado = frase.split(' ');
>let fraseUpdate = separado.join('_');
>console.log(frase);
>console.log(separado);
>console.log(fraseUpdate);
>```

## Pesquisando *String*
Através do método `includes` podemos verificar se um *sub-string* existe dentro de uma *Stirng*, onde o método retorna um booleano informando se encontrou ou não
```js
let phrase = "Eu aMo programar"
console.log(phrase.includes("amo"))  // Resultado: False
console.log(phrase.includes("aMo"))  // Resultado: True
```

## String para Array
Podemos quebrar um `String` em uma `array` através do método `from` para o objeto `Array`, separando cada caractere da `string` para um espaço na `array`
```js
let word = 'Corra'
console.log(Array.from(word))  // Resultad0: ['C', 'o', 'r', 'r', 'a']
```
Também podemos transformar uma _string_ em um _array_ informando um separador especifico.
```js
let frase = 'Eu amo programar';
console.log(frase.split(' '));  // Resultado: ["Eu", "amo", "programar"]
```

# Array
Agora que conhecemos o que é uma [[Introdução ao JavaScript#Array|Array]], podemos realizar operações com ela afim de extrair e manipular dados, utilizando funcionalidades provinda de [[#Prototype]] é as especificas do tipo de dado _Array_.

## Adicionando no Fim
Podemos adicionar um item ao fim da nossa _array_ através do método `push()`, ou podemos utilizar uma espécie de gambiarra acessando o ultimo item que não existe e adicionar valor, porem não é uma boa pratica.
```js
let list = ["html", "css", "js"];

list.push('react');
list[list.length] = 'nodejs';
```
Utilizando o `length` que começa contar nosso _array_ através do 1, conseguimos naturalmente acessar o ultimo item mais um, ou seja, que não existe na nossa _array_, e ai atribuímos valor.

## Adicionando no Começo
Podemos adicionar um item no inicio da nossa _array_ através do método `unshift()`, assim deslocando todos os valores um a frente no _index_ e adicionando o nosso valor no inicio, ou seja, na posição 0.
```js
let list = ["html", "css", "js"];

list.unshift('logica');
```

## Removendo o Ultimo
Podemos remover o ultimo item da nossa lista utilizando o método `pop()`, algo que pode ser ultimo é que o método devolve como valor o item que eles esta removendo, assim sendo útil para capturar esse valor para o que for necessário.
```js
let list = ["html", "css", "js"];

console.log(list.pop());
```

## Removendo o Primeiro
Podemos remover o primeiro item da nossa lista utilizando o método `shift()`, algo que pode ser ultimo é que o método devolve como valor o item que eles esta removendo, assim sendo útil para capturar esse valor para o que for necessário.
```js
let list = ["html", "css", "js"];

console.log(list.shift());
```

## Capturando Intervalo Valores
Podemos capturar um intervalo de valores através do método `slice`, onde como parâmetros informamos a posição inicial dentro da _array_ e a posição do item final mais 1.
```js
let list = ["logica", "html", "css", "js", "react", 'nodejs'];

console.log(list.slice(1, 4));  // ["html", "css", "js"]
```

## Removendo Intervalo de Valores
Podemos remover um intervalo de valores através do método `splice`, onde como parâmetros informamos a posição inicial dentro do _array_ e a quantidade que diferentes da [[#Capturando Intervalo Valores]], informamos a quantidade.
```js
let list = ["logica", "html", "css", "js", "react", 'nodejs'];

list.splice(1, 3);
console.log(list); // ["logica", "react", "nodejs"]
```

## Pesquisando Posição
Podemos pesquisar e capturar a posição de determinado valor dentro de uma _array_ através do método `indexOf()`, onde como parâmetros informamos o valora ser pesquisado.
```js
let list = ["logica", "html", "css", "js", "react", 'nodejs'];

console.log(list.indexOf('js'));  // 3
```
>[!attention] Atenção
>Caso não for encontrado o valor informado, o método retornará o valor `-1`, onde como vimos, em situações que necessita de _boolean_ ou que realizamos a conversão forçada o `-1` passando pelo [[Falsy e Truthy]] retornara `true`

## Ordenando
Podemos ordenar a nossa _array_ através do método `sort()`.
```js
let list = [3, 5, 7, 8, 1];
let list2 = ['b', 'z', 'q', 'y', 'a'];

list.sort();
list2.sort();
```

## Concatenando Arrays
Podemos utilizar o método `concat()` para capturar a junção da nossa _array_ com outra.
```js
let list = [3, 5, 7, 8, 1];
let list2 = ['b', 'z', 'q', 'y', 'a'];

let newList = list.concat(list2);
```
Podemos também utilizar o [[Expressões e Operadores#Operador Spread|operador spread]] porem temos que atentar a suas características para usar em momentos específicos.
```js
let list = [3, 5, 7, 8, 1];
let list2 = ['b', 'z', 'q', 'y', 'a'];

let newList = [...list, ...list2];
```

## Array para String
Podemos capturar uma transformação da nossa _array_ em uma _string_, através do método `join()` onde como parâmetros definimos um separador.
```js
let list = ["logica", "html", "css", "js", "react", 'nodejs'];

console.log(list.join(` -> `));
```

## map
Através do método `map()` que é um método de [[Introdução ao JavaScript#Array|Arrays]] obtido através da [[#Prototype|prototype chain]], onde conseguimos iterar a _array_ executando uma função callback para cada elemento da _array_, (referencia de função ou uma função anônima), e devolve uma nova _array_ com os resultados. ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/map))
Como parâmetro da nossa [[Assíncronismo#Callback Function|Callback]]  podemos capturar, **valor atual**, **índice**, **array de origem**. 
Como segundo parâmetro podemos passar um _thisArg_ (Valor a ser utilizado como o _`this`_ no momento da execução da função `callback`.
>[!attention] Atenção
>Método `map()` não manipula a _array_ base, porem a _callback_ consegui
```js
array.map((value, index, arrayOriginal) => `${index}: ${value} da array ${arrayOriginal}`)
```

```js
let numbers = [1, 4, 9];
let roots = numbers.map(Math.sqrt); // Referencia de Função 
// Resultado: 1, 2, 3

let double = numbers.map(n => n * 2);  // Arrow Function (Função Anonima)
// Resultado: 2, 8, 18
```

## forEach
Através do método `forEach()` que é um método de [[Introdução ao JavaScript#Array|Arrays]] obtido através do [[#Prototype|prototype chain]], onde conseguimos iterar a _array_ executando um função [[Assíncronismo#Callback Function|Callback]] para cada elemento da _array_, (referencia de função ou uma função anônima),  ==não devolve nada, não altera a _array_ original, simplesmente realizamos operações com os valores==. 
Como parâmetro da nossa _Callback_  podemos capturar, **valor atual**, **índice**, **array de origem**. 
Como segundo parâmetro podemos passar um _thisArg_ (Valor a ser utilizado como o _`this`_ no momento da execução da função `callback`.
```js
let numbers = [1, 4, 9];
numbers.forEach(item => console.log(item));
```

## reduce
Através do método `reduce()` que é um método de [[Introdução ao JavaScript#Array|Arrays]] obtido através da [[#Prototype|prototype chain]], onde conseguimos iterar a _array_ executando uma função callback para cada elemento da _array_, (referencia de função ou uma função anônima), resultado em um único valor. ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/map))
Como parâmetros da nossa _callback_ podemos capturar **acumulador**, **valor atual**, **índice**, **array de origem**
```js
array.map((acumulado, value, index, arrayOriginal) => {})
```

```js
const array = [5, 1, 3, 5, 6];
  
const soma = array.reduce( (total, item, indice, array) => {
  console.log(`${indice} na array ${array}`);
  return total += item
});

console.log(`Soma da array ${array} é igual a ${soma}`);
```

## filter
Através do método `filte()` que é um método de [[Introdução ao JavaScript#Array|Arrays]] obtido através da [[#Prototype|prototype chain]], onde conseguimos iterar a _array_ executando uma função _[[Assíncronismo#Callback Function|Callback]]_ para cada elemento da _array_, (referencia de função ou uma função anônima), resultado em uma _array_ contendo os elementos que passaram na verificação, ou seja, quando foi iterado o resultado de sua _callback_ foi `true`. ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/map))
Como parâmetro da nossa _callback_ podemos capturar **valor atual**, **índice**, **array de origim**.
Como segundo parâmetro podemos passar um _thisArg_ (Valor a ser utilizado como o _`this`_ no momento da execução da função `callback`.
```js
array.map((valueAtual, index, arrayOriginal) => {})
```

```js
const array = [5, 1, 3, 5, 6];
  
const filtrada = array.filter( (item, indice, array) => {
  console.log(`${indice} na array ${array}`);
  return item % 2 === 0
});
  
console.log(`Original ${array} resultado ${filtrada}`);
```

# Object
Agora que conhecemos o que é uma [[Introdução ao JavaScript#Object|Object]], podemos realizar operações com ela afim de extrair e manipular dados, utilizando funcionalidades provinda de [[#Prototype]] é as especificas do tipo de dado _Object_.

## Adicionando Elementos
Podemos adicionar um elemento ao nosso objeto, simplesmente passando um nome para chave e atribuindo um valor a ela.
```js
const person = {
	name: 'Wesley'
}

person["age"] = 24;
```
Assim sendo adicionando ao nosso objeto a propriedade `age` com o valor `24`.

## Capturando as Chaves
Podemos capturar as chaves do nosso objeto dentro de uma _array_ através do objeto global `Object` com seu método `keys`, onde como parâmetro/argumento especificamos qual o objeto.
```js
const person = {
	name: 'Wesley',
	age: 24
}

console.log(Object.keys(person));  // ['name', 'age']
```

## Capturando os Valores
Podemos capturar os valores do nosso objeto dentro de uma _array_ através do objeto global `Object` com seu método `values`, onde como parâmetro/argumento especificamos qual o objeto.
```js
const person = {
	name: 'Wesley',
	age: 24
}

console.log(Object.values(person));  // ['name', 'age']
```

## Concatenando Object
Podemos capturar uma concatenação de objetos através do objeto global `Object` com seu método `assign`, onde como parâmetro/argumento especificamos quais os objetos.
```js
const person = {
	name: 'Wesley',
	age: 24
}

const car = {
	model: 'Saveiro',
	ano: 2007
}

const newObject = Object.assign(person, car);
```
Podemos passar como terceiro parâmetro um propriedade que queremos criar.
```js
Object.assign({}, objetoExmeplo, {id: Math.random() / 0.5})
```
Concatenando um objeto vazio com um objeto já existente e criando uma propriedade.
Podemos também utilizar o [[Expressões e Operadores#Operador Spread|operador spread]] porem temos que atentar a suas características para usar em momentos específicos.
```js
const person = {
	name: 'Wesley',
	age: 24
}

const car = {
	model: 'Saveiro',
	ano: 2007
}

const alterPerson = {
	...person,
	age: 28
}

const newObject = {...person, ...car};
const newObject = { ...person, ...car }; // Mesmo resultado, so para ler melhor
```

## Removendo Elemento
Podemos remover um elemento dentro do nosso objeto através do operador `delete`.
```js
const person = {
	name: 'Wesley',
	age: 24
}

delete person.name;
delete person["name"];
```