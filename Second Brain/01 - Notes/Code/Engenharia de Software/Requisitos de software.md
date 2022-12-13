---
title: Requisitos de software
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [engSoftware]
description: Tipos de requisitos e como ser escritos e detalhados.
---
# Introdução
A parte mais árdua da construção do software, se errar nessa etapa ocorre grandes chances de comprometer o projeto inteiro, se atentar muito a cada detalhe, pois, uma informação mau interpretada ou omitida pode trazer danos irreversíveis 

# Especificação ≠ Requisito
Especificação é diferente de requisito.
Requisitos podem ser escritos como bem entender desde que contemple seu objetivo completamente
Esse documento sera lido por todos os envolvidos por isso precisa ser uma linguagem que todos entendem e que esteja bem especificado.

>[!note] Requisito
>**Condição** necessária para a **obtenção** de certo **objetivo**, ou para **preenchimento** de certo **fim**.

>[!note] Especificação
>**Descrição** rigorosa e minuciosa das **características** (Requisito) que um material, uma obra, ou um serviço **deverão apresentar**

- **Especificação de Requisitos** - Serve como padrão para checar se as fases de projeto e implementação do processo de desenvolvimento de software estão corretas.

## Exemplo
- **Requisito** - Cadastro de Aluno
- **Especificação** -  O cadastro do aluno deverá conter todas as informações necessárias para satisfazer as necessidades da Toledo Prudente, Dentre elas será necessário: Nome, RG, CPF, Comprovante Militar, Endereço, outros... Quando um aluno for incluir um novo cadastro, o sistema devera validar se o nome e o CPF já estão cadastrados no banco de dados da Toledo, de forma a não duplicar as informações. O CPF informado pelo aluno, deverá ser validado de forma a garantia que o mesmo está correto. Todos os documentos deverão ser anexo dos digitalmente no ato do cadastro.
	- Outros... ocorre pois é apenas uma explicação, isso nunca deve ocorrer em um projeto real, deve estar tudo explicitamente especificado.
	
# Tipos de Requisitos