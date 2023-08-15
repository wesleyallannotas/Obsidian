---
title: Firebird
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: firebird
description: Criando uma instancia do firebird no docker
---
# 🚀 Introdução
Para subir um Firebird 3.0 em um contêiner Docker, você pode seguir os seguintes passos:

1.  Primeiro, crie um arquivo Dockerfile com o seguinte conteúdo:

```dockerfile
FROM alpine:latest
RUN apk update && apk add firebird
EXPOSE 3050/tcp
CMD ["usr/sbin/fbguard", "-forever"]
```

2.  Em seguida, execute o comando a seguir para criar uma imagem Docker com base no Dockerfile:

```sh
docker build -t firebird3.0 .
```


3.  Depois de criar a imagem, execute o contêiner com o seguinte comando:

bashCopy code

```bash
docker run -p 3050:3050 -v /data/firebird:/var/lib/firebird/3.0/data --name firebird firebird3.0
```

O comando acima cria um contêiner com o nome "firebird", mapeando a porta 3050 do contêiner para a porta 3050 do host e montando um volume no diretório /data/firebird do host para o diretório /var/lib/firebird/3.0/data do contêiner. Certifique-se de ajustar o diretório de volume para um diretório existente no seu host.

4.  Para verificar se o Firebird está em execução, você pode executar o seguinte comando para entrar no contêiner:

```bash
docker exec -it firebird bash
```

Dentro do contêiner, você pode usar o utilitário "isql" para se conectar ao servidor Firebird:

```bash
isql-fb -user SYSDBA -password masterkey
```

Se a conexão for bem-sucedida, você poderá executar comandos SQL no banco de dados Firebird