# Aula 1
Os 3 subsistemas principais, ligados por barramentos  de comunicação
![[Pasted image 20230429123202.png]]
Independente da arquitetura ou device, estão presentes..

## CPU
CPU (_Central Processing Unit_) em português UCP Unidade central de Processamento., tem como função controlar e executar instruções presentes na memória principal.

### Composição
- UC (Unidade de controle) - Gerencia as atividades de todos os componentes do computador
- ULA (Unidade de lógica e Aritmética) - Responsável por testes de comparação, somas e subtração e derivando destas operações consegui executar todas.
- Registradores - Armazenam temporariamente dados relacionados a execução das instruções.
	- Contador de Instruções  CI- Endereço da próxima instrução que deve buscar e executar
	- Apontador de Pilha  AP - Qual o endereço do topo da pilha. 
	- Registrador de instruções RI - Armazena a instrução que será codificada e executada.
	- Registrador de Status RS - Armazena a informação sobrea a execução de instruções ele indica se a instrução já foi executada  e seu status

### Cilho de Busca
- Clico de busca:
- Processador busca na memória principal a instrução armazenada no endereço indicado pelo Cl e armazena no RI;
- Processador incrementa o Cl para que o registrador contenha o endereço da próxima instrução;
- Processador decodifica a instrução armazenada no RI;
- Processador busca os operandos na memória, se houver;
- -Processador executa a instrução decodificada;
Após este último passo, o ciclo é reiniciado.

### Pipelining
Técnica que permita que o processador execute múltiplas instruções paralelamente em estágios diferentes, uma tarefa é dividida em uma sequência de subtarefas.

### RISC e CISC
Cada arquitetura de processador possui uma linguagem de máquina.
- Processadores com arquitetura RISC (Reduced Instruction Set Computer)possuem poucas instruções de máquinas, são mais simples e exigem umnúmero maior de registradores (ARM, AVR Arduino, Apple Ml);
- Processadores com arquitetura CISC (Complex Instruction Set Computers)possuem instruções complexas que são interpretadas pormicroprogramas, número de registradores pequenos e pipelining complexo (Intel e AMD).
![[Pasted image 20230429132414.png]]

## Memória
Temos diferentes tipos de memorias e funcionamento se baseando da capacidade de armazenar informação com e sem energia, no funcionamentos temos as
 - Voláteis - RAM
 - Não volátil - ROM, EEPROM
Quanto mais rápida a memória, menor sua capacidade.
![[Pasted image 20230429130018.png]]

### Memória Principal
- Onde é armazena as instruções e dados (Programas, documentos, músicas, vídeos. entre outros)
- Composta por unidades de acesso chamadas células, cada célula possui um determinado número e bits.
- 1 Byte = 8 bits que 2^8 é igual a 256, ou seja, 256 possíveis combinações. 

### Memória Cache
- Memória volátil de alta velocidade com pequena capacidade de armazenamento.
- Seu proposito é diminuir a diferença de velocidade no qual o processador executa uma instrução e a velocidade de leitura/gravação de uma nova instrução ou dado da memória principal.
- Presente dentro do processador
- É separada em níveis sendo o L1 o mais rápido e com menos capacidade de armazenamento, seguindo esta lógica até o L3

### Memória Secundária
- Memória não volátil, ou seja, mantem os dados mesmo sem energia, é o HD, SSD, Pendrives, CD, DVD.
- Acesso lento aos dados, porem grande armazenamento.
 ![[Pasted image 20230429130815.png]]
## Dispositivos de Entrada/Saida
- Permita a comunicação entre o sistema computacional e o mundo externo
- São divididos em duas categorias
	- Utilizados como memória secundária
		- HDs, SSDs e Pendrives
		- CDs e DVDs
		- Fitas magnéticas
	- Utilizados como interface usuário máquina
		- Teclado e Mouse
		- Monitor e Caixa de Som
		- Webcam e Microfone
		- Impressora e Scanners

