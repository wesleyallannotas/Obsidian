---
title: Distrobox como configurar basico
author: Diolinux
url: 'https://diolinux.com.br/tecnologia/configurar-instalar-distrobox.html'
type: article
completed: false
aliases: Distrobox
tags:  [docker, linux]
description: Tutorial basico de utilização do Distrobox
---
# Introdução

O **Distrobox** é uma ferramenta que permite [gerenciar contêineres na sua distribuição](https://diolinux.com.br/editorial/como-containers-dockers-kubernetes-openshift-ajudar-escalabilidade-aplicacoes.html), com os quais você pode **compartilhar** dispositivos removíveis USB, a pasta ou partição HOME do usuário, o áudio, além de soquetes dos ambientes gráficos X11 e Wayland. 

==Contêineres em computação são **ambientes ou espaços totalmente funcionais e independentes**, “recipientes” que envolvem e isolam um aplicativo== (seus processos, configurações, bibliotecas e dependências) ou até mesmo uma distribuição, mas, ==todos eles compartilham o kernel do sistema operacional e o hardware.==

# Para que você usaria o Distrobox?

Com essa versatilidade, o Distrobox permite que você **execute comandos ou aplicativos sem medo** de causar dano ao seu sistema, já que eles estarão “virtualizados” e isolados, especialmente se usar contêineres com acesso não-root.

Uma das utilidades dele é que você pode [instalar um aplicativo](https://diolinux.com.br/aplicativos/melhores-aplicativos-2021.html) que não esteja disponível na sua distribuição. Que tal **instalar um aplicativo do Arch User Repository (AUR) no Fedora ou Ubuntu**? Você não precisa instalar o Arch para isso, pode usar o Distrobox. 

Não tenha mais incompatibilidades entre o seu sistema e um único aplicativo que precisa utilizar, acesse todos os seus arquivos na pasta (ou partição) HOME, como as pastas Documentos e Downloads.

Outro uso interessante é **comparar o desempenho das distros no seu hardware**. Apesar da pequena queda de desempenho por estarem rodando dentro do Distrobox, o impacto deveria semelhante para todas elas. De qualquer forma, saiba que o desempenho de uma distribuição em contêiner é muito superior ao das máquinas virtuais. Você também pode **testar a velocidade dos mirrors das distribuições**.

Quer **compilar um kernel ou uma ROM customizada** para o seu Android? Você não precisa “contaminar” o seu sistema com as dependências necessárias, pode usar um ambiente de desenvolvimento completamente isolado e sem privilégios de root.

Uma imagem vale por mil palavras. Com o Distrobox, você pode ter muitas distribuições dentro da sua, sem sobrecarregar o sistema.

![distrobox um por todos por um](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-um-por-todos-por-um-1024x578.jpg "Distrobox: como configurar e instalar suas primeiras distros 2")

_“Um por todos, todos por um” do Linux._

# Pré-requisitos para instalar o Distrobox

Tecnicamente, ele é um _wrapper_ para contêineres do docker ou podman. Por isso, antes de instalá-lo, você precisa instalar o **docker** (versão 18.06.1 ou superior) ou o **podman** (versão 2.1.0 ou superior) para criar os contêineres. O docker pode permitir acesso root ao sistema host, enquanto o podman fornece apenas acesso não-root ao sistema host.

<iframe loading="lazy" title="O mínimo que você precisa saber sobre Docker!" width="640" height="360" src="https://www.youtube.com/embed/ntbpIfS44Gw?feature=oembed" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen=""></iframe>

Fica um alerta, os contêineres do Distrobox estão intimamente integrados no sistema host, um contêiner com acesso root tem os mesmos privilégios administrativos do usuário root (ou “sudo”) e pode tomar ações que podem ser desastrosas ao seu sistema, caso você não saiba realmente o que está fazendo. Recomendamos o uso de um **contêiner sem acesso root** sempre que possível.

Verifique se os serviços do gerenciador de contêiner escolhido estão sendo executados, ou reinicie o computador. Por exemplo:

```sh
sudo systemctl enable --now docker
```

```sh
sudo systemctl enable --now podman
```

# Instale o Distrobox no Linux

O comando abaixo **baixa um shell script e o executa** com privilégios de superusuário. Na página oficial do projeto, você pode analisar o shell script antes de executá-lo.

```sh
curl https://raw.githubusercontent.com/89luca89/distrobox/main/install | sudo sh
```

Você também pode instalar usando os pacotes da sua própria distribuição (repositório):

-   Alpine (Edge);
-   Arch (AUR);
-   Debian (12/Unstable);
-   Devuan (Unstable);
-   Fedora (34/35/36/Rawhide);
-   Funtoo (1.4);
-   Kali Linux (Rolling);
-   nixpkgs (21.11/22.05/unstable);
-   OpenMandriva (Rolling/Cooker);
-   openSUSE (Tumbleweed);
-   Raspbian (Testing);
-   Ubuntu (kinetic).

# Crie seu primeiro contêiner

Você precisa usar uma imagem para **criar e executar um contêiner** a partir dela. Ele faz isso através do seguinte comando.

```sh
distrobox-create --image [os-image:version] --name [container-name]
```

Se você precisa de acesso root ao sistema, utilize o comando abaixo:

```sh
distrobox-create --root --image [os-image:version] --name [container-name]
```

Nota: não é possível executar comandos no usuário root do anfitrião, ou seja, não é possível usar “sudo” ou “doas” antes dos comandos do Distrobox.

Por exemplo, para criar um contêiner do Fedora Rawhide (a versão de desenvolvimento do Fedora), chamando-o de “fedora-rawhide”, com acesso root:

```sh
distrobox-create --root --image fedora:rawhide --name fedora-rawhide
```

![distrobox create](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-create-1024x173.jpg "Distrobox: como configurar e instalar suas primeiras distros 3")

Se você quiser isolar os arquivos da HOME do contêiner mantendo simultaneamente acesso à HOME do host, pode informar o caminho para a pasta HOME do contêiner através do seguinte comando:

```sh
distrobox-create --root --image fedora:rawhide --name fedora-rawhide --home [caminho-para-home-contêiner]
```

Esses comandos baixam automaticamente a imagem do contêiner contendo a distribuição escolhida, disponibilizando-a para o Distrobox. Caso seja necessário, informe a variável de ambiente DOWNLOAD\_KEYSERVER antes de executar o comando distrobox-create:

```sh
export DOWNLOAD_KEYSERVER="hkp://keyserver.ubuntu.com"
```

Ao final, uma mensagem informa que o contêiner foi criado com sucesso.

Para mais opções, consulte a página do projeto no Github ou execute o comando:

```sh
distrobox --help
```

Você encontra a [lista das distribuições e contêineres](https://github.com/89luca89/distrobox) oficialmente suportados pelo Distrobox ou qualquer imagem OCI disponível, por exemplo, nos repositórios docker-hub e quay.io.

| Distribuição     | Versão                             |
| ---------------- | ---------------------------------- |
| AlmaLinux        | 8; 8-minimal; 9; 9-minimal         |
| Alpine Linux     | 3.14; 3.15                         |
| AmazonLinux      | 2; 2022                            |
| ArchLinux        | latest                             |
| ClearLinux       | latest                             |
| CentoOS          | 7                                  |
| CentOS Stream    | 8; 9                               |
| RedHat (UBI)     | 7; 8; 9                            |
| Debian           | 7; 8; 9; 10; 11; testing; unstable |
| Neurodebian      | nd100                              |
| Fedora           | 34; 35; 36; 37; Rawhide            |
| Mageia           | 8                                  |
| Opensuse         | Leap; Tumbleweed                   |
| Oracle Linux     | 7; 8                               |
| Rocky Linux      | 8                                  |
| Scientific Linux | 8                                  |
| Slakware         | 14.2                               |
| Ubuntu           | 14.04; 16.04; 18.04; 20.04         |
| Kali Linux       | rolling                            |
| Void Linux       | latest                             |


Lista de imagens disponíveis atualmente.

Se quiser uma imagem do **Gentoo Linux**, como era de se esperar, terá de compilá-la e o ele não dá suporte a contêineres do **NixOS**, pelo alto grau de integração com o host. Se você quer utilizar um contêiner no NixOS, será necessário usar o _nix-shell_.

# Acesse um contêiner do Distrobox

Para **acessar o shell de um contêiner**, use o comando:

```sh
distrobox-enter --name [container-name]
```

Ou, para **acessar como root** use o seguinte comando no seu terminal:

```sh
distrobox-enter --root --name [container-name]
```

No exemplo que vínhamos usando, o comando seria:

```sh
distrobox-enter --root --name fedora-rawhide
```

![distrobox enter](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-enter-1024x435.jpg "Distrobox: como configurar e instalar suas primeiras distros 4")

Nesse momento, o Distrobox faz a sua mágica:

-   Instala todas as **dependências** e pacotes básicos;
-   Monta as **partições virtuais**;
-   Faz a **configuração** dos temas, ícones e fontes;    
-   Cria os **grupos** e **usuários**;    
-   Outras modificações necessárias para que você possa rodar a nova distribuição dentro do seu sistema, como a integração dos soquetes e, se for desejado, **habilitação do root** (sudo).

Em geral, o **tamanho das imagens é pequeno**, variando entre 30 e 60 MB, podendo chegar a mais de 100 MB no caso do Mageia. O tempo de configuração inicial varia conforme o poder de processamento do seu computador, a disponibilidade de mirrors dos pacotes da distribuição, mas não deve ser superior a 15 minutos.

Repare que o **shell do host é alterado imediatamente para o shell do contêiner**, passando de _diolinux@arch_ (host) para _diolinux@fedora-rawhide_ (contêiner dentro do distrobox).

# Atualize o contêiner

Você pode **atualizar a imagem do contêiner** de duas formas:

## Usando o próprio Distrobox

A partir do shell do host (_diolinux@arch_), use o seguinte comando para **entrar e atualizar o contêiner**:

```sh
distrobox-enter --root --name [container-name] -- [update-commands]
```

No nosso exemplo, seria:

```sh
distrobox-enter --root --name fedora-rawhide -- sudo dnf upgrade
```

![distrobox atualizacao imagem](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-atualizacao-imagem-1024x338.jpg "Distrobox: como configurar e instalar suas primeiras distros 5")

Prosseguindo com a instalação após responder “y” (yes):

![distrobox atualizacao imagem completa](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-atualizacao-imagem-completa-1024x292.jpg "Distrobox: como configurar e instalar suas primeiras distros 6")

## Usando o shell do contêiner

Entre no shell do contêiner conforme indicado acima (_distrobox-enter –root –name fedora-rawhide_) e execute o **comando de atualização da distribuição** (repare no shell _diolinux@fedora-rawhide_):

```sh
sudo dnf update && sudo dnf upgrade
```

![distrobox atualizacao imagem conteiner](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-atualizacao-imagem-conteiner-1024x210.jpg "Distrobox: como configurar e instalar suas primeiras distros 7")

# Instale aplicativos no contêiner

Agora você já pode executar comandos dentro desse contêiner. No exemplo abaixo, o host é Arch, o contêiner o Fedora Rawhide, podemos instalar e executar o aplicativo _neofetch_ com os comandos abaixo. Repare que, como numa máquina virtual, a distribuição host não importa mais, os **comandos** e o **gerenciador** de pacotes utilizado são os do **contêiner**:

```sh
sudo dnf install neofetch
neofetch
```

![distrobox instalacao neofetch](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-instalacao-neofetch-1024x198.jpg "Distrobox: como configurar e instalar suas primeiras distros 8")

Repare que as imagens usadas nos contêineres são “minimalistas” e, aos instalar os primeiros aplicativos, muitas **dependências** são automaticamente baixadas e instaladas (no nosso caso, 331MB):

![distrobox instalacao neofetch dependencias](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-instalacao-neofetch-dependencias-1024x163.jpg "Distrobox: como configurar e instalar suas primeiras distros 9")

Rodando o neofetch no contêiner:

![distrobox neofetch](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-neofetch-1024x458.jpg "Distrobox: como configurar e instalar suas primeiras distros 10")

# Exporte aplicativos do contêiner para o host

Você também pode **instalar aplicativos gráficos** no contêiner para, por exemplo, usar um host com um ambiente gráfico KDE com aplicativos GTK “exportados”, evitando conflitos de dependências, sem “contaminar” o host. Após **exportar aplicativos instalados no contêiner para o sistema host de forma transparente,** você vai usá-los normalmente, sem nem mesmo perceber que ele está sendo executado dentro do contêiner. Use o comando:

```sh
distrobox-export --app [aplicativo]
```

No nosso exemplo, entrando no contêiner do Fedora, instalando e exportando o Geany para o Arch (a partir do shell do contêiner, _diolinux@fedora-rawhide_):

```sh
sudo dnf install geany
```

![distrobox instalacao geany](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-instalacao-geany-1024x161.jpg "Distrobox: como configurar e instalar suas primeiras distros 11")

Novamente, muitas dependências são necessárias (104MB), mas a cada instalação elas tendem a ser cada vez menos:

![distrobox instalacao geany dependencias](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-instalacao-geany-dependencias-1024x162.jpg "Distrobox: como configurar e instalar suas primeiras distros 12")

Após instalado no contêiner (Fedora), o aplicativo Geany precisa ser exportando para o host (Arch), o que pode ser feito dentro do contêiner, repare no shell _diolinux@fedora-rawhide_:

```sh
distrobox-export --app geany
```

![distrobox exportacao geany](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-exportacao-geany-1024x125.jpg "Distrobox: como configurar e instalar suas primeiras distros 13")

Aguarde alguns instantes para que o Geany apareça no menu de aplicativos da sua distribuição (no nosso caso, Arch com ambiente KDE):

![distrobox geany exportado](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-geany-exportado-938x1024.jpg "Distrobox: como configurar e instalar suas primeiras distros 14")

# Liste os contêineres criados com o Distrobox

Para **listar todos os contêineres** criados com o Distrobox, use o seguinte comando a partir do shell do host (_diolinux@arch_):

```sh
distrobox-list --root
```

![distrobox list](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-list-1024x194.jpg "Distrobox: como configurar e instalar suas primeiras distros 15")

# Saindo do contêiner

Para **sair do contêiner e retornar ao sistema host**, no terminal, digite “**exit**“.

![distrobox exit](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-exit-1024x94.jpg "Distrobox: como configurar e instalar suas primeiras distros 16")

# Removendo um contêiner

Se você não for mais utilizar um contêiner ou se simplesmente deseja **recuperar espaço em disco**, precisará pará-lo e, em seguida, poderá removê-lo por dois comandos:

```sh
distrobox-stop --root --name [container-name]
distrobox-rm --root --name [container-name]
```

Se falhar, pode forçar a remoção:

```sh
distrobox-rm --root --force --name [container-name]
```

No nosso exemplo, a partir do shell do host (_diolinux@arch_), seria:

```sh
distrobox-stop --root --name fedora-rawhide
distrobox-rm --root --name --name fedora-rawhide
```

![distrobox stop delete](https://u5h3z3d7.stackpathcdn.com/wp-content/uploads/2022/09/distrobox-stop-delete-1024x171.jpg "Distrobox: como configurar e instalar suas primeiras distros 17")

# Comandos avançados do Distrobox

Depois que estiver familiarizado com ele, você pode realizar ações mais avançadas como, por exemplo, **clonar um contêiner** através do comando:

```sh
distrobox-create --name fedora-rawhide --clone fedora-rawhide-test
```

A lista completa de comandos está no manual, digite:

```sh
man distrobox
```

# Resolvendo problemas de implantação do Distrobox

Como o Distrobox está integrado no sistema host, podem surgir problemas de implantação. É impossível fazer um guia solucionando todos os possíveis problemas, mas seguem dois que encontrei nas minhas experiências pessoais.

## Erros de acesso

No caso de imagens com acesso root, você pode se deparar com **mensagens de erro de acesso** e talvez seja preciso executar os comandos abaixo como root (ou usando sudo), substituindo \[username\] pelo seu nome de usuário, antes de executar o comando distrobox-create no shell do host (_diolinux@arch_):

```sh
touch /etc/subuid /etc/subgid
if ! grep -q "[username]" /etc/subuid; then echo "[username]:100000:65536" | sudo tee --append /etc/subuid; fi
if ! grep -q "[username]" /etc/subgid; then echo "[username]:100000:65536" | sudo tee --append /etc/subgid; fi
```

## Correção do idioma

Você deve ter reparado que os contêineres acima estavam em inglês, se deseja ver **mensagens em português**, instale e configure os pacotes _locales_ no shell do contêiner. Por exemplo, em um contêiner Ubuntu que você quisesse utilizar para desenvolvimento:

```sh
sudo apt-get install locales
sudo locale-gen pt_BR.UTF-8
sudo update-locale LANG=pt_BR.UTF-8
```

Os comandos acima têm de ser adaptados segundo a distribuição do contêiner.