---
title: Web APIs
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Entenda web apis
---
# 🚀 Introdução

# 📺 IntersectionObserver
Através desta Web API podemos identificar quando um elemento esta visível, ou seja, dentro da _viewport_.

## Utilizando
Para utilizarmos basta o instancia-lo passando uma _[[Assíncronismo#Callback Function|callback]]_  que será executado quando tal elemento estiver visível.
E depois linkamos o observador com o objeto através do método `observe`.

```js
const observer = new IntersectionObserver( entries => console.log(entries) );
observer.observe(document.querySelector('.init-hidden'));
```

Para adicionarmos vários elementos de uma vez não basta utilizar o `qyerySelectorAll`, pois o método `oberve` espera apenas um elemento, assim sendo necessário percorrer um lista para atingir o resultado.

```js
const observer = new IntersectionObserver( entries => console.log(entries) );
Array.from(document.querySelectorAll('.init-hidden')).forEach( e => oberver.observe(e));
```

Podemos perceber que ele executa a _callback_ quando o primeiro _pixel_ do elemento aparece, podemos mudar esse comportamento através de um objeto de configuração que pode ser passado como segundo parâmetro da [[Expressões e Operadores#Operador *new*|instanciação]].
Assim definindo um valor para `threshold`.
- `1 === 100%` - Quando informamos `1` ele executara a _callback_ quando 100% do elemento estiver dentro da viewport..

Podemos passa mais de um dentro de uma [[Introdução ao JavaScript#Array|array]] `threshold: [0, 0.5, 1]` assim executando toda as vezes que chegar ao ponto passado.

```js
const observer = new IntersectionObserver( entries => console.log(entries), {
	threshold: 1;
} );
```

Podemos dentro da _callback_ verificar o quanto esta visível utilizando a mesma logica de `1 === 100%` através de `entries[0].intersectionRatio`, muito utilizado para `if`

## Carregando os já ultrapados
É muito comum a partir de links carregarmos nossa página em determinado ponto da Web page, assim sendo necessário já estar carregado os elementos acima, podemos obter esse comportamento através de um interação, identificando os já passados.

```js
const observer = new IntersectionObserver( entries => {
	entries.forEach( e => {
		if (entry.intersectionRatio >= 0.5) {
			entry.target.classList.add('init-hidden-off');
		}
		})
}, {
	threshold: [0, 0.5, 1],
} );
```