## Barramento
- Barramento ou Bus é o meio de comunicação compartilha que permita a troce de informações entre unidades funcionais do sistema computacional
- O barramentos possui **linhas de controle** e **linhas de dados**
- Existem **3 tipos de barramentos**
	- Barramentos processador memória: Curta extensão e alta velocidade
	- Barramento de entrada/saída: Maior extensão, mais lentos e permita  a conexão de diferentes dispositivos
	- Barramentos  de blackplane: existentes em algumas arquiteturas, possui a função de conectar o barramentos de E/S ao barramento processador memória
![[Pasted image 20230429131708.png]]

# Aula 2
![[Pasted image 20230429141802.png]]
- Sistemas fortemente acoplados
	- Dois processadores, dividindo os mesmo recursos, acoplados fisicamente na mesma placa mãe, expansão de recursos cara, maior confiabilidades
	![[Pasted image 20230429142453.png]]
- Sistemas fracamente acoplados
	- Computadores acoplados por rede, técnica chama da clustes, expansão de recursos barato, menor confiabilidades.
![[Pasted image 20230429142459.png]]

#  Aula 3
- Transmissor -> Canal de Comunicação -> Receptor
- **Classificação das redes:**
	- **PAN** - Personal Area Network: interliga dispositivos de uma pessoa como mouse, fones de ouvidos e impressoras (USB e Bluetooth);
	- **LAN **- Local Area Network: interliga dispositivos locais de uma mesma casa ou de um mesmo prédio, em uma mesma empresa;
	- **MAN**  - Metropolitan Area Network: interliga redes LANs dentro deuma cidade, um exemplo seria a rede da sua provedora de internet;
	- **WAN** - Wide Area Network: as redes distribuídas interliga dispositivos geograficamente distantes, dando origem a Internet.
- Protocolos para comunicação tem um padrão que os dispositivos usam para  conseguir se comunicar.
- Cada protocolo está associado a uma camada de modelo de referência
- Cada camada defini limites e responsabilidades de atuação aos protocolos, gerados interoperabilidade entre tipos, marcas e arquiteturas de sistemas computacionais diferentes.
- O modelo OSI (Reference Model for Open System Interconnection) foi definido em 1970 pela ISO (International Organization Standardization);
- O modelo OSI previa 7 complexas camadas, o que não colaborou para o seu sucesso;
-  Na mesma época o Modelo Internet, também conhecido como
- Modelo TCP/IP previa 4 camadas, era mais simples e privilegiava os protocolos ao invés da arquitetura de camadas de rede;
- Desta forma o Modelo Internet é amplamente utilizado até os dias de hoje.
![[Pasted image 20230429154633.png]]

## Camada física
- Está ligada ao meio físico de transmissão;
- Cabo ethernet IEEE 802.3, WiFi IEEE 802.11;
## Camada de enlace
- Garante a qualidade do que é transmitido no meio físico;
- Prove mecanismos de controle de acesso a rede;
- No modelo internet a camada física e de enlace são tratadas pelos mesmos protocolos;
- Por exemplo: cabo ethernet IEEE 802.3, Wifi IEEE 802.11;
## Camada de rede
- Permite a comunicação entre dispositivos não adjacentes, através de intermediários, comutadores de pacotes;
- O protocolo IP fornece um endereço único para cada dispositivo.
## Camada de transporte
- Enquanto a camada de rede tem a função de encaminhar os pacotes, a camada de transporte é responsável pela comunicação fim a fim entre o transmissor e receptor;
- A camada de transporte permite que transmissor e receptor conectem-se como se estivessem ligados diretamente um ao outro;
- TCP e IJDP são os protocolos da camada de transporte;
## Camada de aplicação
- É a camada mais próxima do usuário e das aplicações;
- Cada serviço de rede/aplicação possui um protocolo capaz de definir a sua atuação;
- HTTP, HTTPS, FTP, SMTP, POP3, IMAP, SSH.

![[Pasted image 20230429155032.png]]

## TCP e UDP
Ligados a camada de transporte
- TCP é orientado a conexão
	- Transmissor e receptor precisam estar  de acordo "handshake" antes da transmissão
	- Garantia de entrega de pacote através de controle de erro e controle de fluxo
	- Mais seguro e mais lento (upload de anexo de e-mail)
	![[Pasted image 20230429161914.png]]

