---
title: Ferramentas para HTTP
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [web]
description: Ferramentas para manipular e receber dados via HTTP
---
# Introdução
HTTP é o protocolo que permite a comunicação cliente servidor, existem diversas ferramentas que são de extrema ajuda para testar e auxiliar na criação de nossas _Requests_ e _Responses_, temos que entender que toda comunicação base via navegador é HTTP, ou seja, quando acessamos um site, basicamente estamos enviando um _Method_ `GET`, requisitando (_request_) os dados para montar a página. É de extrema importância para todo desenvolvedor Web conhecer boas ferramentas que permitem monitorar as _Responses_ é manipular as _Request_.

# DevTools
Ferramenta padrão de todo navegador Web, possuindo algumas diferenças entre os diferentes navegadores, podemos "Gravar" as requisições e analisas individualmente através da aba _Network_, entre outras diversas ferramentas disponiveis.

# Curl
Programar de linha de comando onde podemos interagir com diversos protocolos diferentes, basta utilizar o nome do comando mais o endereço que traz a resposta _Responde_

```bash
curl https://google.com
```

-  _flag_ `-i` - Traz o _header response_.
- _flag_ `-v` - Traz todos os _Headers_, cheio de detalhes, com operador `>` para _Headers_ de saída e o contrario para entrada.