---
title: Dicionario do Programador
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: 
description: Explicações direto ao ponto sobre o mundo da programação
---
# API
API é um sigla para _Application Programming Interface_ tem como função possibilitar conexão e a troca de informações entre softwares normalmente sendo feita através de requisições e respostas, existem quatro maneiras de funcionamentos de APIs, sendo elas, APIs SOAP, APIs RPC, APIs WebSocket e APIs REST.
O analogia mais comum para explicar o funcionamento de APIs, é o funcionamento do garçom, onde ele é uma API que conecta o cliente com a cozinha, enviando uma _request_ que é o pedido, e a cozinha prepara (processamento dos dados) devolve uma _response_ que é o alimento (informação) no prato (empacotado no `JSON`) pronto para o consumo, podemos perceber que a API realiza apenas a comunicação, não manipulando os dados em nenhum momento.

# JSON
JSON é uma sigla para _JavaScript Object Notaion_ é um formato de arquivos leve utilizado para troca de informações e dados, possui fácil leitura, apesar de se basear na sintaxe de objetos no JavaScript, ele é independente e pode ser consumido por qualquer linguagem de programação.

```json
{
	"name": "Wesley",
	"lastaName": "Silva",
	"age": 24,
	"books": {
		"programação": [
			"Entendo Algoritmos",
			"Estrutura de Dados e Algoritmos com JavaSript",
			"Código Limpo"
		],
		"Entretenimento": [
			"1984",
			"A Revolução dos Bichos"
		]
	}
}
```

# Renderização
Ato de obter um produto através de um processamento digital.

## React
No contexto de React nada mais é do que transformação do componente em um DOM node.