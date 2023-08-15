---
title: Usuários e Permissões
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [mysql]
description: Como criar e manipular permissões de usuários 
---
# Criando Usuário
Dentro do servidor de banco de dados podemos criar um usuário através do comando `create user`

```mysql
create user 'user'@'localhost' identified by 'senha123'; 
```

# Permissões
Podemos manipular as permissões deste usuário através do comando `grant`
```mysql
grant all privileges on *.* to 'user'@'localhost'
```

>[!attention] Atenção
>Após o `on` definimos as permissões nos banco de dados e nas tabelas respectivamentes, ou seja, o primeiro asteriscos pega todos os bancos o segundo todas as tabelas dos bancos e por ultimo após o `to` o usuário

