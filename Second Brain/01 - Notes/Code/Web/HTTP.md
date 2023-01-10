---
title: Protocolu HTTP
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [web]
description: Entenda o Protocolu HTTP 
---
# Introdução
HTTP vem de _HyperText Transfer Protocol_, ou seja, Protocolo de transferência de HyperText.

>[!note] Protocolo
>Conjunto conjunto de informações, decisões, normas e de regras definidas

Quando acessamos algo pela Web, ocorre a transferência de dados através deste protocolo, pois, é ele que permite essa troca de informações, requisições e respostas, onde é aberto uma chamada para cada recurso, sejam eles, HTML, CSS, JavaScript, Imagens, Vídeos, entre outros

![[Desenho_Web_HTTP|600center]]

# Request
_Request_ é o pedido que realizamos ao Servidor, é esse mensagem tem um estrutura que deve ser respeitada para uma boa comunicação com o Servidor.

## Methods
Através do _Methods_ especificamos qual ação desejamos executar com o pedido que estamos realizando.
- `GET` - Pegar um Recurso
- `POST` - Criar um Recurso

## Header
Campos informativos sobre a requisição (_Request_), possuem a estrutura de `Propriedade: Valor`, alguns exemplos
- `Content-Type: application/json`
- `User-Agent: Chrome`

## Body
Conteúdo da requisição (_Request_), por exemplo um `JSON` contendo os dados de um cadastro, ou seja, os dados que estamos enviando para o servidor, entre outros.

# Response
_Response_ é a resposta que o servidor envia para o _Request_ que enviamos, assim criando a comunicação.

## Status Code
Valor inteiro, normalmente de 3 dígitos, que informa a resposta do servidor sobre o estado da requisição (_Request_).
- `200` - Deu certo
- `301` - Redirecionamento, por exemplo acessa por uma URL ele te envia para outra
- `404` - Não foi encontrado
- `500` - Erro interno no servidor

## Header
Campos informativos sobre a resposta (_Response_), possuem a estrutura de `Propriedade: Valor`, alguns exemplos
- `Content-Type: application/json`
- `User-Agent: Chrome`

## Body
Conteúdo da resposta (_Response_), por exemplo o HTML da página, um JSON contendo as informações que enviamos para API pelo _Body_ do nosso _Request_, entre outros.