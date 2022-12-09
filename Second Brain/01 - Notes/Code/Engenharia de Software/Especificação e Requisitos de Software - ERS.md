---
title: 'Especificação e Requisitos de Software - ERS' 
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [note, engSoftware]
description: Padroes para documentação de requisitos.
---
# Introdução
Documentar requisitos de software através do padrão IEEE 830/1998 elaborado pelo *Institute of Electrical and Eletronics Engineers* para **Especificação de Requisitos de Software (ERS)**
- **ERS/SRS** - *Software Requiremets Specification* - Documento que o cliente consegui expressar suas necessidades e o desenvolvedor consegui entende-las, seria um Documento de Requisitos, ele que norteara o desenvolvimento do software (Contrato entre Desenvolvedor e Cliente).
- Quanto à **natureza** da ERS - É uma especificação de produto de software que realiza certas funções em um ambiente especifico.
- Quanto ao **ambiente** da ERS - A ERS deve estar de acordo com os requisitos do sistema, deve estar correta ao que se pretender desenvolver, não detalha sobre implementação ERS esta no nível de usuário, não estabelece restrições adicionais.
- Quanto às **características** da ERS - **Ser correta** (Requisitos expressos devem ser encontrados no software), **Ser não ambígua** (Cada requisito declarado possuir apenas uma interpretação), **Ser Completa** (Incluindo todos os requisitos, respostas para todas entradas e saídas, Referências para todas as tabelas, unidades de medidas, diagramas), **Ser Consistente** (Não deve haver conflitos entre requisitos), **Possuir grau de importância e/ou estabilidade** (Cada requisito deve identificar seu grau de importância ou estabilidade em relação a outros (uns são essenciais, outros desejáveis) (Grau de Estabilidade - Pode ser expresso em termos de número mudanças esperadas para algum requisito) (Grau de Necessidade - Essencial, Condicional, Opcional) **Ser Verificável** (Quando for possível checar cada requisito, ter sua rastreabilidade) **Ser Modificável** (Possuir facilidade na modificação no andamento do projeto, no seu ciclo de vida, pois, o software amadurece com o passar do tempo) **Ser Rastreável** (A origem de cada requisito deve ser documentada e clara)  
- Quanto à **preparação da junção** da ERS - Cliente e fornecedor trabalhar junto para produzir um ERS de qualidade, elaborada durante o desenvolvimento do software (Antes, Durante e na finalização), Protótipos pode ser usados para elicitar (dar clareza) para os requisitos 

>[!quote] Professor
>Muito mais fácil alterar um documento de requisito do que toda uma estrutura de um software que ja foi elaborado.
## Questões Básicas
Todas as informações necessárias para que o software possa se desenvolvido
- **Funcionalidade** - O que o software pretender fazer?
- **Interfaces Externas** - Todas as interações do software com elementos externos por exemplo pessoas, hardware do sistema, outros hardwares e outros softwares
- **Desempenho** - Qual o desempenho que se espera do software, velocidades entre outros.
- **Atributos** - Quais são as considerações sobre portabilidade, manutenibilidade, segurança, entre outros
- **Restrições impostas em uma implementação** - Politicas de bancos de dados, Padrões, linguagem de programação, limitação de recursos, ambientes operacionais entre outros.
>[!note] Estrutura da ERS
>1. Introdução
>	1.1 Objetivo
>	1.2 Escopo
>	1.3 Definições, siglas e abreviações
>	1.4 Referências
>	1.5 Visão Geral
>2. Descrição Geral do Produto
>	2.1 Perspectiva do Produto
>	2.2 Funções do produto
>	2.3 Características do Usuário
>	2.4 Restrições, Suposições e dependências
>	2.5 Requisitos Adiados
>	2.6 Estudo de Viabilidade
>3. Apêndices
# Introdução do ERS
Uma descrição do software a ser desenvolvido, contem as seguintes seções
1.1 Objetivo
1.2 Escopo (Claramente registrado as expectativas  de forma macro do que se espera do software)
1.3 Definições, Siglas e Abreviações
1.4 Referências
1.5 Visão Geral
## Objetivo
Explica como funciona a ERS e para que serve, **não da detalhes sobre o software a ser desenvolvido**, especifica o publico alvo.
## Escopo
**Um dos items mais importante da ERS**, começamos a falar sobre o software, o identificando pelo nome (Começa a dar vida ao software), Explica o que o produto de **software  fará** (Requisitos Funcionais) e o que **não fará** (Requisitos Inversos), se for o caso, **Descreve** a **aplicação** do software incluindo **benefícios relvantes** e os **objetivos específicos**
>[!example] Exemplo de Escopo
O software a ser desenvolvido receberá o nome de ‘IManager’ – Sistema Gerenciador de Imobiliárias e tem como objetivo informatizar internamente o gerenciamento das atividades da imobiliária, como cadastros de imóveis, proprietários e locador, vigência dos contratos e aluguéis, compra e venda de imóveis. 
Para a captação do imóvel (o cadastro do mesmo na imobiliária) é realizada uma avaliação, que pode ser de imóveis para venda ou para locação. A avaliação é feita por engenheiros e arquitetos e é documentada na ficha de “Avaliação para venda” ou “Avaliação para aluguel” aonde são levantados dados como metragens de terreno, área construída, cômodos, quintal etc. Este documento é deixado com o proprietário do imóvel com o valor estimado para o mesmo. Caso o proprietário deseje cadastrar o imóvel na imobiliária para venda ou locação, não é cobrado nem um valor do mesmo, caso contrario, o serviço de avaliação tem um custo variável .  
.....  
O maior benefício que o IManager proporciona consiste em informatizar todos os processos da imobiliária, alimentar a rapidez na obtenção de informações para o melhor atendimento dos cliente, bem como maior controle de todos os imóveis, tanto para venda quanto para locação, e informações quase que  instantâneas sobre o negócio.
## Definições, Siglas e Abreviações
Fornece as definições de termos, siglas e abreviações necessárias para interpretar apropriadamente a ERS
- Podem ser fornecidas por referências a apêndices na ERS ou a outros documentos

| Sigla     | Descrição                                                |
| --------- | -------------------------------------------------------- |
| ERS       | Especificação e requisitos de software                   |
| Help Desk | Equipe de suporte ao sistema de Tecnologia da Informação |
| Backup    | Realizar cópia  de segurança dos dados da empresa                                                         |
## Referências
- Lista completa de todos os documentos referenciados
- Identificar cada documento por título, n⁰, Data, Entre outros
- Especificar as origens da referências (quem forneceu)
	- Os documentos referenciados devem estar em um Anexo

| Título     | Origem                               | Autor        | Data       |
| ---------- | ------------------------------------ | ------------ | ---------- |
| Modelo ERS | Fundamento da Engenharia de Software | Alisson Kuhn | 27/06/2021 |
## Visão Geral
- Descrever o que conterá a ERS, dali para baixo
- Explicar como a ERS estará organizada, **não esta relacionado as funcionalidades do software, e sim quais informações ele ira encontrar**
>[!example] Exemplo
>Este documento está́ organizado em capítulos, sendo que os  
capítulos posteriores trataram de expor os requisitos de sistema. No Capítulo 2 é apresentada uma descrição geral do produto, contendo as perspectivas do mesmo, suas funções, características do usuário, restrições, dependências e suposições a serem consideradas no desenvolvimento e implantação do sistema e os requisitos a serem adiados.
# Descrição Geral do Produto
Onde encontraremos o detalhamento geral de cada funcionalidade, descrição geral, mas não requisitos específicos, fornece um background para esses requisitos (que são detalhados na seção 3)
2.1 Perspectiva do Produto (Requisitos não funcionais)
2.2 Funções do Produto (Requisitos)
2.3 Características do Usuário
2.4 Restrições Suposições e Dependências 
2.5 Requisitos Adiados
2.6 Estudo de Viabilidade
## Perspectiva do Produto
De maneira **resumida**, de forma **textual**, sem detalhamento, aproximadamente ½ página, pois trata-se de uma **descrição geral**, não é obrigatório conter todos, apenas o que for necessário para o processo de desenvolvimento de software.
- As **interfaces** mencionadas nessa seção serão detalhadas na seção "Requisitos  de Interface Externa"
- O Produto é colocado em perspectiva com outros produtos relacionados, **podendo** incluir
	- **Interfaces de Sistema** - Com quais outros sistemas o produto de software interage (se houver)
	- **Interfaces do usuário** - Formatos de telas, relatórios ou consulta, formatos de mensagens, acesso por níveis de usuário
	- **Interfaces de Hardware** - Com o o produto interage com os dispositivos de hardware; características de configuração
	- **Interfaces de Software** - Deve especificar o uso de outros softwares necessários (BD, SO, software p/ capturar imagem, entre outros)
	- **Interfaces de Comunicação** - Especificar os protocolos de redes locais, protocolos de comunicação para sistemas multicamadas, entre outros
	- **Limites de Memória** - Especificar os protocolos de rede locais, protocolos de comunicação para sistemas multicamadas, entre outros
	- **Operações** - Deve especificar requisitos de operações normais e especiais como rotinas de inicialização (definir os níveis de acesso), processamento, backup's e restauração
	- **Requisitos para adaptação de Situação** - Especificar situações em que o software deve ser adaptado antes da instalação (qualquer sequencia de inicialização)
## Funções do Produto
**Seção mais importante do capitulo**, são descritas todas as funções do produto,  trás o detalhamento do requisito que foi detalhado no capitulo 1, mais especificamente no escopo, para cada **função, devem ser descritos:**
- Os itens de entrada (dados/informação) necessário
- As regras de negócio
- Os itens de saída necessários
### Essas funções são classificas em:
Entre parenteses a cicla utilizada para enumerar cada tipo de função substituindo "n⁰".
- **Funções Básicas (RF_Bn⁰):** Referem-se às **operações CRUD** (Create, Read, Update, Delete) necessária para a execução das funções fundamentais. Esse conjunto de operações pode ser denominado "Gerenciar"
	- Normalmente Cadastros Básicos, cadastros de roupas, de clientes, tabela de preço
- **Funções Fundamentas (RF_Fn°):** Referem-se às **transações de negócio** (movimentações)
	- Processos que a empresa possui, por exemplo processo de vender, pedidos, lançar nota fiscal
- **Funções de Saída (RF_Sn⁰):** Referem-se às funções geram **informações de saída** relevantes para atender às necessidades do cliente (consultas/relatórios com cruzamento de informações). Devem ser descritos os itens de entrada (filtros) e os itens de saída (informação) pertinentes
	- Relatórios, funções que pretender extrair informação do sistema.
	
>[!note] Observação
>Cada função necessita de uma **identificação** onde a mesma servira como facilitador para a **rastreabilidade** desse requisito, não é obrigatório, porem e muito interessante e **facilitara** bastante utilizar esse padrão.
>As funções de gerenciamento do usuário, backup e restauração do sistema não serão citadas aqui, uma vez que já foram descritas no item "Perspectiva do Produto"
### Exemplos
- **RF_B01** – **Gerenciar** Cliente: O usuário poderá inserir, consultar, alterar e excluir os dados do cliente. Itens de informação obrigatório: nome, RG, CPF, e-mail. Itens de informação opcional: endereço, bairro, CEP, cidade, estado e telefone. O sistema devera validar se o CPF é valido, verificar se o cliente já está cadastrado na base de dados, verificar se o e-mail informado e válido. Ao ser informado o CEP, o sistema deverá realizar a busca das informações correspondentes no serviço on-line do correio e preencher automaticamente as informações do cadastro.
	- "Gerenciar" - Realizar todas a funções do CRUD.
- **RF_F01** – Fechar ordem de serviço: Esta função tem como finalidade fechar uma ordem de serviço e emitir as parcelas de pagamento quando houver. Ainda poderá́ ocorrer o cancelamento do pedido. Para isso, o cliente deverá pagar uma taxa sobre o valor total da OS. Itens de informação obrigatórios: data de abertura, status, data de fechamento, prazo e código da OS. A data de fechamento não poderá ser superior ao dia atual ou inferir a 120 dias da data atual.
- **RF_S03** – Emitir Relatório de Vendas: O usuário poderá emitir um relatório de vendas informando o período e o vendedor. O relatório exibirá os detalhes de cada venda e o total por período. Itens de informação: código do vendedor, nome do cliente, data da venda, total por venda e total por período.
>[!info] Analisando
>Podemos perceber que a estrutura é a mesma.
## Características do Usuário
Descrever o nível educacional dos usuários do sistema, bem como a sua experiência e o conhecimento sobre informática para que seja diagnosticado a necessidade de treinamento específico.
### Exemplo
| Ordem | Cargo  | Frequência de Uso | Nível de Instrução | Proficiência na Aplicação | Proficiência em Informática |
| ----- | ------ | ----------------- | ------------------ | ------------------------- | --------------------------- |
| 1     | Médico | Diário            | Superior           | Alta/Média/Baixa          | Alta/Média/Baixa            |
| 1     | Médico | Diário            | Superior           | Baixo                     | Baixa                            |

## Restrições, Suposições e Dependências
Deve fornecer uma descrição geral de qualquer outro item que limitará as opções do desenvolvedor
- Exemplo: Normas, Reguladoras, Limitações do hardware, Interfaces com outras aplicações, Linguagem de Programação, Protocolos, Protocolos, Requisitos de Segurança entre outros.
Deve fornecer uma lista de fatores que afetam os requisitos expressos na ERS, Exemplo:
- O limite para que um certo sistema não tenha sua funcionalidade completa seria a não aquisição do ponto eletrônico
- A suposição é de que será adquirido o ponto eletrônico
- O desempenho total do sistema depende da satisfação dessa suposição, pois a não aquisição do ponto eletrônico fará com que a entrada de dados seja feita manualmente, inserindo somente as exceções do ponto diário, ou seja, a falta dos funcionários.
##  Requisitos Adiados
Identificar , dentre os requisitos especificados anteriormente, os que podem ser adiados até as versões futuras do sistema.
## Estudo de Viabilidade
Destacar uma topologia "macro" da rede de computadores e equipamento de tecnologia que serão utilizados no projeto, bem como o custo de cada equipamento, Diagramas, Tabelas de preços