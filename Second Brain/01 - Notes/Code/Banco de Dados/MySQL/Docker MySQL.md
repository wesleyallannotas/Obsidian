---
title: Note
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [bd]
description: Usando MySQL via docker
---
# Inicializando Imagem
Baixando caso não exista a imagem no PC, e criando o contêiner com a ultima versão do MySQL, passando senha "root" para o usuário root
```bash
docker run -p 3306:3306 --name my-mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:8
```
# Entrando do Contêiner
Entrando no contêiner utilizando o shell bash
```bash
docker exec -it my-mysql /bin/bash
```
# Logando no MySQL
```bash
mysql -u root -p -A
mysql -u user -p
```
# Liberando ROOT
Só é necessária para a imagem `mysql/mysql-server`, para a ==imagem padrão já vem configurado.==
```sql
UPDATE mysql.user SET host='%' WHERE user='root';
flush privileges;
```

# Outra ideia
```sh
docker run --name nome-do-container  \
-p 3306:3306 -p 33060:33060  \
-e MYSQL_ROOT_HOST='%' -e MYSQL_ROOT_PASSWORD='sua-senha'   \
-d mysql/mysql-server:latest
```