- UDP não é orientado a conexão
	- As transmissões se iniciam aleatoriamente
	- Sem garantia de entrega de pacote, sem controle de erro e sem controle de fluxo
	- Mais inseguro e mais rápido (ligação de áudio)
	![[Pasted image 20230429161924.png]]

## Protocolo de Apresentação e Transporte
![[Pasted image 20230429162044.png]]

## Portas e Sockets
Para haver a comunicação entre maquinas é necessário portas e sockets onde os mesmos são gerenciados pelo sistema operacional
Com o IP identificamos a maquina e com a porta qual aplicação recebera os dados

## Modelos de Comunicação
Principais modelos de comunicação das arquiteturas em sistemas de internet
- Modelo cliente-Servidor
- Modelo Peer-to-peer (P2P)

### Cliente Servidor
- Recursos compartilhados
- Programa cliente é simples, não requerendo privilégios especiais.
- Modelo baseado em mensagens (**request/response**)
- Independência de plataforma
- Servidor desempenho maior parcela do processamento
- Servidores requerem privilégio do sistema operacional, pois, utilizam portas dos protocolos TCP/IP
- Servidores devem lidar com a concorrência
- **Exemplos:**
	- Arquivos
	- Banco de Dados
	- Aplicação
	- Mensagens
	- Nome (DNS)
	- E-Mail
	- Web (Apache, IIS,  Nginx)

### Peer to Peer
Hora é cliente hora é servidor, trabalhar com o compartilhamento muito famosos com  o advento de aplicações como Naspter, Gnutella, eMule, Torrent, entre outros. porem tem seu uso profissional em sistemas de processamento de imagens, modelagem financeira, bioinformática entre outros.
- Informações não estão concentradas em um único servidor
- Informação distribuída entre diversos nós ou parceiros que compartilham informação
- Conexão direta podem ser estabelecidas entre parceiros
- Modelo direcionado a atender comunidades ou grupos com número elevado de parceiros

# Aula 4
- **Processo é um programa em execução**
	- Programa entidade passiva, processo entidade ativa
	- Precisa de recursos para realizar as tarefas, CPU, RAM ,Entrada e Saída, dados de inicialização
	- No termino devolve os recursos reutilizáveis como memoria RAM, um não reutilizável é um arquivo gerado no HD ou SSD
- Eventos que permitem **criação de processos**
	- Início do sistema operacional
	- Execução de uma chama de sistema de criação de processo pro um processo em execução
	- Um requisição do usuário para criar um novo processo
	- Início de uma tarefa em lote (batch)
 - O término de um processo pode ocorrer  das seguintes formas
	 - Saída normal (voluntário)
		- `exit` (UNIX), 	`ExitProcess` (Windows)
	- Saída por erro (voluntária)
		- Arquivo de entrada inexistente
	- Erro fatal (involuntário)
		- Erro do programa
	- Cancelamento por outro processo (involutário)
		- `kill`  (UNIX), `TerminateProcess` (Windows)

## Classificação do processos em relação a Estrada e Saída
	![[Pasted image 20230502213143.png]]
## Estados do Processo
- Processos passam por conjuntos de estados
- Time Sharing (Compartilhamento do tempo) interromper e continuar depois o processo, temos a impresso que esta tudo acontecendo ao mesmo tempo porem não é
- Estados
	- Em execução - Realmente usando a CPU naquele instante
	- Pronto - Temporariamente parado para dar lugar a outro processo
	- Bloqueado - Incapaz de executar enquanto não ocorrer um evento externo de E/S
	![[Pasted image 20230502214017.png]]
### Outra Forma de Enxergar
	![[Pasted image 20230502214154.png]]

## Process Control Block (PCB) 
- Bloco de controle do processo (PCB) é a representação do processo no sistema operacional
- Conjunto de informações associadas a cada processo, repositório de informações do processo
- Conteúdo da PCB
	- Estado do processo
	- Contador de programa
	- Registradores do UCP
	- Escalonamento de UCP
	- Gerenciamento de memória
	- Registros de contabilidade
	- Status de E/S
	- Código do programa
	- Pilha de dados
	- Seção de dados
	- Pilha de _heap_
	![[Pasted image 20230502214642.png]]
