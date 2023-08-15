---
title: Entendo herança em POO
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [poo]
description: Entenda o conceito de herança. 
---
# Conceito
Se baseia na ideia de herança da vida real, ou seja, filhos podem herdar do pai. Utilizando termos mais técnicos uma classe filha pode herdar métodos e propriedades da classe pai.

# Herança no JavaScript
Em JavaScript criamos a relação de herança utilizando o comando `extends` na declaração da classe, ou seja, tal classe estende tal classe, e no seu construtor utilizamos a função `super()` para puxar os métodos e atributos do pai.

>[!note] Sobre JavaScript
>Herança sempre esta ocorrendo no JavaScript, por se tratar de uma linguagem baseada em [[01 - Notes/Code/JavaScript/Manipulando Dados#Prototype|protótipos]], sempre estamos herdando, por exemplo quando criamos uma _String_, ela herda da cadeia de protótipos (_prototype chain_) que possui o método `trim()`  

```js
class Veiculo {
	rodas = 4;
	
	mover(direcao){};
	virar(direcao){};
}
class Moto extends Veiculo {
	constructor() {
		super() // Puxar atributos e métodos do pai
		this.rodas = 2;
	}
}
```