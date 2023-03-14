---
title: Formulários com React
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Aprenda a desenvolver formulários solidos com react.
---
# 🚀 Introdução
Boa parte da interação com aplicações web é feita por meio de [[01 - Notes/Code/HTML/Formulário| formulários]], a primeira vista parecem ser de fácil construção e manipulação, principalmente com _React_, porem um formulário bem construído engloba diversas caracterizas e "reatividades".
Para melhor gestão dos mesmo é muito recomendado o uso da _lib React Hook Forms.

![[Desenho_ReactForm_Introdução|600]]

É de extrema importância se atentar aos estados dos _inputs_ e como manipula-lo dentro do nosso formulário e o estado do próprio formulário pensando e mesclando ideias para encontrar a melhor forma de exibir erros para o usuário.

# Controlled e Uncontrolled
Basicamente _inputs_ do tipo _controlled_ são os que a gente fica ouvindo o estado a todo momento é os _uncontrolled_ é quando os ouvimos apenas em determinados momentos, basicamente.
- _controlled_ - Todo tempo sendo controlado, ouvido.
- _uncontrolled_ - Sem controle, só ouvi em momentos específicos.

# Capturando Dados
Podemos capturar os dados do nosso formulário de diversas formas, sendo uma das mais simples utilizando a _Web API_ `FormData`, onde a partir da mesma é criada pares de chave e valor, podendo ser acessado e manipulado facilmente.

```js
form.onsubmit( e => {
	e.preventDefault();
	const data = new FormData(e.target);
	window.alert(data.get('name'));
});
```

No exemplo acima estamos pegando o dado de nome que esta no nosso formulário e exibindo no _alert_
Para ==renderizações condicionas essa não é uma boa alternativa==.