---
title: Frameworks para desenvolvimento de software
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags:
description: 
---
# Aula 1 - Introdução aos frameworks
## Mapa Mental
![[Pasted image 20230803224214.png]]

## Vídeo 1
- Framework tem um sentido de uma estrutura organizada, buscando resolver problemas específicos.
- Não existe somente no mundo do desenvolvimento, por exemplo o SCRUM é um framework de gestão de projetos.
- Basicamente um framework no mundo de desenvolvimento e um conjunto de códigos fontes, afim de facilitar e agilizar o desenvolvimento.
- Garante uma flexibilidade no desenvolvimento, garantidas pelo framework, como troca de banco de dados.
- MVC (Model-View-Controller)
- E um padrão que define a divisão de camadas do sistema, os dados são passados entre as camadas por meio de interfaces.

![[Pasted image 20230804172132.png]]

- **View** - O que manda para o usuário visualizar. (Frontend)
- **Controller** - Onde é realizado as manipulações dos dados. (Backend)
- **Model** - A camada que esta em contado com o banco de dados. (ADM do banco de dados)
- Não especifica as tecnologias a serem usadas, se preocupa na padronização do projeto.
- Manutenção em uma camada não influencia na outra.

### Model
- A camada que representa o negocio da aplicação
- Onde é executando as operações com os dados.
- Pode ser divido em _Logic Layer_ (BLL) e _Access Layer_ (DAL) 

### View
- Camada de apresentação dos dados
- Interage com o usuário.
- Formulários entre outros.

### Controller
- Recebe as requisições do usuário.
- Direciona os processos necessários para camada model, processa os dados e devolve para view.
- Isola a  camada _view_ da camada _model_, assim sendo necessário passar toda as requisições pela mesma.
- Responsável pelas rotas da aplicação.
- Com bancos nosql normalmente a camada da regra fica no _controller_.

### CRUD
- Um sistema é constituído de CRUDs
- Os CRUDs são ferramentas que habilitaram dinamismo no sistema.
	- Create -  Criar um novo registro no banco de dados.
	- Retrive - Recuperar um registro do banco de dados
	- Update - Atualizar um registro no banco de dados
	- Delete - Excluir um registro no banco de dados.

## Vídeo 2
- Utilizando python é interessante criar ambientes virtuais para instalar os pacotes, invés de instala-los globalmente, para isso podemos usar o `virtualenv` onde podemos criar a estrutura para o mesmo utilizando o seguinte comando `python3 -m venv myenv`
- _myenv_ é um exemplo de nome para o diretório que será criado.
- Posterior mente é necessário ativar esse ambiente através do código, `source myenv/bin/active`
- Interessante adicionar o diretório no `.gitignore`
- Podemos criar um arquivo de bibliotecas requisitas facilmente através do comando `pip freeze`, onde o mesmo lista as _libs_ instaladas, assim podemos redirecionar para um arquivo sua saída `pip freeze > requirements.txt`

# Aula 2 - Flask na prática
## Mapa Mental
![[Pasted image 20230805150302.png]]

## Vídeo
- Para pegar parâmetros utilizamos o `<>`, por exemplo.

```python
@app.route('/sobre/<nome>')
def sobreNome(nome):
	return f'Olá {nome}
```

- Para renderizar páginas HTML com o _flask_ é necessário utilizar a `render_template`, onde podemos criar um diretório com o nome `templates` e desenvolver os códigos HTML.
- Para chamar nosso arquivo HTML basta utilizar a função importada `render_html` com o nome do arquivo que se encontra no diretório `templates`
- Podemos passar valores para o nosso documento HTML através de variáveis que passamos junto ao documento por exemplo.

```python
@app.route('/user/<username>')
def profile(username):
	return render_template('profile.html', username=username)
```

- A esquerda o nome da variável para o HTML a direita o valor que estamos passando para ela, normalmente utilizamos o mesmo mas nada impede de mudar por exemplo `user=username`
- Para definir os locais no documento HTML onde será inserido tal valor, basta colocar o nome da variável para o HTML entre dois colchetes por exemplo `{{username}}`
- Para evitar erros podemos passar um valor base para o valor do parâmetro e criar uma rota sobreposta que não possui valor no parâmetro

```python
@app.route("/user/")
@appl.route("/user/<username>")
def profile(username=None):
	return render_template('profile.html', username=username)
```