## Troca de Contexto
- A troca de contexto acontece a cada mudança de estado do processo (Pronto --> Executando, Executando --> Pronto, Executando --> Bloqueado)
- O contexto é presentado no PCB do processo
- A cada troca é necessário salvar as variáveis atuais do processo e restaurar as variáveis do próximo processo a  ser executado
- O tempo de troca de contexto causa overhead no processamento, ou seja, o sistema não realiza trabalho útil enquanto realiza a troca
- Este tempo de troca depende do suporte do hardware (UCP, Memória e Barramentos)
![[Pasted image 20230502215101.png]]

## Leitura 1
-  A gerência de processos é uma das principais funções de um sistema operacional, possibilitando aos programas alocar recursos, compartilhar dados, trocar informações e sincronizar suas execuções.
- O processador é projetado para executar instruções a partir do ciclo de busca e execução.
- O conceito de processo pode ser definido como sendo o conjunto necessário de informações para que o sistema operacional implemente a concorrência de programas

## Criando Processos
- Qual o objetivo do sistema multitarefa?
	- Ter mais de um processo na memória RAM;
- Qual o objetivo do compartilhamento de tempo?
	- Alternar a UCP entre os processos com muita frequência, para que os usuários interajam com cada programa em execução;
- Resultado
	- Em um sistema com um único processador nunca haverá mais do que um processo em execução, mas a sensação do usuário é que existem vários processos executando simultaneamente!

## Filas
- Fila de tarefas
	- Conjunto de todos os processos no sistema;
- Fila de prontos
	- Conjunto de todos os processos residindo na memória principal, prontos e esperando para executar
- Filas de dispositivos
	- Conjunto de processos esperando por um dispositivo de E/s.

## Tipos de Escalonadores
- Processos estão migrando entre as diversas filas;
- Os escalonadores controlam as migrações;
- Escalonador de longo prazo;
	- Seleciona qual processo deve ser trazido para a fila de prontos;
	- Invocado com baixa frequência, lento (segundos, minutos);
- Escalonador de curto prazo;
	- Seleciona qual processo deve ser executado em seguida e aloca na CPU;
	- Invocado com muita frequência, rápido (milissegundos);
- Escalonador de meio termo;
	- Seleciona qual processo deve ser removido da memória e da disputa pela UCP e salvo na memória secundária (disco);
	 - Esse esquema é chamado de swapping.

## Tipos de Processo
- Processo CPU-bound;
	- Processo que gasta mais tempo realizando cálculos;
- Processo 1/0-bound;
	- Processo que gasta mais tempo com E/S.

## Manipulando Processos no UNIX
![[Pasted image 20230503215337.png]]
![[Pasted image 20230503215349.png]]

## Manipulando Processos no Windows
![[Pasted image 20230503215445.png]]

## Termino do Processo
- Após executar a ultima instrução o processo "pede" para ser excluído (`exit`)
	- Dados de saída comunicado ao pai via `wait`
	- Recursos do processo são deslocados pelo sistema operacional
- Processo pai pode terminar a execução dos processos-filho (`abort`)
	- Processo-filho excedeu recursos alocados
	- Tarefa atribuída ao processo-filho não é mais necessária
	- Se o processo-pai estiver saindo
		- Alguns sistemas operacionais não permitem que o processo filho continue se o processo-pai terminar: término em cascata conduzido pelo SO.

# Aula 5
- Unidade básica de utilização de CPU
- São subdivisões de um processo que podem executar concorrentemente
	- São chamados de **"Processos leves"**
- São compostos por um ID de thread, um contador de programa, um conjunto de registradores e uma pilha
- Compartilha com outros threads
	- Seção de código, seção de dados e outros recursos pertencentes ao mesmo processo.
- Um novo processe é mais custoso por precisa montar um PCB nova e toda sua estrutura.
![[Pasted image 20230506153445.png]]
- Praticamente todo software é multithread
- Threads **mesmo contexto de software porem de hardware não**

