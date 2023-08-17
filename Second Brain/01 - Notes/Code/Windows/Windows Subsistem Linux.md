---
title: Windows Subsistem Linux
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [windows]
description: WSL2 no Windows
---
# Introdução
O Windows Subsystem for Linux 2 (WSL2) é uma tecnologia desenvolvida pela Microsoft que permite a execução de um ambiente Linux completo diretamente dentro do sistema operacional Windows. Ao contrário do seu antecessor, o WSL, o WSL2 utiliza uma camada de virtualização baseada no kernel do Linux, proporcionando melhor desempenho e compatibilidade com diversas distribuições Linux. Isso permite que desenvolvedores e usuários executem aplicativos e ferramentas Linux de forma integrada com o Windows, facilitando o desenvolvimento cruzado e a utilização de ambientes de desenvolvimento familiares.

>[!tip] Opção do ArchLinux
>Podemos utilizar o Arch Linux dentro do WSL2, não é um suporte oficial porem funciona bem.
>[Como configurar | ArchWSL official documentation (wsldl-pg.github.io)](https://wsldl-pg.github.io/ArchW-docs/locale/pt-BR/How-to-Setup/)

# Configurando o Root
Inicialmente iniciamos logado como usuário `root`, porem sem uma senha, é necessário defini-la, conseguimos isso através do seguinte comando.

```bash
passwd
```

# Criando Usuário
Por padrão nosso Linux no WSL2  vem com o Ubuntu e apenas com o usuário `root`, é necessário configurar as permissões do `sudo` e criar um usuário, em seguida o definir como o usuário padrão.

```bash
echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel
```

Para criar o usuário utilizaremos o comando `useradd` definindo seu `shell` padrão e o adicionando o grupo `whell`

```bash
useradd -m -G wheel -s /bin/bash {usuário}
```

Após criar o usuário é necessário definir uma senha para o mesmo, utilizaremos o mesmo comando utilizado para o `root`, porem passando um usuário especifico agora.

```bash
passwd {usuário}
```

# Definindo Usuário como Padrão
Podemos definir um usuário padrão através do seguinte comando utilizando Arch Linux, basta ir no binário e executar

```bash
./Arch.exe config --default-user {usuário}
```

# Atualizar Sistema
Após as configurações inicias é de extrema importância atualizar o sistema ao máximo, caso esteja utilizando Arch Linux é necessário também inicializar as chaves.

```bash
sudo pacman-key --init

sudo pacman-key --populate

sudo pacman -Syy archlinux-keyring
```

# Mudando Shell Padrão
Hoje em dia é muito comum usuário optarem por outros `shells` além do padrão que é o `bash`, para alterar o `shell` do nosso usuário basicamente podemos alterar o arquivo encontrado no _path_ `/etc/passwd`, ou através do seguinte comando.

```bash
sudo chsh --shell /bin/{shell que deseja} {usuário}
```

# Instalando Docker
Para instalar _Docker_ no nosso WSL2, primeiramente é necessário instalar o _Docker Desktop_ no _Windows_ em seguida nas configurações do mesmo devemos ativar o _Arch_, em seguida entramos no WSL2 e instalamos o _Docker_

```bash
sudo pacman -S docker
```