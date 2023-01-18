---
title: Generics
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [typescript]
description: Como utilizar Generics.
---
# Introdução
_Generics_ vem para adicionar flexibilidade ao nosso código, assim como o [[Tipagem#Operador Union|Operador Union]], porem com o operador _union_ sempre estamos flexíveis para os valores especificado através dele, já no _generics_, deixamos nosso código flexível para qualquer tipo de dado, porem o tipo escolhido, ==será especificado na declaração e não poderá mudar.==

# Utilizando Generics
Para utilizarmos o _generics_ basta adicionar o sinais de maior e menor e uma espécie de identificador entre os sinais, que podemos escolher o que desejarmos, existe um [[#Convenção]] que é interessante seguir, mas a linguagem não obriga a nada.

```typescript
function useState<T>() {
	let state: T;
	
	function get()  {
		return stet
	}
	
	function set(newValue: T) {
		state = newValue;
	}
	
	return { get, set }
}
let newState2 = useState<string>();
newState.set('Ola!');
console.log(newState.get());
newState.set(123);  // ERRO!
```

No exemplo acima, como especificamos na declaração com _generics_ que o tipo é _string_, só será aceito _string_

## Convenção
São convenções, ou seja, praticas adotadas pela comunidade para fácil entendimento entre os programadores.
- `S` - State
- `T` - Type
- `K` - Key
- `V` - Value
- `E` - Element

# Estendendo o Generics
Na realidade utilizando essas sintaxe estamos restringindo nosso _generics_ aos tipos especificados, assim caso informe outro tipo além dos especificados, informara erro.

```typescript
function useState<T extends string | number>() {
	let state: T;
	
	function get()  {
		return stet
	}
	
	function set(newValue: T) {
		state = newValue;
	}
	
	return { get, set }
}
let newState = useState<string>();
let newState1 = useState<number>();
let newState2 = useState<boolean>(); // Erro!
```

>[!attention] Omitir Generics
>Caso omitirmos o tipo de dado no generics, terá o mesmo efeito que utilizar [[Tipagem#Operador Union|Operador Union]] assim se tornando flexível para os dois tipos a todo momento.

# Tipo Padrão no Generics
Quando não especificamos o tipo de uma função utilizando _Generics_, ele fica como `unknow` para _generics_ comuns, e para _generics_ com _extends_ terá o mesmo efeito que utilizar [[Tipagem#Operador Union|Operador Union]] assim se tornando flexível para os dois tipos a todo momento. para contornamos esse problema, podemos especificar um tipo padrão, assim, caso não seja informado um tipo, por padrão assumira aquele.

>[!attention] Restrições aos estendidos
>Quando utilizados o `extends` logicamente ficamos presos a definir como um padrão, os tipos passados pelo `extends`.

```typescript
// Extends sem Tipo padrão
function useState<T extends string | number>() {
	let state: T;
	
	function get()  {
		return state
	}
	
	function set(newValue: T) {
		state = newValue;
	}
	
	return { get, set }
}

// Sem extends sem tipo padrão
function useState2<T>() {
	let state: T;
	
	function get()  {
		return state
	}
	
	function set(newValue: T) {
		state = newValue;
	}
	
	return { get, set }
} 

// Extends com tipo padrão
function useState3<T extends number | string = number>() {
	let state: T;
	
	function get()  {
		return state
	}
	
	function set(newValue: T) {
		state = newValue;
	}
	
	return { get, set }
}

// Sem extends com tipo padrão
function useState4<T = string>() {
	let state: T;
	
	function get()  {
		return state
	}
	
	function set(newValue: T) {
		state = newValue;
	}
	
	return { get, set }
} 

let newState = useState();    // Tipo: string | number
let newState2 = useState2();  // Tipo: unknow
let newState3 = useState3();  // Tipo: number
let newState4 = useState4();  // Tipo: string
```