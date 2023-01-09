---
title: Programação Funcional
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [pf]
description: introdução sobre programação funcional 
---
É um paradigma de desenvolvimento, esta diretamente envolvido com funções, onde abstrai um problema e isola ele **dentro de funções**, uma função **só ira modificar os dados conditos dentro dela**, as funções devem ser **pequenas e bem específicas** no que fazem.
Um dado (ou mais) entra em uma função e um novo dado  sai dessa função, não guarda estado  oque é chamado de `stateless`.
Alguns exemplo de linguagens funcionais:
- JavaScript (Multiparadigma)
- PHP (Multiparadigma)
- Elixir
- Haskell

# Imutabilidade
De grosso modo as variáveis não iram variar, se você precisar mudar uma variável, você não muda, você cria uma nova, ou seja, na realidade tudo são constantes.

```js
const cart = {
	quatity: 2,
	total: 200
}

// Não fazer 👎
cart.quantity = 3;

// Correto 👍
const newCart = {...cart, quantity: 3};
```

Utilizamos a [[Introdução ao JavaScript#Copiando Elementos|copia de elementos]] de um objeto para o outro, originando uma novo objeto e nele a quantidade (_quantity_) é diferente, exemplo de trecho de código encontrado no dia a dia trabalhando com _React_

```js
const [amount, setAmount] = useState(0);

// Não funciona 👎
amount = 2;

// Funciona 👍
setAmount(2);
```

Estamos criando uma constante `amount` e pegando uma função `setAmout`, tudo será retornado por `useState()`.

# Stateless
Não há memória (estado) mantido pelo programa, nenhum registro ou estado de todas as interações anteriores são salvos e cada interação é tratada com base nas informações disponíveis para a interação.
Como não conhece e nem é influenciado por dados externos que não são os passados como argumento/parâmetro, sua resposta não pode variar, ou seja, se sempre receber apenas o valor 2 como dado, sempre retornara o mesmo resultado, por que não sofre interferência externa.
Contrario de _Stateless_ é _Stateful_
- Não guarda estado
- A função só conhece dados entregues a ela
- A resposta não poderá variar

```js
let number = 2;

// Stateful Function
function square() {
	return number * number;
}

number = square();

// stateless function
const square = n => n * n;
```

No caso a _Stateful function_ usa o estado anterior da variável `number`.  Podemos perceber que causa ate uma certa confusão neste caso, já a _Stateless function_ não tem relação nenhuma com estados externos, ele recebe um valor e devolve outro, sempre sendo destruída no final da execução com cada vez que é chamada é recriada de forma pura.