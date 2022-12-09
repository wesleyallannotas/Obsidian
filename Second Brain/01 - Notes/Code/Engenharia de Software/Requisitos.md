---
title: Requisitos de software
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [note, engSoftware]
description: Tipos de requisitos e como ser escritos e detalhados.
---
# Requisitos de software
A parte mais árdua da construção do software, se errar nessa etapa ocorre grandes chances de comprometer o projeto inteiro, se atentar muito a cada detalhe, pois, uma informação mau interpretada ou omitida pode trazer danos irreversíveis 

## Especificação ≠ Requisito
Especificação é diferente de requisito.
Requisitos podem ser escritos como bem entender desde que contemple seu objetivo completamente
Esse documento sera lido por todos os envolvidos por isso precisa ser uma linguagem que todos entendem e que esteja bem especificado.

>[!note] Requisito
>**Condição** necessária para a **obtenção** de certo **objetivo**, ou para **preenchimento** de certo **fim**.

>[!note] Especificação
>**Descrição** rigorosa e minuciosa das **características** (Requisito) que um material, uma obra, ou um serviço **deverão apresentar**

- **Especificação de Requisitos** - Serve como padrão para checar se as fases de projeto e implementação do processo de desenvolvimento de software estão corretas.

### Exemplo
- **Requisito** - Cadastro de Aluno
- **Especificação** -  O cadastro do aluno deverá conter todas as informações necessárias para satisfazer as necessidades da Toledo Prudente, Dentre elas será necessário: Nome, RG, CPF, Comprovante Militar, Endereço, outros... Quando um aluno for incluir um novo cadastro, o sistema devera validar se o nome e o CPF já estão cadastrados no banco de dados da Toledo, de forma a não duplicar as informações. O CPF informado pelo aluno, deverá ser validado de forma a garantia que o mesmo está correto. Todos os documentos deverão ser anexo dos digitalmente no ato do cadastro.
	- Outros... ocorre pois é apenas uma explicação, isso nunca deve ocorrer em um projeto real, deve estar tudo explicitamente especificado.
	
## Tipos de Requisitos
Os requisitos podem ser classificados
- **Organização**
	- Funcionais
	- Não Funcionais
	- Inversos
- **Tipo de Detalhamento**
	- De Usuário
	- De Sistemas
	- Interfaces Externas
	- Especificação de Projeto de Software
	
### Requisitos Funcionais
São funcionalidades que o sistema vai ter, descreve **o que** o software vai fazer, devem ser **completos**, **precisos** e **consistentes**.
>[!example] Exemplo
É perceptível que falta especificar (detalhar)
>- **RF001** - O sistema a deve permitir que um aluno realize sua matricula em uma disciplina pela internet.
>- **RF002** - O sistema deve permitir que um cliente realize empréstimo de mais de um livro.
>- **RF003** - O sistema deve controlar o horário de entrada e saída dos funcionários.
- **RF** - Requisito Funcional
- **001...** - Sequencia numérica para criar uma chave facilitando a identificação

### Requisitos Não Funcionais
Relacionados aos **aspectos de qualidade** (por exemplo ser acessível a todos os navegadores) que o software ira apresentar ou **restrição** (por exemplo tempo máximo de espera 3 segundos)  a serem atendidas
>[!example] Exemplo
É perceptível que falta especificar (detalhar)
>- **RNF001** - O tempo de  resposta para uma consulta deve demandar no máximo 3 segundo
>- **RNF002** - O sistema deve ser executado no ambiente Windows
>- **RNF003** - O usuário será capaz de utilizar todos as funcionalidades dos sistema após 2 horas de treinamento
>- **RNF004** - O relatório mensal dos horários, por funcionários, deve ser impresso em papel timbrado
- **RNF** - Requisito Não Funcional
- **001...** - Sequencia numérica para criar uma chave facilitando a identificação

### Requisitos Inversos
Relacionados a **condições** que **nunca** poderão **ocorrer** ou que estão **fora do escopo** da solução.
>[!example] Exemplo
É perceptível que falta especificar (detalhar)
>- **RI001** - O sistema não deve permitir apagar os dados do cliente.
>- **RI002** - O sistema deverá ser implementado somente em idioma nacional.
>- **RI003** - O sistema não emitirá nota fiscal
>- **RI004** - O sistema não permitirá vender a crediário.

### Detalhamento  de Requisitos do Usuário
Declaração em nível de usuário, utilizando linguagem natural ou diagramas, sobre as ==funções quais deve operar== (Funcionais e não funcionais)
>[!example] Exemplo
>1. Software deve oferecer um meio de representar e acessar arquivos externos criados por outras ferramentas

