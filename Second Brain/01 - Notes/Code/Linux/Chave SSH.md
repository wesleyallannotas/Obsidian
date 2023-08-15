---
title: Chave SSH
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [ssh]
description: Como criar e utilizar uma chave SSH 
---
# Introdução
Chaves SSH são chaves assimétricas onde existe uma chave publica que disponibilizamos aos provedores, e a chave privada que deve ser mantida sobre proteção, para a aprovação as duas chaves tem que bater, como um aperto de mão

# Criando
Para criar uma chave SSH utilizando o Linux o comando usado é
```bash
ssh-keygen -o -a 100 -t ed25519 ~/.ssh/id_nomechave -C "email@email.com"  # Akita
ssh-keygen -t rsa -b 4096 -C "email@mail.com" # Dicover
```
Será peido uma frase para ser utilizado como senha, e como foi especificado no comando será armazenado na chave `.ssh`

# Configurando várias chaves
Podemos ter varias chaves e delegar especificas para hosts, por exemplo:

```
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519

Host github-m3code
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_m3code****
```

Assim basta adicionar a origin no github com a Host correto

```sh
git remote add git@github-m3code:M3Code/LumineBackend
```