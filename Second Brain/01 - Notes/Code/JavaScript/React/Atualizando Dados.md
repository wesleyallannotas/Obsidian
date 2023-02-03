---
title: Atualizando Dados
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Atualizando dados automaticamente.
---
# Introdução
Funcinalidade poderosa e muito utilizada no [[Introdução ao React|React]] é a possibilidade de manter todas as telas atualizadas, sendo sincronizadas a cada determinado tempo, o _React_ através de [[Hooks]] e o funcionamento do [[Hooks#Hook Flow|Hook Flow]] consegui atingir essa objetivo facilmente.

# Criando Sincronizador
Basicamente utilizaremos o [[Hooks|hook]] [[Hooks#useEffect|useEffect]], onde utilizando de forma inteligente o [[Hooks#Hook Flow|hook flow]] podemos ativar o sincronizador que será feito através de um [[Timers#Interval|setinterval]], onde será verificado uma condição para ativa-lo ou não dependendo do estado.

```tsx

const TIME_TO_UPDATE_MS = 1000

useEffect(() => {
	if (editMode) return;
	
	const intervalChanged = setInterval(() => {
		void fetchAndUpdateData();
	}, TIME_TO_UPDATE_MS);
	
	return () => {
		clearInterval(intervalChanged);
	};
}, [editMode]);
```