### Detalhamento de Requisitos de Sistema
Estabelecem detalhadamente as ==restrições que o sistema deverá atender== (são descrições mais detalhadas dos requisitos do usuário; ponto de partida para o projeto do sistema)
Escritos para ==servir como contrato==
>[!example] Exemplo
>1.1. O usuário deve dispor de recursos para definir o tipo dos arquivos externos
>1.2. Cada tipo de arquivo externo pode ter uma ferramenta associada
>1.3. Cada tipo de arquivo externo pode sr representado por um ícone específico na tela do usuário
>1.4. Quando um usuário seleciona um arquivo externo, a ferramenta associada é ativada para manipular adequadamente esse arquivo

### Detalhamento Requisitos de Interfaces Externas
Interfaces externas estabelecem requisitos para o sistema possa **interoperar** com **outros sistemas** e com os **usuários** (são, portanto, requisitos de sistema) O IEEE classifica as interfaces externas em
- Interfaces de usuário
- Interfaces de hardware
- Interfaces de software
- Interfaces de comunicação
As interfaces de software definem
- Procedimentos (Serviços providos/requiridos)
- Estruturas de dados (trocados entre sistemas)
- Representação de dados trocados (XML, Base64, ...)

### Detalhamento Especificação de Projeto de Software
Descrição ==abstrata de projeto== de software; base para o ==projeto e a implementação==
Acrescenta ==mais detalhes== à especificação dos requisitos de sistema
==Escrita para desenvolvedores==

# Obtenção de Requisitos
Utilizando as **técnicas** corretas e as perguntas corretas para ==extrair os requisitos de forma eficiente do cliente==, o engenheiro de software deve ==compreender conceitos abstratos== que vem da cabeça do cliente e **reorganizar** de forma logica e sintetizar  em uma solução, ou seja, necessita de uma capacidade para **absorver fatos** pertinentes a partir de **fontes conflitantes** (Por exemplo duas pessoas do mesmo setor em entrevistas passando informações diferentes) ou **confusas**, e com essas informações em mãos o engenheiro de software deve possuir uma habilidade de **se comunicar bem** tanto de maneira escrita como verbal.
>[!cite] 
>Capacidade de **ver a floresta em vez das árvores**

## Alguns Meios de Coleta de Dados
- Entrevista
- Coleta de Documentos
- Observação

## Levantamento de Requisitos
- Levantas as primeiras informações sobre o sistema para definir o escopo do software
- Entender quem é o cliente
- Entender qual é o problema
- Entender quem são as pessoas chaves (Quem realmente entende o problema a ser resolvido, ou seja, maior potencial para fornecer requisitos)
- FeedBack sobre o processo de levantamento de requisitos (Conversar com o cliente para compreender se você esta entendendo corretamente)

# Técnicas  Para Levantamento de Requisitos
Existem diversas técnicas que podem ser utilizadas para obter exceto nesta tarefa, entre elas
- Entrevista
- Questionário
- Brainstorming
- Rastreamento de Processos
- Estudo de Caso
- Simulação e Protótipos

## Entrevista
Técnica mais utilizada entre os engenheiros de software, porem é uma técnica que exige habilidade do entrevistador, onde o mesmo deve instigar o seus entrevistado a passar o máximo de informações uteis, existem duas formas de fazer a entrevista sendo elas
- **Entrevista Desestruturada** - Buscamos entender as necessidades de forma macro, não possui uma estrutura especifica para esta conversa
- **Entrevista Estruturada** - Quando se deseja informações especificas do conteúdo e do problema, ou seja, conhecendo o software que sera desenvolvido podemos aproveitar para detalhar os requisitos
O Background que o **entrevistador** possui sobre aquele assunto e te extrema importância, ou seja, caso não conheça aquela segmento de mercado, e interessante realizar uma pesquisa para elaborar e encaminhar a entrevista da melhor forma possível.
É de extrema importância **planejar a entrevista**, **definindo uma forma de anotação** (Manual, Gravação em fita ou em vídeo), claro com o **consentimento do entrevista** para não causar desconforto, importante se atentar ao agendamento de horário, pois, o entrevistado provavelmente tem tarefas para realizar na empresa, não estando disponível o dia todo.

