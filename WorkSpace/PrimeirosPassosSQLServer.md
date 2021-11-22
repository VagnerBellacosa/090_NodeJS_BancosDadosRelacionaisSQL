Artigo[Invista em você! Saiba como a DevMedia pode ajudar sua carreira.](https://www.devmedia.com.br/primeiros-passos-no-sql-server/40653#modulo-mvp)

# Primeiros passos no SQL Server

## Daremos os primeiros passos com o gerenciador de bancos de dados relacionais Microsoft SQL Server. Conheça suas principais características, como instalar e como criar o primeiro banco de dados.

Por que eu devo ler este artigo:Nesse artigo vamos entender o conceito de bancos de dados, as principais características do SQL Server e como realizar a instalação dessa ferramenta para gerenciar bancos de dados.

[Voltar](https://www.devmedia.com.br/sql-server/tabelas)Suporte ao alunoAnotarMarcar como concluídoCódigo fonte

[Artigos](https://www.devmedia.com.br/artigos/)[Banco de Dados](https://www.devmedia.com.br/artigos/banco-de-dados)Primeiros passos no SQL Server

Quando agrupamos dados e criamos relações entre eles temos o cenário para a criação de bancos de dados. Um banco de dados relacional é uma forma de manipular e armazenar dados na forma de tabelas, como a que vemos na **Figura 1**.

![Tabela de Produtos](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_01/Figura_01.PNG)**Figura 1**. Tabela de Produtos

Os Sistemas Gerenciadores de Bancos de Dados Relacionais ou SGBDR, são softwares que gerenciam bancos de dados relacionais. Um dos SGBDRs mais usados é o Microsoft SQL Server.

Ele está disponível em diferentes edições que atendem a desenvolvedores, pequenos negócios e grandes empresas.

Ele pode ser integrado a outras soluções da Microsoft, incluindo as ferramentas para desenvolvimento de software como a linguagem C#. Essa parceria enriquece o desenvolvimento de aplicações modernas.

Nesse artigo vamos entender o conceito de bancos de dados, as principais características do SQL Server e como realizar a instalação dessa ferramenta para gerenciar bancos de dados.

Vamos aprender a instalar o SQL Server em nosso computador e o Azure Data Studio, uma ferramenta gratuita e leve que podemos usar para acessar o SGBDR. E por fim, vamos criar um banco de dados com uma tabela simples chamada Produto. Na **Animação 1** abaixo vemos o resultado final, onde inserimos e consultamos dados nessa tabela.

![Tabela de Produtos](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_02/Animacao_01.gif)**Animação 1**. Visualizando a tabela “Produto” no Azure Data Studio.

### O que é um banco de dados relacional?

Em um banco de dados relacional organizamos as informações em forma de tabelas que podem estar relacionadas.

#### Tabelas

Tabelas possuem uma estrutura de colunas com os tipos de dados e linhas com as informações.

Por exemplo, em uma tabela Produto temos as colunas Id do tipo inteiro, nome do tipo string e quantidade do tipo inteiro, conforme a **Figura 2**.

Não pretendemos seguir alguma regra de negócio específica com os exemplos utilizados, mas apenas ilustrar as explicações dadas neste post.

![Colunas da tabela Produto com seus tipos de dados](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_03/Figura_01.PNG)**Figura 2**. Colunas da tabela “Produto” com seus tipos de dados.

#### Chave Primária

A coluna ID tem a função chave primária (primary key), que é uma coluna com um valor único que identifica essa linha de dados na tabela. O valor de uma coluna que é chave primária não pode ser repetido na mesma tabela.

Os dados que vão preencher a tabela devem ser do mesmo tipo definido para as colunas. Por exemplo, as colunas id e Quantidade foram definidas com o tipo inteiro e por este motivo não podem receber valores que não sejam números inteiros, conforme a **Figura 3**.

![Dados do tipo String inválidos para as colunas Id e Quantidade](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_03/Figura_02.PNG)**Figura 3**. Dados do tipo String inválidos para as colunas “Id” e “Quantidade”

#### Relacionamentos

Os bancos de dados relacionais permitem criarmos relacionamentos entre as tabelas. Por exemplo, podemos ter uma segunda tabela Vendas com as colunas Id, Data, Pago e Produto_id. Esta tabela será preenchida com dados sobre as vendas dos produtos, sendo que a coluna Produto_id receberá o valor da coluna Id do respectivo produto na tabela Produto.

#### Chave Estrangeira

Esse tipo de coluna é chamado chave estrangeira (foreign key) e serve como uma referência para o valor de uma coluna chave primária em outra tabela e essa referência cria o relacionamento entre as duas tabelas.

Se fizermos uma venda do produto CAFÉ vamos preencher a coluna Produto_id com o valor 4 que é o valor da coluna Id deste produto, conforme a **Figura 4**.

![Tabela Vendas preenchida com os dados de uma venda do produto CAFÉ identificado pelo valor preenchido na coluna Produto_id](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_03/Figura_03.PNG)**Figura 4**. Tabela “Vendas” preenchida com os dados de uma venda do produto “CAFÉ” identificado pelo valor preenchido na coluna “Produto_id”

Assim criamos um relacionamento entre as tabelas “Produto” e “Vendas”, conforme a **Figura 5**.



![Relacionamento entre as tabela Vendas e Produto](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_03/Figura_04.PNG)**Figura 5**. Relacionamento entre as tabela “Vendas” e “Produto”

Com o valor da chave estrangeira Produto_id podemos consultar na tabela Produto o nome do produto dessa venda e qual a quantidade disponível.

### Conhecendo o SQL Server

O SQL Server é um sistema gerenciador de bancos de dados relacionais (SGBDR). Com ele podemos criar bases de dados com tabelas e manipular seus respectivos dados. Dentre as operações que podemos realizar com as tabelas podemos citar aquelas conhecidas como CRUD, conforme a **Figura 6**.

![Operações CRUD- Criar, Consultar, Alterar e Apagar dados em tabelas](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_04/Figura_01.png)**Figura 6**. Operações CRUD: Criar, Consultar, Alterar e Apagar dados em tabelas

Vamos explicar o acrônimo CRUD:

- **CREATE**: criamos ou incluímos novos dados em uma tabela;
- **READ**: lemos ou consultamos dados de uma ou mais tabelas;
- **UPDATE**: atualizamos ou alteramos os dados em uma tabela;
- **DELETE**: apagamos ou excluímos os dados em uma tabela.

### Linguagem T-SQL

Podemos escrever queries para nossos bancos de dados com a linguagem T-SQL que é muito semelhante a linguagem SQL utilizada em outros gerenciadores de bancos de dados relacionais (SGBDR). Por exemplo, podemos consultar a tabela “Produto” com a query abaixo:

```
SELECT Id, Nome, Quantidade FROM Produto
```

Explicando essa query:

- **SELECT**: selecionamos as colunas da tabela que queremos retornar escrevendo seus nomes após a palavra SELECT. Se queremos retornar todas as colunas de uma tabela podemos usar o caractere * no lugar dos nomes de todas colunas da tabela.
- **FROM**: informamos a origem dos dados ou o nome da tabela após a palavra FROM.

### Instalando a edição Express

Atualmente o SQL Server está disponível nas edições Enterprise, Standard, Express e Developer. Vamos conhecer as características de cada edição.

- **Enterprise**: possui recursos de missão crítica para fornecer segurança, capacidade de escalar, alta disponibilidade e performance as bases de dados. Indicado para cenários em que for preciso manipular quantidades de dados que crescem rapidamente de forma segura e eficiente.
- **Standard**: possui os mesmos recursos que a edição Enterprise, mas para cenários intermediários.
- **Express**: essa edição é gratuita e não possui todos recursos da edição Enterprise. Pode ser utilizada em produção com bases de dados de até 10 GB.
- **Developer**: possui todos recursos da edição Enterprise. Não pode ser utilizada em produção, mas apenas em desenvolvimento.

Os requisitos para instalação do SQL Server podem variar de acordo com a edição. Vamos instalar a edição Express que pode ser utilizada em produção de aplicações menores.

Para instalar o SQL Server edição Express vamos fazer o [download ](https://www.microsoft.com/pt-br/sql-server/sql-server-downloads)da ferramenta.

A versão 2017 e o preview da versão 2019 podem ser instalados nas plataformas Windows, MacOS, Linux e Docker. Aqui vamos instalar o SQL Server na plataforma Windows.

Nesta página temos uma descrição da edição Express e a opção “Faça download agora mesmo”, conforme a **Figura 7**.

![Link de download da edição Express do SQL Server]()**Figura 7**. Link de download da edição Express do SQL Server

### Instalação básica da edição Express do SQL Server

Execute como administrador o arquivo de instalação para abrir a instalação conforme a **Figura 8**.

![Tela inicial de instalação da edição Express do SQL Server]()**Figura 8**. Tela inicial de instalação da edição Express do SQL Server

Nessa tela inicial clique no tipo de instalação “Básico”. A segunda tela é o termo de licença do SQL Server, conforme a **Figura 9**.

![Termo de licença do SQL Server]()**Figura 9**. Termo de licença do SQL Server

Clique no botão “Aceitar” para abrir a terceira tela com o local de instalação, conforme a **Figura 10**.

![Tela para escolher o local de instalação](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_05/Figura_04.PNG)**Figura 10**. Tela para escolher o local de instalação

Mantenha o local de instalação que foi sugerido pelo instalador. Apenas clique no botão “Instalar”. Em seguida começa a instalação em si, conforme a **Figura 11**.

![Progresso da instalação](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_05/Figura_05.PNG)**Figura 11**. Progresso da instalação

Ao fim da instalação temos esta última tela, conforme a **Figura 12**.

![Conclusão da instalação do SQL Server](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_05/Figura_06.PNG)**Figura 12**. Conclusão da instalação do SQL Server

Nela temos alguns recursos interessantes:

- **Cadeia de conexão:** Uma cadeia de conexão ou **ConnectionString** que pode ser utilizada no desenvolvimento de aplicações .NET. Basta clicar no botão "copiar" e colar a cadeia de conexão no código da aplicação.
- **Botão “Conectar agora”:** Ao clicar neste botão, abre-se o prompt de comando e automaticamente executa a ferramenta de linha de comando do SQL Server, conectando ao SGBDR e disponibilizando o prompt para executar comandos da T-SQL.
- **Botão “Instalar o SSMS”:** Esse botão vai conduzir a instalação do SQL Server Management Studio para trabalharmos com o SQL Server sem a linha de comando. Nesse post vamos utilizar outra ferramenta que será apresentada na próxima aula.
- **Nome da instância:** Para cada instalação de SQL Server temos uma instância. Podemos ter diversas instâncias de SQL Server que podem ser diferentes umas das outras.

Guarde o nome da instância porque vamos utilizá-la quando conectarmos a primeira vez com nossa instância do SQL Server.

Já temos o SQL Server instalado e em execução!

### Instalando o Azure Data Studio

Quando instalamos o SQL Server foi disponibilizada a ferramenta sqlcmd, para ser utilizada no prompt de comando. Muitos desenvolvedores preferem utilizar uma ferramenta com interface visual para gerenciar o SQL Server. Por muitos anos o SQL Server Management Studio tem sido a ferramenta preferida para trabalhar com SQL Server.

### Alternativa ao SQL Server Management Studio

Recentemente a Microsoft lançou uma ferramenta mais leve que é o **Azure Data Studio**. Ela foi criada para trabalhar com bancos de dados SQL Azure e com BDs SQL Server. O Azure Data Studio está disponível para as plataformas Windows, MacOS, Linux e Docker, mas aqui vamos instalar o Azure Data Studio na plataforma Windows.

O Azure Data Studio não substitui o SQL Server Management Studio, mas é uma nova opção. Enquanto o SQL Server Management Studio é mais indicado para Administração de bancos de dados e tarefas mais complexas com SQL Server, o Azure Data Studio é indicado para quem trabalha muito criando queries.

### Como instalar

Para começar a instalação do Azure Data Studio vamos abrir o navegador e acessar a [página de downloads](https://docs.microsoft.com/pt-br/sql/azure-data-studio/download?view=sql-server-ver15).

Navegamos para a página de download do Azure Data Studio, conforme a **Figura 13**.

![Página de download do Azure Data Studio](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_06/Figura_01.PNG)**Figura 13**. Página de download do Azure Data Studio

Na página de download temos uma tabela com as opções de instalação para as plataformas Windows, MacOS e Linux. Nas opções para a plataforma Windows clique no link “instalador do usuário (recomendado)”, conforme a **Figura 14**.

![Link para o instalador para plataforma Windows](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_06/Figura_02.PNG)**Figura 14**. Link para o instalador para plataforma Windows

Baixe e execute o instalador. Veja como é simples a instalação na **Animação 2**.

![Instalando o Azure Data Studio](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_06/Animacao_01.gif)**Animação 2**. Instalando o Azure Data Studio

### Criando um banco de dados e uma tabela

Nas aulas anteriores instalamos a edição Express do SQL Server e o Azure Data Studio para gerenciá-lo. Nessa aula vamos criar um banco de dados e uma tabela apenas para ter um primeiro contato com a ferramenta. Não se preocupe em entender tudo agora, porque esses passos serão vistos em detalhes em outros conteúdos.

Abra o Azure Data Studio e ele exibirá um formulário para configurar a conexão ao nosso servidor SQL Server.

Lembra que na última tela de instalação do SQL Server ele resumiu as informações de conexão? Vamos utilizá-las agora.

Como escolhemos a instalação básica do SQL Server, só precisamos de uma informação que é o **nome da instância**. Na instalação que fizemos ele nomeou a instância como SQLEXPRESS01. Vamos preencher o campo Server do formulário com os caracteres .\ e o nome da instância e clicar no botão **Conectar-se**. Acompanhe o processo na **Animação 3**.

![Conectando a instância do SQL Server no Azure Data Studio](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_07/Animacao_01.gif)**Animação 3**. Conectando a instância do SQL Server no Azure Data Studio

### Query para criar um banco de dados

Na aba de nossa instância SQLEXPRESS01 clique na imagem “New Query” para abrir o Editor de Query. Nesse editor podemos escrever queries em T-SQL (TRANSACT-SQL) e executar em nossa instância SQL Server. Vamos escrever uma query para criar nosso primeiro banco de dados:

```
CREATE DATABASE LOJA
```

**Listagem 1.** Criando um banco de dados com a instrução CREATE DATABASE.

Explicando a query:

- O comando CREATE DATABASE LOJA cria um banco de dados com o nome LOJA na instância ativa do SQL Server.

Clique em Executar ou tecle F5 para executar a query. Veja a criação e execução dela na **Animação 4**.

![Executando uma query para criar o banco de dados LOJA](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_07/Animacao_02.gif)**Animação 4**. Executando uma query para criar o banco de dados “LOJA”

### Informando o banco de dados ativo

Antes de começar a escrever queries para executar em um banco de dados precisamos informar ao SQL Server para qual banco de dados vamos escrever a query. Podemos fazer isso de duas maneiras.

- No Azure Data Studio quando abrimos uma aba com o editor de query temos uma lista suspensa com os bancos de dados criados em nosso servidor. Basta selecionar o banco de dados e em seguida começar a escrever a query, conforme na **Animação 5**
- Podemos usar uma instrução T-SQL para informar o banco de dados que iremos escrever a query usando o comando USE seguido do nome do banco de dados, conforme a **Listagem 2**.

Veja como informar ao SQL Server para qual banco de dados vamos escrever a query na **Animação 5**.

![Instalando o Azure Data Studio](https://www.devmedia.com.br/arquivos/Artigos/40684/selecionando_banco_de_dados.gif)**Animação 5**. Instalando o Azure Data Studio

Com o novo banco de dados LOJA criado podemos mudar o banco de dados ativo selecionando na lista suspensa da aba do editor de query o banco de dados “LOJA”.

```
USE LOJA;
```

**Listagem 2.** Informando o banco de dados ativo com a instrução USE.

### Query para criar uma tabela

Vamos criar uma tabela no banco de dados “LOJA” escrevendo uma nova query:

```
CREATE TABLE PRODUTO (
      ID INT,
      NOME VARCHAR(50),
      QUANTIDADE INT
  )
```

Explicando a query:

- O comando CREATE TABLE PRODUTO cria uma tabela com o nome PRODUTO no banco de dados ativo.
- ID INT define a coluna “ID” com o tipo INT para números inteiros.
- NOME VARCHAR(50) define a coluna “NOME” com o tipo VARCHAR e tamanho 50 para uma string de até 50 caracteres.
- QUANTIDADE INT define a coluna “QUANTIDADE” com o tipo INT para números inteiros.

Executamos a query e temos a tabela PRODUTO em nosso banco de dados, conforme a **Animação 6**.

![ Executando uma query para criar a tabela PRODUTO](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_07/Animacao_03.gif)**Animação 6**. Executando uma query para criar a tabela PRODUTO

### Query para alterar uma tabela

Após criada, uma tabela pode ser alterar utilizando o seguinte comando:

```
ALTER TABLE PRODUTO
```

Explicando a query:

- O comando ALTER TABLE PRODUTO indica que vamos alterar a tabela com o nome PRODUTO.

Este comando (ALTER TABLE nome_da_tabela) é seguido da alteração que queremos fazer na tabela. Veja alguns exemplos:

**Exemplo 1:** Inserindo uma coluna:

```
ALTER TABLE PRODUTO
ADD TIPO VARCHAR(50);
```

Explicando a query:

- O comando ALTER TABLE PRODUTO indica que vamos alterar a tabela com o nome PRODUTO.
- ADD TIPO VARCHAR(50) indica que vamos inserir a coluna com o nome TIPO.

Ao executar a query a coluna TIPO será inserida na tabela PRODUTO.

**Exemplo 2:** Alterando o tipo de uma coluna:

```
ALTER TABLE PRODUTO
ALTER COLUMN TIPO INT;
```

Explicando a query:

- O comando ALTER TABLE PRODUTO indica que vamos alterar a tabela com o nome PRODUTO.
- ALTER COLUMN TIPO INT indica que vamos alterar a coluna com o nome TIPO definindo que o seu tipo será INT.

Ao executar a query a coluna TIPO passa a ser do tipo INT.

**Exemplo 3:** Removendo uma coluna:

Para remover uma coluna utilizamos o seguinte código:

```
ALTER TABLE PRODUTO
DROP COLUMN TIPO;
```

Explicando a query:

- Mais uma vez utilizamos o comando ALTER TABLE PRODUTO para alterar a tabela com o nome PRODUTO.

- Dessa vez utilizamos o comando DROP COLUMN TIPO para remover a coluna com o nome TIPO.

- Após a execução do código a coluna TIPO será removida da tabela PRODUTO.

- ### Query para incluir dados em uma tabela

- Podemos também criar uma query para incluir dados na tabela “PRODUTO” e consultar os dados da tabela:

- ```
  INSERT INTO PRODUTO (ID, NOME, QUANTIDADE) VALUES (1,’BISCOITO’,10);
  INSERT INTO PRODUTO (ID, NOME, QUANTIDADE) VALUES (2,’LEITE’,5);
  INSERT INTO PRODUTO (ID, NOME, QUANTIDADE) VALUES (3,’SABÃO’,7);
  INSERT INTO PRODUTO (ID, NOME, QUANTIDADE) VALUES (4,’CAFÉ’,12);
  ```

- Explicando a query:

- - INSERT INTO PRODUTO é comando para inserir dados na tabela “PRODUTO”
  - (ID, NOME, QUANTIDADE) informa as colunas da tabela que vão receber dados
  - VALUES (1,’BISCOITO’,10) informa os valores para cada coluna na mesma ordem das colunas.
  - As três linhas seguintes repetem o comando para inserir dados, onde cada uma insere uma linha diferente de dados na tabela.

- ### Query para consultar uma tabela

- Agora vamos escrever uma query para consultar a tabela PRODUTO:

- ```
  SELECT ID, NOME, QUANTIDADE FROM PRODUTO
  ```

- Explicando a query:

- - SELECT ID, NOME, QUANTIDADE seleciona as colunas da tabela para serem exibidas na consulta, nesse caso ID, NOME e QUANTIDADE.
  - FROM PRODUTO informa de qual tabela queremos trazer os dados, nesse caso PRODUTO.
  - Como não foi informado uma condição para consulta serão trazidas todas as linhas da tabela PRODUTO.

- Veja a execução dessa query e o resultado da consulta a tabela na **Animação 7**.

- ![ Inserindo dados e consultando a tabela PRODUTO](https://www.devmedia.com.br/arquivos/cursos/SQLServer_2344/Aula_07/Animacao_04.gif)**Animação 7**. Inserindo dados e consultando a tabela “PRODUTO”

- Parabéns! Você criou seu primeiro banco de dados no SQL Server!

Tecnologias:

- [SQL](https://www.devmedia.com.br/sql/)
-  

- SQL Azure
-  

- [SQL Server](https://www.devmedia.com.br/sql-server/)
-  

- Transact-SQL

[Voltar](https://www.devmedia.com.br/sql-server/tabelas)AnotarMarcar como concluído



Inicie agora sua carreira de programador por apenas R$ 54,90*/mês*

Ainda está em dúvida? Experimente a plataforma durante 3 dias sem cartão. [Faça um teste grátis](https://www.devmedia.com.br/pro/)

BENEFÍCIOS

- Suporte em tempo real
- Certificado de autoridade
- Exercícios para praticar
- Estudo gamificado
- Planos de estudo para cada carreira de programador

[Saiba mais](https://www.devmedia.com.br/pro/)

![autor](https://www.devmedia.com.br/imagens/fotoscolunistas/643270_20191113033309.jpg)

Por [Renato](https://www.devmedia.com.br/perfil/renato-dias-6)Em 2019

![img](https://my.rtmark.net/img.gif?f=sync&partner=8d192082bc983b05cb53af79646518fd98e3750c921f0ae655da3dd5cb2d040f&ttl=&rurl=https%3A%2F%2Fwww.devmedia.com.br%2Fprimeiros-passos-no-sql-server%2F40653)