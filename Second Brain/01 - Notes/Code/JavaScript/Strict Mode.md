---
title: Strict Mode
author: Wesley Silva
url:
book:
type: note
completed: false 
aliases:
tags: [javascript]
description: Entenda o strict mode
---
# Introdução
Basicamente é um modo que ativamos deixando nosso JavaScript em um "Modo Estrito", onde basicamente erros que antes eram silenciosos, ou até mesmo que executavam e podiam causar problemas futuros, agora exibem erro de execução, deixando nosso código mais seguro, bem escrito e otimizado.

# Ativando
Podemos ativar o modo estrito em todo nosso projeto ou apenas ==dentro de uma função== por exemplo, o mais recomendado e sempre usar em ==todo o escopo.==
Para ativar basta adicionar uma _[[Introdução ao JavaScript#String|String]]_ com o seguinte conteúdo.

```js
'use strict';
```

Pode ser adicionado no inicio do arquivo, adicionando-o no escopo global, ou dentro de uma função por exemplo.

```js
function soma(x, y) {
  'use strict';
  let total = x + y;
  return total;
}
```

# Vantagens
Existem diversas vantagens em utilizar o `use strict`, um dos erros mais comuns e que ele evita, é o de declarar funções sem o uso de um operador como `const`, `var` e `let`.
Emite erro para erros ignorados como a tentativa de deletar o _document_, entre outras.
Emite erro em tentar declarar valor para [[Introdução ao JavaScript#Propriedade Calculada|propriedades calculadas]].
Argumento repetidos como `function soma(x, x, y)`.
Entre diversos outros.