## Benefícios
- Capacidade de resposta
	- Permite que um programa interativo continue sendo executado mesmo que parte dele esteja bloqueada ou executando uma operação demorada;
- Compartilhamento de recursos
- Os threads podem se comunicar através de variáveis globais, enquanto os processos necessitam de auxílio do sistema operacional para realizarem essa comunicação;
- Economia
	- A criação de threads é menos custosa em relação a criação de processos. No Solaris, velocidade de criação de 30x1, velocidade de troca de contexto de 5x1;
- Escalabilidade
	- Permite a execução de um processo em múltiplos processadores.
## Suporte
O thread de usuário precisa encontrar suporte em um thread de kernel (do Sistema Operacional) para ser executado;

- Em sistemas operacionais que implementam o modelo de suporte Muitos-para-um, muitos threads em nível de usuário são mapeados para um único thread de kernel;
- A desvantagem desse modelo é que se um único thread realizar uma chamada bloqueadora, todo o processo será bloqueado.

![[Pasted image 20230506154235.png]]

- Em sistemas operacionais que implementam o modelo Um-para-Um mapeia-se cada thread de usuário para uma thread de kernel;
- Permite uma maior concorrência entre as threads;
- Caso um thread faça uma chamada bloqueante o processo não será bloqueado por completo;
- Desvantagem está na necessidade de que para cada thread de usuário exista uma thread de kernel;
- Restrição do número de threads suportado pelo sistema;
- Linux e Windows.
![[Pasted image 20230506154614.png]]

- Em sistemas operacionais que implementam o modelo Muitos-para-Muitos multiplexa-se muitos thread de usuário um número menor ou igual de threads de kernel;
- O número de threads de kernel pode ser específico para determinada aplicação ou máquina; thread de Usuário
- Possibilidade de criação de threads ilimitadas;
- Não implementa concorrência real, pois o sistema operacional pode incluir na fila de execução apenas uma thread por vez.
 ![[Pasted image 20230506161935.png]]

- Fornecem ao programador uma API (Application Program Interface) para criação e gerenciamento de threads;
- Técnicas de implementação da biblioteca;
	- Biblioteca inteiramente no espaço do usuário, sem suporte do kernel;
		- Chamada da função local no espaço do usuário;
	- Biblioteca no nível do kernel, com suporte direto do sistema operacional;
		- Todas as estruturas estão no espaço do kernel.

## Biblioteca PTHREADS
- PTHREASDS é uma API baseada no padrão POSIX (IEEE 1003.1c);
- O padrão POSIX é adotado por sistemas baseados em UNIX (Solaris, Linux e MacOs);
- Pode ser fornecida como biblioteca no nível do usuário e no nível do kernel;
- Possui certa de 100 rotinas que manipulam threads, as funções são prefixadas por "pthread—";
- Existe uma variação da PTHREADS para o Windows (PTHREADS-WlN32).
![[Pasted image 20230506165359.png]]

## Biblioteca WIN32
-  implementação de THREADS no Windows é realizada pela biblioteca WIN32 API;
- Suporte 16, 32 e 64 bits;
- Além do suporte a criação de threads a WIN32 API também suporta as seguinte funcionalidades;
	- Serviços básicos: sistema de arquivo, threads, processos, entre outros;
	- Serviços avançados: registros, desligar/reiniciar, entre outros;
	- Interface gráfica e caixas de diálogo;
	- Serviços de rede como Winsock, RPC, entre outros.

## Biblioteca Threading no Python
- Threading API é a biblioteca em Python que suporta a criação dos Threads;
- Como Python é multiplataforma, a biblioteca serve em todos os sistemas operacionais que suportam Python.
 ![[Pasted image 20230506170815.png]]

- A ordem dos resultados muda por causa da concorrência.

# Aula 6

## Comunicação Entre Processos
- Processos independentes
	- São aqueles que não compartilham dados com outros processos;
	- Não afeta e nem pode ser afetado por outro processo.
- Processos cooperativos
	- Podem afetar outros processo em execução;
	- Permitem compartilhamento de informações;
	- Usufruem de agilidade na computação através da subdivisão de tarefas;
	- Modularidade com funções em processos separados.

