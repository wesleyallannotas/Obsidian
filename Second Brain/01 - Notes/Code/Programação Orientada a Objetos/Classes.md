---
title: Entendo Classes
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [poo]
description: Entenda o conceito de classes 
---
# Conceito
As classes na orientação a objeto, funcionam como um **molde** para criação de objetos. Objetos são criados a partir de classes, com muitos podendo ser criado da mesma classe, cada objeto criado a partir da classe é uma instancia da mesma. Normalmente a convenção para nomeação de classes é primeira letra de cada palavra maiúscula `class ContaCorrente()`

# Classe no JavaScript
JavaScript possui uma diferenças em seus conceitos para a teoria no geral, por se tratando de uma linguagem multiparadigma.
Em JavaScript, classe é uma **_Syntactical Sugar_**, ou seja, é uma maneira "Bonita" de se escrever em [[01 - Notes/Code/JavaScript/Manipulando Dados#Prototype|Prototypes]]. Podemos classificar assim, pois, em JavaScript, uma classe instanciada herdara toda uma cadeira de protótipos (*Prototype Chain*) de um objeto, já uma classe criada em uma linguagem totalmente orientada a objetos como Java, seria pura, com nenhum método ou propriedade além das criadas na classe, a não ser que uso herança.