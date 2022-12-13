---
title: Modelos de processos de desenvolvimento de software
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [engSoftware]
description: Modelos já consolidados no mercado
---
# Introdução
Modelos de processos de desenvolvimento de software que já estão estabelecidos no mercado, onde são divididos entre os modelos **clássicos** e os modelos **ágeis**, onde invés de desenvolver um novo modelo, organizações preferem utilizar os modelos já testados amplamente pelo mercado, assim obtendo uma maior probabilidade de exito no desenvolvimento do software.
>[!revisao] Recapitulando
![[01 - Notes/Code/Engenharia de Software/Introdução#Elementos]]

# Ciclo de Vida do Software
Assim como o ser humano o software possui um ciclo de vida, que não é ceifado pelo desgastes físico como o hardware, mas sim uma degradação proveniente de consecutivas alterações no seus código, seja para adicionar funções ou corrigir bugs, assim o software permeia pelos ciclos, de inicio com alta demanda de correção e adição de funcionalidades ate chegar a faze que entrega sua função completamente, porem obviamente ainda passando pro correções, ate chegar a fase do fim da sua vida, quando ou suas tecnologias estão muito defasadas, ou ate mesmo com muita dificuldade de correção, assim tomando muito tempo dos desenvolvedores.
A escolha do **modelo** de processos que permeara por toda a vida do software depende de vários fatores para ser escolhido, podem ser ate mesmo uma escolha hibrida, para melhor atender o desenvolvimento da empresa, pode depender
- Da natureza do projeto e da aplicação (Da empresa desenvolvedora, da empresa cliente, do tipo do software, da necessidade de entrega)
- Dos métodos e ferramentas a serem usadas
- Dos controles e produtos que precisam ser entregues

# Modelos Clássicos
Os modelos criados pela literatura e incorporado inicialmente pelas empresas.
- **Modelo Cascata** - Requer uma abordagem sistemática, ==sequencial ao desenvolvimento== (Um processo só é iniciado apos o fim do anterior)
	- Pode ser inviável para projetos muito grandes, por exemplo uma empresa perder muito tempo documentando e levantando requisitos para começar a desenvolver só depois, pois, só pode começar o processo de desenvolvimento, após acabar todos os anteriores.
- **Modelo Prototipação** - Possibilita que o desenvolvedor crie um modelo do software que dever ser construído.
- **Modelo RAD** - (Rapid Application Development) é um modelo iterativo e incremental que enfatiza um ciclo de desenvolvimento extremamente curto.
- **Modelos Evolutivos** - Combinação de vários modelos de desenvolvimento de software.
- **Técnicas de 4 Geração** - Os requisitos os quais são traduzidos para um protótipo operacional, pulando a parte do desenvolvimento do software (low-code, no-code).

# Modelos Ágeis
Modelos adaptados para à realidades das industrias/empresas de desenvolvimento de software.

>[!info] Criação
>Em 2001, **Kent Beck** e mais **16 desenvolvedores, produtores e consultores** de software, que formavam a **Aliança Ágil**, assinaram o **Manifesto do Desenvolvimento Ágil de Software**

Podemos perceber que os modelos clássicos forem criado por **pesquisadores** dentro das academias e foram enviados para a industria, e os modelos ágeis, percorreram o percurso contrario, a industria desenvolveu e envio para as academias (Buscando mais agilidade no desenvolvimento), menas documentação e mais codificação, através de mais contado com o cliente.
Em seu livro, **Pressman(2010)** apresenta as seguintes metologias ágeis:
- XP (Extreme Programming)
- DAS (Desenvolvimento Adaptativo de Software)
- DSDM (Dynamic Software Development Method)
- Scrum - (O mais utilizado atualmente) Equipes dividias em células de trabalho que possuem vários membros, onde cada um fica responsável pelo desenvolvimento de uma parte e possuem um líder, com entregas particionadas no menor tempo possível.
- Crystal
- FDD (Feature Drive Development)
- Modelagem ágil (AM)
- Processo Unificado Ágil (AUP)
- DevOps (não esta do livro) - Muito utilizado junto com o Scrum, trabalha a parte da produção de software e colocar o software em produção.