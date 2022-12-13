---
title: Bubble Sort
author: Wesley Silva
type: note
urls:
book: 
completed: true
aliases: bubbleSort
tags: [ordenação, algoritmo]
description: Algoritmo de ordenação simples, que usa da comapração 
---
# Introdução
Algoritmo *Bubble Sort* é um algoritmo de Ordenação que tem seu funcionamento baseado na **comparação entre vizinhos** assim realizando ou não inversão de posições, onde o mesmo só para de ser executado quando **percorre toda a lista sem registrar nenhuma troca.**

```ad-info
A liguagem utilizada no exemplo sera **Python**
```

# Algoritmo
```python
def bubbleSort(lista):
	trocou = True
	while trocou:
		trocou = False
		i = 0
		while i < len(lista) - 1:
			if lista[i] > lista[i+1]:
				lista[i], lista[i+1] = lista[i+1], lista[i]
				trocou = True
			i += 1
```

```ad-attention
title: Atenção

Note que o ultimo valor da variavel `i` (Variável de controle) sera o tamonho da lista menos 2, pois, busca evitar erro de indexação estrapolando o tamanho da lista.
```
