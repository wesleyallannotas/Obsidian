---
title: Tipagem
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [typescript]
description: Adicionando tipos ao nosso javascript
---
# Tipagem Explicita
Quando informamos o tipo da variável, possui os mesmo tipos dos JavaScript.

```typescript
let info: string = 'Vire a esquerda'
let info: string;
function sum(a: number, b:number) {}
```

De forma explicita informamos que `info` é do tipo [[Introdução ao JavaScript#String|String]], assim não aceitando valores diferentes e trazendo a informação para os desenvolvedores quando bate o olho e para a "IDE" informar o erro caso especificado outro tipo de valor.

# Tipos Primitivos
São os tipos de dados mais simples e sem uma estrutura, os mesmo do [[Introdução ao JavaScript#Primitivos (*Primitive*)|JavaScript]]

```typescript
let text: string;
let num: number;
let loading: boolean;
```

# Tipos Estruturais
São estrutura de dados que buscam armazenar mais que um dado apenas, os mesmo do [[Introdução ao JavaScript#Estuturais (*Structural*)|JavaScript]]

```typescript
let numeros: number[];       // Array/Vetor de Numbers
let numeros: Array<number>;  // Array/Vetor de Number
```

# Tipagem em Funções
Adicionamos tipagem em uma função, informando os tipos dos parâmetros/argumentos e o tipo de seu retorno, ficando da seguinte forma.

```typescript
function showMessaages(message: string): void{
	console.log(message);
}


function sum(x: number, y:number): number {
  return x + y;
}

function sum(x: number, y:number) { // Inferi como retorno do tipo number.
	return x + y;
}
```

O valor `void` é vazio, ou seja, informamos que essa função não tem retorno, assim a "IDE" já consegui nos informar erro caso utilizarmos o `return` dentro da função.

>[!attention] Caso omitido
>Caso não informarmos o tipo de retorno, [[Introdução ao TypeSript#Inferência de Tipo|TypeScript o inferi]] baseado no retorno.

# Tipo `any`
Quando declaramos uma variável sem informar seu tipo, ela recebe a tipagem com `any`, nada mais é do que uma variável sem tipo especifico, assim aceitando qualquer tipo de valor, ou seja, possuindo o funcionamento normal do JavaScript de tipagem dinâmica.

```typescript
let info;    // Tipo any
let age any; // Tipo any
```

# Operador Union
O operador _union_ nada mais é do que `|` na declaração do tipo, o utilizamos quando queremos informar que um variável aceita mais do que um tipo de dado.

```typescript
function printUserId(id: number | string): void {
	console.log(`O ID do usuário é: ${id}`);
}
```

Assim informamos que nosso parâmetro/argumento `id` aceita um valor do tipo `number` ou `string`, podemos encadear quantos operadores _union_ for necessário, por exemplo.

```typescript
function printUserId(id: number | string | boolean): void {
	console.log(`O ID do usuário é: ${id}`);
}
```

[TypeScript Playground - Types vs Interfaces (typescriptlang.org)](https://www.typescriptlang.org/pt/play?#code/PTAEFEA8EsGcBcCmBbUATA9nU9oAcNZQ8AnaAOwGN8BDbPGkm9RSgG0cdGYDMMTkzNIlABXZAFgAUCFAYARgCtE8DAC5QFJCR41KiIiNwFYAOmnTZ4NgdCwAxxlDyUxRq2iZDbpt1CDofmghQlBKGlhCSzAeUSpA8hpUNGZkA0FQPgEacylpeABPPBEAFXwMAAUI2EYnAF5QAG9pUG4a2A0AJgBuaQBfXrypLUQdPREASXJtXX0q2BqSJ2apVoiIrsG+iylKDHIENwXagEYNMoJ5xfqmto3QTtAB6T2D+CPrzo0pmfGr2tADUadw6Dyeg2ioAq-AAjqIRE4SkUDJQyHh3gBLsSoWBwJAZYQ4WgAc1cBngJFE8FETDYkKxJlgAFuAG6INj+PE0rhOWCIURiSI4JLyDHIXIvfaHBjHJYAZm+01Gs0Q-yWgI+pwhMjAAEFkPJQrBRAQSPAkn5EJAkAdHCw5FSmEQRmN9N5jIRcrIAPJED1EXQAL1ccCFNApNBZGKIKU0SpIfIA53bCf6ADSQxDkOE0aZOF0qoiM+GocTMBgcFlMAC0lAAFpHEBKpIViqAAML8USKZhA0DkDDUkgDjQU+FPUAAMlAF0q1Vqg1bIgASgoKBrgQOhyPMjQ2HyJ9Ofsq-vOltqC+MoZGaE4rTa0ERZ2rli0whg2EFMKPKYhBq0WQwGgNF0fc-36aRL30UAAHE9woBtQHvLNH1AY9XVVM9X1Wd9PzIb9dzA-9QEA4DCL5LYdhsd49kpHsNE7Oje1udZQU6NN+0HGkdzHERnikajQGJeDyAbDQ4LYBDmOBViug4vY8M8dRyMQDjSJAvcD34yEShQpw0GgVRNAWJxyAAZ6IEhWAwNJyBSZBQkAygACu-FERY41+N1uHzcgoxjIxyjMSFwFgYpqD3WykGIWFxyc1yrP0Fx-HZOt+FsWyalJA57VGJYvTAABlEQZQ8pwHPckRInkKy5CQkgljUjAXJiwk2RIORDAa0I4QRGdkVgVF8HgSEAgDZqaC8HxmCg2w9gcvwJKk5taO7ZjhMk0SaEGDapI1Vae21WQAFUCQifw6HSmNoB4UYs0Tc6swpQKTCQzyT28rFeshWaiAcJwaBcM1HqJV7-syVgGy8Aq0JMuxoGJcgbvCUBepI5rXIIQlkLs0Z3owgL2E4OyMEhMs7EQYk4ljNlA2bWbYPDbDWiWchWbIw0P0QXNKKGBm4KMlZWlojQEDIchiV5yFoQ6jBHScDhMFB0JyDtLHXD5Dq920SbQiyGhIVjUgzNIYIWCJphkwwZsl1AAAxaA2DS6KgTfEW7ApChJf6bVbYdp3BxEV2cJqiheq8DRyHEIGtiOsAABFEGKXGSfQI1+SIBRlFwQDDGOdAbru8gHtaqrRkhExDOgFlmDl-tKfDauclAAA5O9plzTAOIYXwrVNTrlaLUR5Ek8IosQekUoDjqIwOLJkAAQ+rT9DFQX7m1kTsFvENOiDSafbESmlIiLTgSLx1QptCcIT-tdzSZ1e1-RI5140LDjEpslCklCAwahwOsVlJpp1AIVc0lAADWGB2o8E-AAd0hPNJwO9DSoAIHme0PdcApDUDsWQdZ4DwDwB0EACA9BQJgfA0w81gC9QQAkWAwA5QAHZOhyhYXKAArMAJcg00TwGrL9asLJYDVl4cAThnQABsAAOTo8iAAMABiSRsj5GdAUdIIAA)
[Principais diferenças entre types e interfaces em TypeScript | by Vinícius Estevam | Medium](https://viniciusestevam.medium.com/principais-diferen%C3%A7as-entre-types-e-interfaces-em-typescript-a00c945e5357)
[Interfaces vs Types in TypeScript - Stack Overflow](https://stackoverflow.com/questions/37233735/interfaces-vs-types-in-typescript/52682220#52682220)
