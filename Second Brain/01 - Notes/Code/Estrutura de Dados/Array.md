---
title: Conhecendo Estrutura de Dados Vertor
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [estruturaDados]
description: Funcionamento e logica da estrutura de dados Array ou Vetor
---
>[!attention] Atenção
>A linguagem utilizada para os exemplo é o **_JavaScript_**

Também conhecido como vetor ou arranjo, é uma estrutura de dados amplamente utilizada e implementada em quase todas as linguagens de programação, uma das estruturas mais simples, que consistem em armazenar itens em ordem de inserção, os indexando a partir do numero `0`

```js
['a', 10, 'd', true]
//0,  1,   2,    3
```

Em teoria a _array_ armazena os dados um ao lado do outro na memoria assim possuindo uma **acesso aos elementos rápido**, porem por exigir que um elemento esteja armazenado do lado do outro na memoria, caso a _array_ sofra uma **inserção, será lenta**, pois necessita realocar toda a _array_ na memoria, para que se acomodem um ao lado do outro, o mesmo para operações de delete, pois, será necessário realocar os elementos para preencher o buraco deixado pelo elemento deletado.
_arrays_ aceitam dados repetidos.

# Dados Aceitos
Em **_JavaScript_** _array_ possui uma natureza **heterogenia**, ou seja, aceita valores de diferentes tipos, podendo misturar os tipos de dados livremente.
Em muitas linguagens, _Arrays_, pelo menos de forma nativa, possui natureza **homogenia**, com seu tipo especificado na criação e só aceitando valores desse tipo pré-definido, porem normalmente possui bibliotecas que permitem a criação de espécies de _Arrays_ heterogenias.

# Tamanho
Em **JavaScript** _arrays_ possuem **tamanho dinâmico**, assim não sendo necessário especificar o tamanho na declaração, já em muitas outras linguagens é **necessário especificar o tamanho** antes, pois, será alocado o tamanho na memoria, para alocar os dados um ao lado do outro.