- Existem duas formas de realizar a comunicação entre processos:
	- Memória compartilhada (Os processos no mesmo computador)
	- Passagem de mensagem (podem estar distantes)

![[Pasted image 20230507122551.png]]

## Memória Compartilhada
- Área comum na memória que pode ser acessada por dois processos para comunicação entre eles;
- Operações de escrita e leitura;
- Maior velocidade na comunicação, não há intermediários;
- Menos seguro;
- O formato e o local dos dados são determinados pelos processos envolvidos;
- Os processos devem garantir a proteção de escrita;
- Disponível apenas na memória local do computador;
- Implementação mais complexa.
![[Pasted image 20230507122754.png]]

## Passagem de Mensagem
- Utiliza o suporte do sistema operacional para troca de mensagens através de um protocolo;
- As operações necessitam de enlace
	- send(mensagem);
	- receive(mensagem)
- Útil para quantidades menores de dados, pois não há conflitos;
- Disponível tanto no ambiente local quanto em ambientes distribuídos;
- Os processos não precisam se preocupar com os enlaces de comunicação, todas as tratativas ficam por conta do Sistema Operacional;
- Implementação mais simples.
- **Comunicação direta**
	- Transmissão de dados explicitamente nomeadas;
	- send(ProcessoA, mensagem);
	- receive(ProcessoB, mensagem);
- **Comunicação indireta** (Internet)
	- Transmissão de dados através de caixas de correio ou portas;
	- Cada porta tem um identificador exclusivo;
	- send(portaA, mensagem);
	- receive(portaA, mensagem);
	- Proprietário da porta;
		- Pode ser o processo;
		- Pode ser o SO;
	- Suporte do SO para criação de nova porta, destruição da porta. envio e recepção e destruição de porta

## Modelos de Passagem de Mensagem
- A passagem de mensagens no modelo cliente-servidor pode ser realizada de duas formas
	- Socket;
	- RPC (Remote Procedure Call);
	- VVebServices.

## Socket

- O socket é uma API (Application Programming Interface) fornecida pelo Sistema Operacional para implementar uma extremidade de comunicação;
- Um socket é identificado por um endereço IP concatenado com um número de porta;
- A comunicação acontece entre uma par de sockets e a troca de dados é sem estrutura;
- Estamos na camada de transporte.![[Pasted image 20230507123723.png]]
- Servidor porta fixa, usuário porta sorteada fornecida pelo SO

## Soccket TCP
![[Pasted image 20230507123951.png]]

## Socket  UDP
![[Pasted image 20230507124249.png]]

## RPC (Remote Procedure Call)
- Chamada de Procedimento Remoto
	- Permite o compartilhamento de funções e procedimentos entre processos através da rede de computadores;
- Diferentemente dos Sockets, estamos na camada de apresentação, RPC possui estrutura própria definida;
- O processo cliente realiza uma chamada da função remota passando os parâmetros necessários para sua execução. A função é executada no servidor e devolve apenas os resultados da execução para o processo cliente;
- Implementações:
	- CORBA
	- SunRPC
	- DCOM
	- SOAP
	- RMI
![[Pasted image 20230507125239.png]]

![[Pasted image 20230507125352.png]]

## Sincronismo
- Processos podem executar concorrentemente
	- Podendo ser interrompidos a qualquer momento
- Acessos concorrentes a dados compartilhados pode resultar em dados inconsistentes;
- Manter a consistência de dados requer mecanismos para garantir a ordem de execução de cooperação entre processos;
- Problema do consumidor-produtor, compartilhando um buffer;
- Contador inteiro que indica o tamanho do buffer;
	- Incrementado pelo produtor;
	- Decrementado pelo consumidor.

## Problema de Seção Critica
- Seção Crítica
	- Código acessando recursos compartilhados eção Restante (remanescente)
- Seção Restante (remanescente)
	- Código acessando recursos exclusivos
- Seção de Entrada
	- Código que permite a entrada na seção crítica
- Seção de Saída
	- Código executado após a saída da seção relacionada ao acesso a seção crítica crítica

