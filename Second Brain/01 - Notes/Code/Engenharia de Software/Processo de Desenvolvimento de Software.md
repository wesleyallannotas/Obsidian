---
title: Processo de Desenvolvimento de Software
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [engSoftware]
description: As etapas e processo para obter um bom desenvolvimento de software 
---
# Processo de Desenvolvimento
Vem para diminuir as frustrações com o desenvolvimento abaixo do esperado do software desenvolvido, ainda mais na era que vivemos que é conhecida como **Era da Qualidade**, onde os usuários exigem qualidade no software que utilizam, ainda mais com a ampla concorrência que área traz, assim ==qualidade não e mais uma vantagem e sim uma obrigação== para se manter competitivo.

# Etapas do Desenvolvimento
- **Código** - Entorno de 7%
- **Modelagem do Projeto** - Entorno de  27%
- **Levantamento de Requisitos** - Entorno de 56%
- **Outros** - Entorno de 10%

# Fases Genéricas
1. **Análise** - ==Estabelecer requisitos e restrições==, como o cliente quer que funcione o sistema, por exemplo para realizar uma venda é apenas pelo computador, ou vai ter mobile também, entre outros, ou seja, definir o comportamento e funções do software.
2. **Projeto** - Projetar o software, gerar a documentações para a produções do mesmo.
3. **Implementação** - Construir o sistema.
4. **Verificação, Validação e Testes** - Verificar se o software atende as necessidades estabelecidas na análise e se não apresenta erros (bugs).
5. **Implantação** - Liberar o sistema para o cliente e garantir sua funcionalidade, treinando, configurando entre outros.
6. **Manutenção** - Eliminar defeitos e evoluir o sistema conforme demanda, se mantem no mesmo ate o fim da vida útil do software.

# Qualidade de Software
>[!cite] Pressman, 1994
>Qualidade de software é a **conformidade** a **requisitos** funcionais e de desempenho que foram explicitamente declarados, a **padrões de desenvolvimento** claramente documentados, e a **características implícitas** que são esperadas de todo software desenvolvido por profissionais
>>[!note]- Em outras palavras
Software que atende as necessidades do cliente, que possui padrões de desenvolvimento e que esteja atendendo todas as características documentadas e implícitas de um software

Qualidade de software possui um significado diferente para cada tipo de ser que interage com o mesmo, por exemplo:
- **Usuário** - Facilidade de uso, desempenho, confiabilidades dos resultados, preço do software, entre outros
- **Desenvolvedor** - **Alem das preocupações do usuário**, taxa de defeitos, facilidade de manutenção e conformidade em relação aos requisitos dos usuários, entre outros
- **Organização** - **Alem das preocupações dos usuários e Desenvolvedores**, cumprimento de prazo, boa previsão de custo, boa produtividade.
Através desses **requisitos** levantando com todos os participantes entramos na faze do desenvolvimento do software passando pelas [[Processo de Desenvolvimento de Software#Fases Genéricas|fases genéricas]] atendendo aos padrões.

# Processo
>[!cite] NBR ISO 9000, 2000
>Qualquer atividade, ou conjunto de **atividades**, que utiliza recursos para **transformar insumos** (entradas) **em produtos** (saída)

>[!cite] IEEE 610.12, 1990
>Conjunto de **passos** realizados para atingir um determinado **propósito**

Algumas características de um processo:
- Estabelece a ordem que deve ser seguida
- Utiliza recursos
- Está sujeito a restrições
- Gera produtos intermediários e finais (Bolo não ficar tão bom, fazer outro)
- Pode ser composto de sub-processos relacionados (Fazer a cobertura do bolo)
Para que o processo funcione é necessário **procedimentos e métodos** que descrevem a relação entre as taregas, **ferramentas e equipamentos** para para realização da tarefas e ajudar na resolução das mesmas, e **pessoas** com capacidades de realizar as atividades.

# Modelos de Processos de Desenvolvimento
Modelos de processos de desenvolvimento de software que já estão estabelecidos no mercado, onde são divididos entre os modelos **clássicos** e os modelos **ágeis**, onde invés de desenvolver um novo modelo, organizações preferem utilizar os modelos já testados amplamente pelo mercado, assim obtendo uma maior probabilidade de exito no desenvolvimento do software.
>[!revisao] Recapitulando
![[01 - Notes/Code/Engenharia de Software/Introdução#Elementos]]

## Ciclo de Vida do Software
Assim como o ser humano o software possui um ciclo de vida, que não é ceifado pelo desgastes físico como o hardware, mas sim uma degradação proveniente de consecutivas alterações no seus código, seja para adicionar funções ou corrigir bugs, assim o software permeia pelos ciclos, de inicio com alta demanda de correção e adição de funcionalidades ate chegar a faze que entrega sua função completamente, porem obviamente ainda passando pro correções, ate chegar a fase do fim da sua vida, quando ou suas tecnologias estão muito defasadas, ou ate mesmo com muita dificuldade de correção, assim tomando muito tempo dos desenvolvedores.
A escolha do **modelo** de processos que permeara por toda a vida do software depende de vários fatores para ser escolhido, podem ser ate mesmo uma escolha hibrida, para melhor atender o desenvolvimento da empresa, pode depender
- Da natureza do projeto e da aplicação (Da empresa desenvolvedora, da empresa cliente, do tipo do software, da necessidade de entrega)
- Dos métodos e ferramentas a serem usadas
- Dos controles e produtos que precisam ser entregues

## Modelos Clássicos
Os modelos criados pela literatura e incorporado inicialmente pelas empresas.
- **Modelo Cascata** - Requer uma abordagem sistemática, ==sequencial ao desenvolvimento== (Um processo só é iniciado apos o fim do anterior)
	- Pode ser inviável para projetos muito grandes, por exemplo uma empresa perder muito tempo documentando e levantando requisitos para começar a desenvolver só depois, pois, só pode começar o processo de desenvolvimento, após acabar todos os anteriores.
- **Modelo Prototipação** - Possibilita que o desenvolvedor crie um modelo do software que dever ser construído.
- **Modelo RAD** - (Rapid Application Development) é um modelo iterativo e incremental que enfatiza um ciclo de desenvolvimento extremamente curto.
- **Modelos Evolutivos** - Combinação de vários modelos de desenvolvimento de software.
- **Técnicas de 4 Geração** - Os requisitos os quais são traduzidos para um protótipo operacional, pulando a parte do desenvolvimento do software (low-code, no-code).

## Modelos Ágeis
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