- Também podemos tratar dentro do HTML com _python_ também (Aumento o processamento no Backend)

```html
{% if username %}
	<h1>Bem Vindo ao ECommerce, {{username}}</h1>
{% else %}
	<h1>Bem-Vindo ao ECommerce, Anonimo</h1>
{$ endif %}
```

### Cookies
- Para trabalhar com _cookies_ é necessário utilizar `make_response` que se encontra dentro do _flask_
- Para "setar" um cookie, primeiro e necessário instancia-lo em uma variável com `cok = make_response()` em seguida utilizamos a mesma para 'setar' o valor `cok.set_cookie('username', username)` e retornamos a variável com os _cookies_.
- Para pegar um valor salvo nos _cookies_ é necessário importar o `request` do _flask_ e utiliza-lo da seguinte forma `cookUsername = request.cookies.get('username')`

# Aula 3 - Estrutura do sistema
## Mapa Mental
![[Pasted image 20230805203932.png]]

## Vídeo
- Ideia de estruturação do sistema.
![[Pasted image 20230807185900.png|400]]
- Para criar _links_ dentro no nosso site, podemos utilizar no endereço da _tag_ [[HyperLinks|Ancora]], onde como valor do atributo `href` passamos o seguinte valor `{{url_for("user")}}` _user_ é um exemplo de **função de uma rota**.
- Dentro de uma rota devemos definir os [[HTTP#Methods|métodos]] que aceitamos, os adicionando dentro de uma _[[Array|array]]_, por exemplo

```python
@app.route("/cat/user", methods=['post'])
def catUser():
  return request.form
```

- Através do `request.form` temos acesso aos dados recebidos, ou seja, o corpo da requisição.

# Aula 4 - Mapeamento ORM
## Mapa Mental
![[Pasted image 20230810151850.png]]

## Vídeo
- Instalarmos as dependências via `pip` sendo elas `wheel, mysqlclient, mysql-connector`.
- Em seguida é necessário configurar a conexão com o banco de dados, e passar uma instancia do SQLAlchemy para uma variável.

>[!attention] Atenção
>Pode ser que seja necessário instalar dependencias no sistema, quando utilizei Arch Linux via WSL2, foi necessário instalar o pacote `mariadb-libs`
>```bash
>sudo pacman -S mariadb-libs
>```

```python
app.config[ 'SQLALCHEMY_DATABASE_URI' ] = 'mysql://testeuser:user123@localhost:3306/bestec'
app.config[ 'SQLALCHEMY_TRACK_MODIFICATIONS' ]  = False

db = SQLAlchemy(app)
```

>[!attention] Atenção com WSL2
>Utilizando o WSL2 é necessário invés do `localhost`, utilizar o _IP_ que se encontra dentro do _path_ `/etc/resolv.conf` na frente do texto `nameserver`, basta utilizar o comando `cat`
>```bash
>cat /etc/resolv.conf
>```

- Devemos criar os modelos das nossas tabelas no banco de dados que serão classes e um construtor, caso já exista a tabela no banco e caso não exista será criado, passamos `db.Model` para herdar de uma classe base já disponibilizada pelo SQLAlchemy.

```python
class Usuario(db.Model):
    id = db.Column(db.integer, primary_key=True, autoincrement=True)
    nome = db.Column(db.String(250), nullable=False)
    email = db.Column(db.String(250), nullable=False)
    senha = db.Column(db.String(250), nullable=False)
    cpf = db.column(db.integer, nullable=True)
    dt_nascimento = db.Column(db.Date, nullable=True)
    telefone = db.Column(db.integer, nullable=True)
    rua = db.Column(db.String(250), nullable=True)
    numero = db.Column(db.integer, nullable=True)
    complemento = db.Column(db.String(250), nullable=True)
    bairro = db.Column(db.String(250), nullable=True)
    cidade = db.Column(db.String(250), nullable=True)
    estado = db.Column(db.String(250), nullable=True)

    def __init__(self, nome, email, senha, cpf, dt_nascimento, telefone, rua, numero, complemento, bairro, cidade, estado):
        self.nome = nome
        self.email = email
        self.senha = senha
        self.cpf = cpf
        self.dt_nascimento = dt_nascimento
        self.telefone = telefone
        self.rua = rua
        self.numero = numero
        self.complemento = complemento
        self.bairro = bairro
        self.cidade = cidade
        self.estado = estado
```