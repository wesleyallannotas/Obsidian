---
title: Configurando Esquiva
author: Wesley Silva
url: '[Cyberpunk 2077 | Como Trocar a Tecla de Esquiva? | Sacrossauro - YouTube](https://www.youtube.com/watch?v=R9e7N53PO6o)'
book:
type: note
completed: true
aliases:
tags: note
description: Como configurar a esquiva para um botão de escolhar
---
# Alterando Arquivo
Para conseguirmos mudar  o botão da esquiva será ==necessário acessar os arquivos do jogo==, mais precisamente no caminho
```shell
C:\Program Files (x86)\Steam\steamapps\common\Cyberpunk 2077\r6\config
```
Em seguida ==criaremos uma pasta backup== para recuperar os arquivos originais em caso de problema, dentro desta pasta armazenamos copias dos arquivos:
- `inputContexts.xml`
- `inputUserMappings.xml`

## Arquivo `inputContexts.xml`
Dentro do arquivo pesquisaremos `DodgeForward` onde encontraremos as configurações sobre a esquiva, nos seguintes:
- `DodgeForward`
- `DodgeRight`
- `DodgeLeft`
- `DodgeBack`
Mudaremos o `count` de todos para **99**, em seguida alteraremos o pai deles, ou seja, apenas `dodge` para **1**

## Arquivo `inputUserMappings.xml`
Dentro do arquivo pesquisaremos  `Dodge_Button` em seguida ==apague a linha==
```
<button id="IK_LControl" overridableUI="crouchToggle"/>
```
Na linha de baixa apague apenas o trecho
```
overridableUI="crouchToggle"
```
E após `IK` adicione a tecla desejada.