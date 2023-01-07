---
title: Quick Sort
author: Wesley Silva
type: note
url:
book: Entendendo Algoritmos
completed: true
aliases: qsort
tags: [algoritmo]
description: Entender o algritmo quick sort que utiliza técnicas de recurão
---
# Introdução
Algoritmo de Ordenação que usa a técnica DC (Dividir para conquistar), **algoritmos DC são [[Recursão|recursivos]]**, ou seja, devemos encontrar o **caso base** e o **caso recursivo** 

>[!info]
A linguagem utilizada no exemplo sera **Python**

# Caso-Base
Normalmente é uma função recursiva que utilizam ***array*** ou qualquer outro tipo de lista, o caso base geralmente é uma array **vazia ou com apenas um elemento.**

# Caso-Recursivo
1. Caso possua dois elementos basta ordená-los com uma comparação simples.
2. Caso tenha três ou mais elementos, será necessário ==escolher um **pivô**== e a partir de **comparações com o pivô** será ==gerado **duas subarrays**== com os valores **menores** e os **maiores**, a vendo mais de 2 valores em alguma das subarray basta executar o mesmo procedimento.

# Algoritmo
```python
def qsort(lista):
	if len(lista) < 2:
		return lista
	else:
		pivo = l[0]
		menores = [i for i in lista[1:] if i > pivo]
		maiores = [i for i in lista[1:] if i <= pivo]
		return qsort(menores) + [pivo] + qsort(maiores)
```
```ad-attention
title: Atenção

Note que envolvemos o pivô em uma lista, para conseguir concatenar, sem retorar erro.
```

# Mapa Mental
![[MapaMental _QuickSort|640]]