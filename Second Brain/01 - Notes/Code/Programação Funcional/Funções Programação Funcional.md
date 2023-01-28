---
title: Funções na Programação Funcional
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [pf]
description: Entenda as caracteristicas das funções na programação funcional. 
---
# Introdução
Intender as diferenças e as caracteres das diferenças funções na programação funcional
- Função Independentes  (Qual a diferença da Pura?)
- Funções Puras  (Qual a diferença da independente?)
- First-class Functions
- Higher-order Functions
- Composição de Funções


# Funções Independentes
- Deverá ter ao menos 1 **argumento**, não deverá depender de nenhum dado externo
- Deverá **retornar** algo, e sempre o mesmo valor para os mesmos argumentos
- Não pode ser afetado por fatores externos
	- Dados imutáveis
	- Não guardar estados
- Não usa _loops_, caso haja necessidade deve usar recursividade.

```js
const random = (number, Math) => Math.floor(Math.random() * number);
```

Acima exercemos a ideia de **independência** onde sendo necessário a API do JavaScript `Math`, a pedimos como argumento invés de acessa-la de dentro da função.

```js
const factorial = x => {
	if (x === 0) {
		return 1;
	}
	return x * factorial(x - 1);
}
```

Para o calculo da fatorial é necessário um _loop_, pois, para calcular a fatorial de 5 é necessário realizar a operação `1 * 2 * 3 * 4 * 5`, onde para seguir a ideia de função independente usamos **recursão**, uma função chamando ela mesma.

# Funções Pura
- Não deverá depender de nenhum dado externo, apenas dos passados como argumento
- Sempre o mesmo valor para os mesmos argumentos
- Não pode ser afetado por fatores externos
	- Dados imutáveis
	- Não guardar estados
- Não terá nenhum efeito colateral no seu código

```js
const changePersonName = {person, name} => ({...person, name})
```

# First-Class Function
- Podem estar em qualquer lugar, inclusive como parâmetro de outras funções
- A função poderá ser entendi como uma variável

```js
const sayMyName = () => console.log('Wesley'); // First-Class Function
const runFunction = fn => fn();

runFunction(sayMyName)
runFunction(() => console.log('Discover'));

console.log(runFunction(Math.random))
```

Vale lembrar que por ser uma [[Funções#*Arrow Function*|Arrow Function]] de uma linha, já esta retornando o valor, mesmo com o comando `return` omitido.

# Higher-Order Function
- Funções que recebe funções como argumentos
- Funções que poderão retornar outras funções

```js
// Exemplo com .map() JS
const numbers = [2, 4, 8, 16];
const square = n => n * n;
const squaredNumber = numbers.map(square);
```

