---
title: Introduçõa ao TypeScript
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [typescript]
description: Entenda os beneficios e por que usar TypeScript
---
# Introdução
TypeScirpt foi um _superset_ de tipagens criado pela Microsoft para o JavaScript, hoje pode ser chamado de linguagem de programação, pois, existem soluções como o Deno, que roda o código TypeScript nativamente, sem a necessidade de transpilar através do `Babel` por exemplo, porem a maioria ainda possui a necessidade de realizar a transpilação para um código JavaScript nativo. **(Ou seja, maioria das vezes TypeScript será uma dependência de desenvolvimento apenas)**
O TypeScript não te obriga adicionar tipagem em tudo, porem quando mais tipagem adicionarmos a nossa aplicação, maiores erros poderão ser evitado através na segurança que as tipagens trazem, além de ajudar muito na produtividade.

>[!tip] Ferramenta Interessante
>Dentro do site oficial do TypeScript existe uma ferramenta chama Playground, onde podemos escrever o código TypeScript, Testar códigos. E é informado em tempo real o código compilado para JavaScript.

# Vantagem da Tipagem
Além da própria "IDE" entender o código melhor, evitando erros bobos como acessar propriedades não existentes em objetos, um erro comum que pode acontecer quando os tipos não foram definidos corretamente, e somar _String_ com _Number_.

```js
function sum(a, b) {
	return a + b;
}
console.log(sum(1, '2')); // 12
console.log(4 / []) // Infinity
```

No primeiro caso ocorre o [[Manipulando Dados#Type Coersion|type coersion]] alterando o tipo de `1` que é um _[[Introdução ao JavaScript#Number|Number]]_ para _[[Introdução ao JavaScript#String|String]]_, e realizando a concatenação, exibindo no _console_ o valor `12`, esses entre outros diversos erros ocorrem por falta de tipagem, utilizando TypeScript seria informado os tipos de dados aceitos, assim evitando o erro.

```typescript
function sum(n1: number, n2: number): number {
  return n1 + n2;
}
console.log(sum('1', 2));  // IDE informa Erro, tipo number do parâmetro.
console.log(4 / []);       // IDE informa erro na operação.
```

# Transpilando
Existem diversas formas de transpilar um código em TypeScript, normalmente essa função já estará pré-programada por ferramentas que criam o ambiente de desenvolvimento como o _vite_, _Create React app_ entre outros, porem para teste podemos transpilar na mão rapidamente com o próprio comando do TypeScript.

```bash
tsc index.ts
```

Gerando um arquivo de mesmo nome com a extensão e código de JavaScript puro.
