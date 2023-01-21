---
title: Date
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Manipulando datas com JavScript
---
# Introdução
Utilizamos a classe `Date` para manipular datas no javaScript, possuindo métodos para edição e controle de datas, pois, JavaScript, assim como outras linguagens de programação só entendem números, sendo necessário possui uma classe especifica que normalmente vem inclusão com a linguagem para realizar a manipulação de forma eficiente.

>[!note] Inicio da Data
>A contagem de datas se inicia em `01/01/1997` as `00:00:00`, podemos verificar esse comportamento instanciando uma data com valor 0
>```js
>let dataInicial = new Data(0);
>console.log(dataInicial) // Resultado: 1970-01-01T00:00.000Z
>```

```js
let date = new Date(2023, 24, 10);  
```

Para instanciar um objeto do tipo data utilizamos o [[Expressões e Operadores#Operador *new*|Operador New]] e em seguida `Date()`, caso não informado nada na construção, é utilizado a data atual, caso queira utilizar uma data especifica basta passar como parâmetro/argumento, sendo todos opcionais, em ordem são ano, mês, dia, hora, minuto, segundo, milissegundo.

>[!attention] Atenção com os Meses
>Meses tem sua contagem iniciada em 0, ou seja, caso seja necessário referenciar o mês de Novembro, o valor passado para o mês é `10` não `11` que é o numero dele no calendário.

# Transformando em String
Nossa data é um objeto, podemos captura-la transformada em uma [[Introdução ao JavaScript#String|String]] através dos seguintes métodos.
- `toString` - `Fri Nov 24 2023 00:00:00 GMT-0300 (Brasilia Standard Time)`
- `toLocaleDataString` - `11/24/2023`
- `toISOStirng` - `2023-11-24T03:00:00.000Z`

```js
let andressa = new Date(2023, 10, 24);  // 24/11/2023

console.log(andressa.toString())
console.log(andressa.toLocaleDateString())
console.log(andressa.toISOString())
```

O mais recomendado é o ISO, por ser um padrão e estar disponível em todas linguagens de programação.

# Alterando Dia
Podemos capturar e manipular o dia da nossa data através dos métodos `getDate()` e `setDate()` consecutivamente.

```js
const dia = hoje.getDate();
console.log(dia)
hoje.setDate(dia + 1);
console.log(hoje);
```

## Capturando Dia da Semana
Podemos capturar o dia da semana, sendo eles numerados de 0 - 6, iniciando a semana no domingo e terminando no sábado.

```js
let diaSemana = hoje.getDay();
console.log(diaSemana);
```

# Alterando Mês
Podemos capturar e manipular o mês da nossa data através dos métodos `getMount()` e `setMonth()` consecutivamente.

```js
const mes = hoje.getMonth();
console.log(mes);
hoje.setMonth(mes + 1, 24);
console.log(hoje);
```

Através do `setMonth()` podemos manipular o mês e o dia, sendo o dia opcional.

# Alterando Ano
Podemos capturar e manipular o ano da nossa data através dos métodos `getFullYear()` e `setFullYear()` consecutivamente.

```js
const ano = hoje.getFullYear();
console.log(ano);
hoje.setFullYear(ano + 1, 5, 29);
console.log(hoje);
```

Através do `setFullYear()` podemos manipular o ano, mês e dia, sendo o mês e dia opcional.

# Alterando Hora
Podemos capturar e manipular a hora da nossa data através dos métodos `getHours()` e `setHours()` consecutivamente.

```js
const horario = hoje.getHours();
console.log(horario);
hoje.setHours(horario + 1, 35, 25, 780);
console.log(hoje);
```

Através do `setHours()` podemos manipular o hora, minuto, segundo e milissegundos, sendo minuto, segundo e milissegundos opcional.

# Alterando Minutos
Podemos capturar e manipular os minutos da nossa data através dos métodos `getMinutes()` e `setMinutes()` consecutivamente.

```js
const minutos = hoje.getMinutes()
console.log(minutos);
hoje.setMinutes(minutos + 1, 26, 781);
console.log(hoje);
```

Através do `setMinutes()` podemos manipular o minuto, segundo e milissegundos, sendo segundo e milissegundos opcional.

# Alterando Segundos 
Podemos capturar e manipular os segundos da nossa data através dos métodos `getSeconds()` e `setSeconds()` consecutivamente.

```js
const segundos = hoje.getSeconds();
console.log(segundos);
hoje.setSeconds(segundos + 1, 600);
console.log(hoje);
```

Através do `setSeconds()` podemos manipular os segundo e milissegundos, sendo milissegundos opcional.

# Alterando Milissegundos 
Podemos capturar e manipular os milissegundos da nossa data através dos métodos `getMilliseconds()` e `setMilliseconds()` consecutivamente.

```js
const milisegundos = hoje.getMilliseconds();
console.log(milisegundos);
hoje.setMilliseconds(milisegundos + 1);
console.log(hoje);
```

Através do `setMilliseconds()` podemos manipular os milissegundos.

# Comparando Datas
Podemos comparar datas no JavaScript através dos [[Expressões e Operadores#Operadores de Comparação|Operadores de Comparação]], onde por baixo dos panos o JavaScript chama o método `valueOf` que converte a data em milissegundos a partir da data inicial que é `1970-01-01 00:00:00` até hoje, assim conseguindo realizar a comparação.

```js
const wesley = new Date(1998, 5, 29);
const andressa = new Date(1991, 10, 24);

console.log(wesley > andressa);

// Nada impedete fazer direto, pois a instancia retorna o objeto da mesma forma.
console.log(new Date(1998, 5, 29) > new Date(1991, 10, 24));
```

O resultado será `true`, pois a variável `wesley` contem um data mais nova, seu tempo em milissegundos desde `1970-1-1 00:00:00` é maior do que a da variável `andressa` que é mais antiga.