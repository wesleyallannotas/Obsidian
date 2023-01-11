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
HTTP é um acrônimo para _HyperText Transfer Protocol_, ou seja, Protocolo de transferência de HyperText.

>[!note] Protocolo
>Protocolo conjunto de informações, decisões, normas e de regras definidas

Quando acessamos algo pela Web, ocorre a transferência de dados através deste protocolo, pois, é ele que permite essa troca de informações através das **HTTP Messages**, requisições e respostas, onde é aberto uma chamada para cada recurso, sejam eles, HTML, CSS, JavaScript, Imagens, Vídeos, entre outros

![[Desenho_Web_HTTP|600center]]

# Request
_Request_ é o pedido que realizamos ao Servidor, é esse mensagem tem um estrutura que deve ser respeitada para uma boa comunicação com o Servidor.

![[Desenho_Web_Request|center]]

## Methods
Através do _Methods_ especificamos qual ação desejamos executar com o pedido que estamos realizando
Métodos seguros, que não alteram o estado do servidor, somente leitura, sendo eles `GET`, `HEAD` e `OPTIONS`
Métodos Idempotente, são métodos que sempre devolvem a mesma resposta, por exemplo um pedido para o google, sempre traz os mesmo dados, normalmente os **idempotente** são todos os seguros mais o `PUT` e o `DELTE`
- `GET` - Pegar um Recurso, idempotente, *cacheable*
- `HEAD` - Recebe somente o cabeçalho, idempotente, _cacheable_
	- `curl -I https://endereco.com`.
- `OPTIONS` - Informa disponibilidade da requisição, idempotente.
	- `curl -X OPTIONS http://localhost:3000/posts -i`.
- `POST` - Criar um Recurso, publicar cadastrar. dependendo dos dados pode ser _cacheable_
	- `curl -d '{request body}' -H 'request header' -X POST`
	- `curl -d '{"id": 2, "title": "json-server-2", "author": "Wesley Silva"}' -H "content-type: aplication/json" -X POST http://localhost:3000/posts` 
 - `PUT` - Criar um novo ou atualizar um recurso completamente, idempotente.
	 - `curl -d '{"name": "Wesley"}' -H 'content-type: aplication/json -X PUT http://localhost:3000/profile'`
- `PATCH` - Modificação parcial de um recurso, não é idempotente
	- `curl -d '{"title": "my-title"}' -H "Content-type: application/json" -X PATCH http://localhost:3000/posts/1`
- `DELETE` - Remover um recurso, Idempotente
	- `curl -X DELETE http://localhost:3000/posts/2`

## Header
Campos informativos sobre a requisição (_Request_), possuem a estrutura de `Propriedade: Valor`, alguns exemplos
- `Content-Type: application/json`
- `User-Agent: Chrome`
- `method: GET`
- `path: /`
- `scheme: https`

## Body
Conteúdo da requisição (_Request_), por exemplo um `JSON` contendo os dados de um cadastro, ou seja, os dados que estamos enviando para o servidor, entre outros.

# Response
_Response_ é a resposta que o servidor envia para o _Request_ que enviamos, assim criando a comunicação.

![[Desenho_Web_Response|300center]]

## Status Code
Valor inteiro, normalmente de 3 dígitos, que informa a resposta do servidor sobre o estado da requisição (_Request_).
- `100` - Continue
- `200` - OK (GET, POST)
- `201` - Created (PUT)
- `204` - No Content (DELTE, PUT)
- `301` - Moved Permanently, Redirecionamento, por exemplo acessa por uma URL ele te envia para outra (GET)
- `308` - Permanent Rediret (POST)
- `302` - Found, encontrado e você vai ser redirecionado (GET)
- `307` - Temporary Redirect
- `400` - Bad Request, pedido mau efetuado
- `401` - Unauthorized, Sem autorização, não logado por exemplo
- `403` - Forbidden, Não tem permissão
- `404` - Not Found, Não foi encontrado
- `405` - Method Not Allowed
- `429` - Too Many Requests
- `500` - Internal Server Error, Erro interno no servidor
- `503` - Service Unavaiable

## Header
Campos informativos sobre a resposta (_Response_), possuem a estrutura de `Propriedade: Valor`, alguns exemplos
- `content-length: 220`
- `content-type: text/html; charset=UTF-8`
- `cache-control: public, max-age=2592000`

## Status Message / Body
Seria o _body_, ou seja, contem o conteúdo da resposta (_Response_), por exemplo o HTML da página, um JSON contendo as informações que enviamos para API pelo _Body_ do nosso _Request_, entre outros.

# Conceitos
HTTP possui conceitos que é importante serem conhecidos, para maior conhecimento da Tecnologia.
HTTP foi feita para ser legível e de fácil leitura para qualquer pessoa, independente do seu nível de conhecimento.
Se baseia na ideia de **Cliente/Servidor**, onde essa comunicação é feita através de trocas de mensagens chamadas de _Request_ e _Response_.
Assim como o [[Introdução a Programação Funcional|paradigma de programação funcional]], HTTP também possui a característica _Stateless_, ou seja, não guarda estado (informação), assim não existindo relação com outras conexões, normalmente quando acessamos um site novamente e ele já esta logado, é por que o navegador armazenou a sessão seja por _cookies_ ou _local storage_, e não o protocolo HTTP.

# Proxies
Proxies são as maquinas entre o cliente e o servidor muitas vezes chamados de representantes, que ajudam a fazer o transporte dos dados, por exemplo o mais conhecido e presente na maioria das casas é o roteador, os proxies possuis diversas funções sendo entre elas
- Cache
- Filtro (Tipo um antivírus ou controle parental)
- Load Balancing (Distribuição de carga)
- Autenticação
- Autorização

# URI
URI significa _Uniform Resource Identifier_, um identificador único de um **recurso**, onde sua identificação é feita pelo nome ou localização.

## Resource (Recurso)
Recurso é o alvo do pedido HTTP, ou seja, que pode ser referenciado pela [[#Locator (Localização)]] ou pelo [[#Name (Nome)]], esse recurso pode ser qualquer coisa identificável ou também chamado de entidade
- **Digital** - E-mail (Porem e-mail é acessado por outro protocolo)
- **Abstrata** - Sessão, Autenticação
- **Físico** - Produto, Usuário
Em suma  se podemos identificar, nomear, endereçar ou manipular, estamos falando de um recurso.

## Locator (Localização)
Podemos encontramos o recurso pela localização, que nada mais é do que a endereço URL que significa _Uniform Resource Locator_.
Toda URL será uma URI, mas nem toda URI é uma URL.
Uma URL deve ser composta pelos seguintes elementos, sendo eles

![[Desenho_Web_URL|800center]]

### Obrigatórios
- Protocolo
- Domínio

### Opcionais
- Subdomínio
- Path
- Parâmetros
- Porta
- Âncora

## Name (Nome)
Podemos encontrar um recurso pelo nome, que nada mais é do que a URN que significa _Uniform Resource Name_, segui os exemplos
- `urn:isbn:0451450523`
- `urn:oasis:names:specification:docbook:dtd:xml:4.1.2`