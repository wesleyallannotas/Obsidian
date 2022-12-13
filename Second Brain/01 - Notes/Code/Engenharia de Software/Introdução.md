---
title: Introdução a Engenharia de Software
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [engSoftware]
description: Introdução abortando a historia e o que é engenharia de software.
---
# Introdução
**Software** é uma sequencia de **instruções** que quando executado produzem a função e o desempenho desejado, que utiliza de **estrutura de dados** para manipular as informações adequadamente, também é considerado parte do software os **documentos** gerado parar a utilização do mesmo, como por exemplo colocá-lo no mercado.
O software não desgasta como o hardware que é físico e com o seu tempo de uso vai perdendo seu real poder, porem o software **deteriora**  através das varias intervenções que ocorre em seu código, assim o tornando cada vez mais inflexível, e encarecendo manutenções futuras. 
- **SIBC** - Sistema de Informação Baseado em Computador.
Baseado em computador, pois, existem sistemas de informações mais simples, por exemplo utilizando papel e caneta, ou ate mesmo guardando na mente.
>[!cite] Segundo Pressman SIBC
Conjunto ou disposição de **elementos**, organizado para **executar certo método**, **procedimento ou controle ao processar informações**
![[Desnho;engSoftware;SIBC]]

Percebemos que esta tudo ligado, a organização possui um **software** que necessita de um **hardware** para rodar, onde, possui seus **procedimentos** que são os processos que a empresa executa utilizando o hardware que vem de **pessoas** que conhecem os **processos** e o **software** para que consiga trabalhar, ou seja, executar os processos, onde o **software** possui o banco de dados para armazenar as informações e dados que terá interação com os **processos** executados pelas **pessoas** através do **software** em seu **hardware**, onde toda esse interação ocorre através da **telecomunicação**, ou seja, as redes que integra tudo, assim recebendo a **entrada** dos dados e gerando a **saída** através de toda essa interação.

Antes do 1965, quem possuía maior importante dentro das organizações era o hardware, onde o priorizaram na compra e deixa o software em segundo plano, porem a partir dos anos 1965, houve a virada de chave, e as organizações perceberam a importância de softwares bem desenvolvidos, com a chegada de gerenciadores de banco de dados (SGBD), a necessidade de multiusuários em tempo real no mesmo hardware, e começaram a enxergar o software como produto, essa mudança repentina e a alta demanda de software gerou a **crise do software**, pois, não existia padrões de desenvolvimento nem atenção as melhores praticas, assim houve a chegada da engenharia para software trazendo melhores processos e praticas.
- Hoje me dia houve uma inversão onde o ==software é mais caro do que o hardware==
# Crise do Software
A crise do software ocorre decorrente de alguns problemas entre eles os a baixos, onde como resposta veio a **engenharia** buscar resolver os mesmo.
- **Imprecisão** na estimativa de **prazo e custo**
- **Insatisfação** do cliente com o software desenvolvido
- **Qualidade do software** as vezes não atingia a necessidade da empresa contratante
- **Dificuldade na manutenção** de software existente
# Engenharia
Para enter como a engenharia de software foi capaz de resolver esses problema, precisamos entender o a definição de engenharia
- Ciência de adquirir e de aplicar conhecimento matemático, técnicos e científicos na criação, aperfeiçoamento e implementação de utilidades tais como materiais, estruturas, máquinas, aparelhos, sistemas ou processos, que realizam uma determinada função ou objetivo.
Aplicações dos princípios científicos a:
- Exploração dos recursos naturais
- Projeto e à construção de comodidades
- Fornecimento de utilidades
# Engenharia de Software
O objetivo da engenharia de software para acabar com a crise dos software é trazer **produtos de software de alta qualidade,** com **produção rápida** e **custo reduzido.**
>[!cite] Segundo Pressman
>Estabelecimento e uso de sólidos princípios de engenharia para que se possa obter um software economicamente viável que seja confiável e que funcione eficientemente em máquinas reais

>[!cite] Segundo IEEE (Padrão paras engenharias)
>Aplicação de uma abordagem sistemática, disciplinada e possível de ser medida para o desenvolvimento, operação e manutenção do software

## Elementos
- **Ferramentas** - Apoio automatizado ou semi-automatizado aos métodos
	- Existem ferramentas para todos os métodos
	- Quando as ferramentas são integradas é estabelecido um sistema de suporte ao desenvolvimento de software chamada **CASE** (Computer Aided Software Engineering)
- **Métodos** - Proporcionam os detalhes de como fazer para construir o software
	- **Como** desenvolver o software detalhadamente
	- **Notações** de requisito de software, como traduzir o que o usuário quer para o desenvolvedor
- **Processo** - Elo de ==ligação entre métodos e ferramentas==, como vou realizar as atividades utilizando as ferramenta que existem e os métodos.
- **Qualidade** - Objetivo produzir produtos de software com qualidade.
## Princípios da engenharia de software
- **Formalidade** - **Especificado e documentado** aquilo que se pretende produzir
- **Abstração** - Permite que o desenvolvedor se concentre no problema a ser resolvido
- **Decomposição** - Subdivisão do trabalho em atividades específicas, dividir o grande software que precisa ser desenvolvido em partes menores.
	- **Decomposição do Processo** - **Planejamento das atividades**, para **não perder tempo** na mudança entre atividades
	- **Decomposição do Produto** - Permite que **atividades de desenvolvimento** sejam feitas **em paralelo**
- **Generalização** - Solução mais **geral** para um problema tem maior potencial de ser **reutilizado**, ou seja, um mesmo software poder atender clientes diferentes.
- **Flexibilização** - Permitir que o produto possa ser **modificado com facilidade**