## Estrita Alternancia
Um executa de cada vez, porem pode haver problemas caso a diferença de velocidade for grande
![[Pasted image 20230507132017.png]]

## Semaforos
- onhecer rapidamente a Solução de Peterson, que visa permitir que os processos progridam;
- Mesmo isolando a região crítica que seria a variável compartilhada, nós criamos um novo problema;
- Compartilhamos uma nova variável: turn;
- Corremos o risco de mais uma vez gerar dados inconsistentes;
- A solução está no **Sistema Operacional**, Semáfaros
- Ferramenta de sincronização que (Sistema Operacional) para que os atividades;
- Só pode ser acessado através de controladas pelo Sistema Operacional; 
- Uso do semáforo:![[Pasted image 20230507132528.png]]

# Aula 7
- Escalonadores de CPU são os responsáveis por dar a sensação de esta realizando varias coisas ao mesmo tempo, quando na verdade está havendo uma alternância muito rápida, a ideia é sempre usar o máximo da CPU ![[Pasted image 20230513165402.png]]
- Fila de prontos não é necessário mente uma fila do tipo FIFO first-in first-out.
- Preempção
	- Preemptivos processo interrompido no meio do caminho para dar espaço a outro, depois volta.
		- Dados compartilhados entre dois processos pode gerar estado incoerente (solução: sincronismo)
- Existe diferentes algoritmos para realizar o escalonamento.
- Throughput (Vazão) - Número de processo que completam sua execução por unidade de tempo
- Tempo de Turnaround (tempo de retorno) - Quantidade de tempo para executar um processo em partícula desde o carregamento na memória até o termino da execução.
- Tempo de espera -Todo o tempo em que um processo esteve esperando na fila de prontos. Não contempla espera por E/S
- Tempo de resposta -Tempo desde quando uma solicitação foi submetida até a
primeira resposta

## First-Come, First-Served (FCFS)
- Parecido com um fila FIFO.
- Fácil implementação da pólitica por meio de uma FIFO
	- O PCB do processo que entra na fila de prontos é associado ao final da fila
	- A CPU é alocada ao processo cujo PCB está na cabeça da fila
- Não-preemptivo
- O tempo médio de espera geralmente não é mínimo
	- Depende dos tempos de burst do processo.

### Exemplo
| Processo | Tempo de Burst |
| -------- | -------------- |
| P1       | 24             |
| P2       | 3              |
| P3       | 3              |

- Supondo que os processos cheguem  nesta ordem: P1, P2, P3
- Diagrama de Gantt ![[Pasted image 20230513171739.png]]
- Tempo de espera para P1=0; P2=24; P3=27
- Tempo de espera média: (0 + 24 + 27)/3 = 17

### Exemplo 2
- Mesmo dados porem chegada de processos diferente: P2, P3 e P1 ![[Pasted image 20230513172056.png]]
- Tempo de espera para P1=6; P2=0; P3=3
- Tempo de espera média: (6 + 0 + 3)/3 = 3
- Muito melhor que o caso anterior
- **Efeito comboio** - Processo curto atrás de processo longo
	- Um processo CPU-bound, vários processos I/O bound
	- Solução: Priorizar processos I/O bound no uso de CPU

### Exercício
| Processo | Tempo de Burst |
| -------- | -------------- |
| P1       | 5              |
| P2       | 10             |
| P3       | 3              |
| P4       | 15               |

![[Arqutetura, sistemas operacionais e rede de computadores 2023-05-13 17.25.38.excalidraw|center]]

## Shortest Job First (SJF)
- Não preemptivo
- Organiza a fila de chegada pelo tamanho do busrt
- Burst menores tem prioridade na execução

### Exemplo

| Processo | Tempo de Burst |
| -------- | -------------- |
| P1       | 6              |
| P2       | 8              |
| P3       | 7              |
| P4       | 3               |

![[Pasted image 20230513173231.png]]

### Exercício

| Processo | Tempo de Burst | Tempo de Chegada |
| -------- | -------------- | ---------------- |
| P1       | 5              | 0                |
| P2       | 10             | 1                |
| P3       | 3              | 1                |
| P4       | 15             | 2                |
| P5       | 2              | 4                 |

