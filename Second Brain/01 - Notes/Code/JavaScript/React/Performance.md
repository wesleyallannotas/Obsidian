---
title: Performance
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Melhorando a performance do React 
---
# 🚀 Introdução
Basicamente uma maior performance se aplica em evitar Re-renders, antes de aplicar uma atualização no DOM ele realiza uma comparação chamada de _Shallow Compare_, onde basicamente  com ==tipos primitivos consegui comparar tranquilamente==, já com estruturas não, pois, mesmo que dois ==objetos== possuam estrutura e conteúdo igual, o resultado é falso, pois a ==referencia na memoria é diferente.==

```js
const obj = { title: "Test" };
const objCopy = { title: "Test" };

obj === objCopy // False
obj.title === objCopy.title // True
```

# 🛠️ React-Dev-Tools
É uma ferramenta que podemos instalar no nosso navegador que permiti analisar os sites que utilizam _React_, adicionando novas funcionalidades onde podemos ver os componentes carregados, alterar estados, testar performance habilitando um _highlight_ toda vez que o componentes é renderizado, gravadores de ações, afim de melhorar e entender melhor nosso código, auxiliando no desenvolvimento.