### Durante a Entrevista
- **Motivar os participantes**, para fornecer o mais numero de informações relevantes, porem deve se atender a não perder o foco da entrevista.
- **Fornecer um resumo verbal do problema**, ouvir o entrevista e retornar ao mesmo o que você entender a fim de verificar e eliminar ruídos na comunicação.
- **Relacionar a pergunta inicial com o tópico global da sessão**, ou seja, manter o foco no tópico do momento, ou seja, se estão falando sobre a tela de cadastro tirar todas as duvidas da mesma evitando alternância entre diferentes tópicos ou manter vários em paralelo.

### Após a entrevista
Exemplo o que o senhor espera sobre a tela de cadastro
- **Documentar todos os pontos relevantes obtidos**
- **Enviar a documentação ao entrevistado**, buscando uma aprovação final, ou seja, confirmando se os dados ali contidos refletem as reais necessidades.
- Se for **necessário um esclarecimento postérios**, contatar o entrevistado pra marcar outra reunião

### Perguntas Abertas
Exemplo quem possuirá permissão para cadastrar no sistema
- Tender a não ser especificas
- Não são seguidas por alternativas
- Encorajam resposta livre
- Apropriadas quando deseja-se observar respostas de alto nível para reconhecer o escopo de entendimento do entrevistado
- Possibilitam ao entrevistado o fornecimento de informações que o entrevistador não tem conhecimento para perguntar
- As respostas a essas perguntas consomem muito tempo, e podem trazer pouca informação

### Perguntas Fechadas
- Definem limites no tipo, nível e quantidade de informação fornecida pelo entrevistado
- Fornecem escolha de alternativas ou níveis de resposta

### Níveis de Perguntas
- **Primárias** - Aquelas que o entrevistador usa para introduzir áreas ou transições para outras áreas
- **Secundárias** - Perguntas, na maioria das vezes, exploradoras, ou seja, descobrir mais sobre determinado tema.
	- **Propósito** - Descobrir mais sobre as informações oferecidas em resposta em alguma pergunta
	Tomar cuidado com **respostas ambíguas**, **comentários irrelevantes**, **resposta genéricas**, entre outras...
	
## Questionário
Quando se vê a possibilidade de **extrair informações de uma massa de pessoas** sendo impossível marcar reunião com todos, preparar antecipadamente com **questões objetivas**, como **desvantagens** temos a comunicação restringida, ou seja, **não há o contado verbal**, o contado direto, e a **preparação exige tempo**, durante a preparação é necessário
- Identificar o tipo de informação que deseja obter
- Escolher um **formato adequado** para o questionário (Papel, Formulário Eletrônico)
- Deixar espaço suficiente para resposta de questões descritivas
- Montar questões de maneira simples,clara e concisa
- Enviar uma carta acompanhando o questionário para enfatizar a sua importância
- Identificação é opcional, optando pelo anonimato ou não
- Sua distribuição deve ser controlada, buscando qualidade na resposta e ate mesmo evitar perda de tempo
- Após a obtenção das respostas, e necessário **analisar e consolidar as informações coletas**, documentar as **principais descobertas** e **enviar um relatório** com as principais descobertas para todos os respondentes, transmitindo uma mensagem implícita de agradecimento e importância no tempo que disponibilizaram

## Brainstorming
Em tradução livre seria "Tempestade de ideias", se baseia em uma técnica onde por meio de exercícios fomenta a criatividade e a geração de ideias do grupo participante, muito útil, principalmente para **sessões inciais de levantamento de requisitos**

## Rastreamento de Processos
Acontecia na observação de como o processo ocorre na organização, pode ser **verbalizado** com conversa direta com os participantes do processo explicando enquanto realiza, existe também a **verbalização retrospectiva** onde primeiro realiza o processo depois explica todo o processo

## Estudo de Caso
Obtém-se o conhecimento através de **outros softwares** que já foram resolvido para aquela realidade, ou seja, parti de projetos que obterão sucesso na mesma realidade.

## Simulações e Protótipos
Criar protótipos pare representar aquilo que espera, um paralelo importante e com a área da construção civil, onde são criados protótipos que mostrarão como sera o projeto pronto, o mesmo ocorre aqui, criando imagens e telas simplesmente visuais, exemplificando o funcionamento, muito usado pela galera de design

## Sugestão de Aplicação das Técnicas
Uma simples sugestão não existe uma melhor forma
- **Etapas Iniciais** - Entrevista Desestruturada, Questionário, Brainstorming
- **Etapas Intermediárias** - Entrevista Estruturada
- **Etapas Finais** - Entrevista Estruturada, Rastreamento de Processo, Simulações e Protótipos