![[Arqutetura, sistemas operacionais e rede de computadores 2023-05-13 17.38.46.excalidraw|center]]

## Shortest-Remaining-Time-First (SRTF)
- Preemptivo
	- Se um novo processo chega com tamanho de burst de CPU menor que o tempo restante do processo atualmente em execução, a troca acontece e a CPU é alocada ao novo processo
 - Os processos vão chegar em tempos diferentes

### Exemplo

| Processo | Tempo de Burst | Tempo de Chegada |
| -------- | -------------- | ---------------- |
| P1       | 8              | 0                |
| P2       | 4              | 1                |
| P3       | 9              | 2                |
| P4       | 5              | 3                 |

![[Pasted image 20230513180307.png]]

- Tempo de médio de espera = ((0  9) + 0 + 15 + 2)/4 = 6.5

### Exercício

| Processo | Tempo de Burst | Tempo de Chegada |
| -------- | -------------- | ---------------- |
| P1       | 10             | 0                |
| P2       | 8              | 1                |
| P3       | 6              | 2                |
| P4       | 4              | 3                 |

![[Arqutetura, sistemas operacionais e rede de computadores 2023-05-13 18.08.03.excalidraw|center]]

## Escalonamento por Prioridade
- Um número inteiro associado a cada processo
- A CPU é alocada ao processo com maior prioridade (menor inteiro =maior prioridade ou maior inteiro = maior prioridade)
	- PtiVO
	- Não-preemptivo
- SJF é um escalonamento por prioridade (ordem de chegada)
- Tipos de prioridades
	- Internamente: uma quantidade mensurável, limites de tempo, memória, número de arquivos abertos, entre outros
	- Externamente: fora do SO, importância do processo, quantidade pago pelo uso da CPU, fatores políticos, entre outros
- Cuidado com o uso da prioridade
- Problema de estagnação (Starvation)
	- Processos com baixa prioridade podem nunca ser executados
	- O IBM 7094 no MIT foi desativado em 1973 e tinha um processo de baixa prioridade submetido em 1967 ainda não executado!
- Solução para a estagnação: Envelhecimento (Aging)
	- Conforme o tempo passa, aumenta-se a prioridade do processo
		- Um processo de prioridade 127 (baixa) chega à prioridade O (alta) em quase 32 horas, se sua prioridade aumentar em 1 a cada 15 minutos

## Round Robin (RR)
- Algoritmo de escalonamento preemptivo
	- Acabou o quantum de tempo, o processo sai de contexo
- Quantum de tempo
	- Define o tempo máximo de uso da CPU por aquele processo (normalmente 10-100 milissegundos)
- Funcionamento
	- Se houver n processos na fila de prontos (circular) e o quantum de tempo q, então cada processo recebe l/n do tempo da CPU em pedaços de no máximo q unidades de tempo de uma só vez
- Desempenho
	- Depende do tamanho do quantum de tempo
	- A troca de contexto pode durar 10 microssegundos
	- 80% dos bursts de CPU devem ser menores que o quantum de tempo

### Exemplo

| Processo | Tempo de Burst |
| -------- | -------------- |
| P1       | 53             |
| P2       | 17             |
| P3       | 68             |
| P4       | 24               |

- Quantum = 20

![[Pasted image 20230513184049.png]]
- Normalmente maior turnaround médio que SJC, porém com resposta melhor

## Fila Multinível
- Divisão da fila de prontos (critério)
	- Primeiro plano (interativo) e segundo plano (batch)
	- Possuem requisitos diferentes para tempo de reposta
	- Memória, prioridade, tipo de processo
- Cada fila tem o seu próprio algoritmo de escalonamento
	- Primeiro plano -RR
	- Segundo plano— FCFS
- Escalonamento entra as filas
	- Escalonamento com prioridade fixa
	- Serve tudo em primeiro plano, depois em segundo plano
	- Possibilidade de estagnação

![[Arqutetura, sistemas operacionais e rede de computadores 2023-05-14 22.12.05.excalidraw]]