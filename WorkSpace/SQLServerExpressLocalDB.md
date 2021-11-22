# SQL Server Express LocalDB

- Artigo - 23/10/2021 - 10 minutos para o fim da leitura
- - [![img](https://github.com/markingmyname.png?size=32)](https://github.com/markingmyname)
  - [![img](https://github.com/olprod.png?size=32)](https://github.com/olprod)

Esta página é útil?

**Aplica-se a:** ![sim](https://docs.microsoft.com/pt-br/sql/includes/media/yes-icon.png?view=sql-server-ver15)SQL Server (todas as versões compatíveis)

O LocalDB do Microsoft SQL Server Express é um recurso do [SQL Server Express](https://docs.microsoft.com/pt-br/sql/sql-server/editions-and-components-of-sql-server-version-15?view=sql-server-ver15) voltado para desenvolvedores. Ele está disponível no SQL Server Express com Advanced Services.

A instalação do LocalDB copia um conjunto mínimo de arquivos necessários para iniciar o Mecanismo de Banco de Dados do SQL Server. Depois do LocalDB ser instalado, você poderá iniciar uma conexão usando uma cadeia de conexão especial. Ao conectar, a infraestrutura necessária do SQL Server é criada e iniciada automaticamente, permitindo que o aplicativo use o banco de dados sem tarefas de configuração complexas. O Developer Tools pode fornecer aos desenvolvedores um Mecanismo de Banco de Dados do SQL Server que permite que eles gravem e testem o código Transact-SQL sem precisar gerenciar uma instância de servidor inteira do SQL Server.

## Mídia de instalação

LocalDB é um recurso selecionado durante a instalação do SQL Server Expresse que está disponível durante o download da mídia. Se você baixar a mídia, escolha **Express Advanced** ou o pacote **LocalDB** .

- [SQL Server Express 2019](https://go.microsoft.com/fwlink/?LinkID=866658)
- [SQL Server Express 2017](https://go.microsoft.com/fwlink/?LinkID=853017)

O instalador do LocalDB — `SqlLocalDB.msi` — está disponível na mídia de instalação para todas as edições, exceto para o Express Core. Ele está localizado na pasta `<installation_media_root>\<LCID>_ENU_LP\x64\Setup\x64`. O LCID é uma ID de localidade ou código de idioma. Por exemplo, um valor LCID de 1033 refere-se à localidade **en-US**.

Como alternativa, é possível instalar o LocalDB pelo [Instalador do Visual Studio](https://visualstudio.microsoft.com/downloads/), como parte da carga de trabalho de **Processamento e Armazenamento de Dados**, da carga de trabalho de **desenvolvimento Web e ASP.NET** ou como um componente individual.

## Instalar o LocalDB

Instalar o LocalDB por meio do assistente de instalação ou usando o programa `SqlLocalDB.msi`. O LocalDB é uma opção na instalação do SQL Server Express LocalDB.

Escolha LocalDB na página **Seleção de Recursos/Recursos Compartilhados** durante a instalação. Pode haver somente uma instalação dos arquivos binários do LocalDB para cada versão principal do Mecanismo de Banco de Dados do SQL Server. Vários processos do Mecanismo de Banco de Dados podem ser iniciados e todos usarão os mesmos binários. Uma instância do Mecanismo de Banco de Dados do SQL Server iniciada como o LocalDB tem as mesmas limitações do SQL Server Express.

Uma instância do LocalDB do SQL Server Express é gerenciada com o utilitário `SqlLocalDB.exe`. O LocalDB do SQL Server Express deve ser usado no lugar do recurso de instância do usuário SQL Server Express que foi preterido.

## Descrição

O programa de instalação do LocalDB usa o programa `SqlLocalDB.msi` para instalar os arquivos necessários no computador. Uma vez instalado, o LocalDB torna-se uma instância do SQL Server Express que pode criar e abrir bancos de dados do SQL Server. Os arquivos de banco de dados do sistema para o banco de dados são armazenados no caminho de AppData local, que normalmente é oculto. Por exemplo, `C:\Users\<user>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\`. Arquivos de banco de dados do usuário são armazenados onde o usuário determinar, normalmente em algum lugar na pasta `C:\Users\<user>\Documents\`.

Para saber mais sobre como incluir o LocalDB em um aplicativo, confira a Visual Studio [Visão geral de dados locais](https://docs.microsoft.com/pt-br/previous-versions/visualstudio/visual-studio-2012/ms233817(v=vs.110)), [Criar um banco de dados e adicionar tabelas no Visual Studio](https://docs.microsoft.com/pt-br/visualstudio/data-tools/create-a-sql-database-by-using-a-designer).

Para saber mais sobre a API LocalDB, confira [Referência de LocalDB do SQL Server Express](https://docs.microsoft.com/pt-br/sql/relational-databases/sql-server-express-localdb-reference?view=sql-server-ver15).

O utilitário `SqlLocalDB` pode criar instâncias do LocalDB, iniciar e interromper uma instância do LocalDB, além de contar com opções para ajudar a gerenciar o LocalDB. Para obter mais informações sobre o utilitário `SqlLocalDB`, confira [Utilitário SqlLocalDB](https://docs.microsoft.com/pt-br/sql/tools/sqllocaldb-utility?view=sql-server-ver15).

A ordenação de instâncias do LocalDB foi definida como `SQL_Latin1_General_CP1_CI_AS` e não pode ser alterada. Normalmente há suporte para ordenações nos níveis de banco de dados, de coluna e de expressão. Os bancos de dados independentes seguem os metadados e as regras de ordenações `tempdb` definidas por [Ordenações de banco de dados independentes](https://docs.microsoft.com/pt-br/sql/relational-databases/databases/contained-database-collations?view=sql-server-ver15).

### Restrições

- O LocalDB não pode ser corrigido além dos Service Packs. CUs e atualizações de segurança não podem ser aplicadas manualmente e não serão aplicadas por meio do Windows Update, Windows Update para Empresas ou outros métodos.
- O LocalDB não pode ser gerenciado remotamente por meio do SQL Management Studio.
- O LocalDB não pode ser um assinante de replicação de mesclagem.
- O LocalDB não dá suporte a FILESTREAM.
- O LocalDB só permite filas locais para Service Broker.
- Uma instância do LocalDB pertencente às contas internas, como `NT AUTHORITY\SYSTEM`, pode ter problemas de capacidade de gerenciamento devido ao redirecionamento do sistema de arquivos do Windows. Em vez disso, use uma conta normal do Windows como o proprietário.

### Instâncias automáticas e nomeadas

O LocalDB oferece suporte a dois tipos de instâncias: Instâncias automáticas e instâncias nomeadas.

- As instâncias automáticas do LocalDB são públicas. Elas são criadas e gerenciadas automaticamente para o usuário e podem ser usadas por qualquer aplicativo. Existe uma instância automática do LocalDB para cada versão do LocalDB instalada no computador do usuário. As instâncias automáticas do LocalDB fornecem gerenciamento de instância contínuo. Não há necessidade de criar a instância; assim é o suficiente. Esse recurso facilita a instalação e migração do aplicativo para um computador diferente. Se o computador de destino tiver a versão especificada do LocalDB instalada, a instância automática do LocalDB para essa versão também estará disponível no computador de destino. As instâncias automáticas do LocalDB têm um padrão especial para o nome de instância que pertence a um namespace reservado. As instâncias automáticas evitam conflitos de nomes com instâncias nomeadas do LocalDB. O nome da instância automática é **MSSQLLocalDB**.
- As instâncias nomeadas do LocalDB são privadas. Elas pertencem a um único aplicativo, que é responsável por criar e gerenciar a instância. As instâncias nomeadas fornecem isolamento de outras instâncias e melhoram o desempenho reduzindo a contenção de recursos com outros usuários de banco de dados. As instâncias nomeadas devem ser criadas explicitamente pelo usuário por meio da API de gerenciamento do LocalDB ou implicitamente por meio do arquivo app.config para um aplicativo gerenciado (embora o aplicativo gerenciado também possa usar a API, se desejado). Cada instância nomeada do LocalDB tem uma versão associada do LocalDB que aponta para o conjunto respectivo de binários do LocalDB. O nome da instância do LocalDB é o tipo de dados **sysname** e pode ter até 128 caracteres. (Isso difere das instâncias nomeadas normais do SQL Server, que limitam os nomes a nomes NetBIOS normais de 16 caracteres ASCII.) O nome de uma instância do LocalDB pode conter qualquer caractere Unicode legal em um nome de arquivo. Uma instância nomeada que usa um nome de instância automática torna-se uma instância automática.

Usuários diferentes de um computador podem ter instâncias com o mesmo nome. Cada instância é um processo diferente executado como um usuário diferente.

## Instâncias compartilhadas do LocalDB

Para oferecer suporte a cenários onde vários usuários do computador precisam se conectar a uma única instância do LocalDB, o LocalDB oferece suporte ao compartilhamento de instâncias. O proprietário de uma instância pode optar por permitir que outros usuários do computador se conectem à sua instância. As instâncias automáticas e nomeadas do LocalDB podem ser compartilhadas. Para compartilhar uma instância do LocalDB, o usuário escolhe um nome compartilhado (alias) para isso. Como o nome compartilhado fica visível para todos os usuários do computador, ele deve ser exclusivo no computador. O nome compartilhado de uma instância do LocalDB tem o mesmo formato da instância nomeada do LocalDB.

Somente um administrador no computador pode criar uma instância compartilhada do LocalDB. Uma instância compartilhada do LocalDB pode ser descompartilhada por um administrador ou pelo proprietário da instância compartilhada do LocalDB. Para compartilhar e descompartilhar uma instância do LocalDB, use os métodos `LocalDBShareInstance` e `LocalDBUnShareInstance` da API do LocalDB ou as opções de compartilhamento e descompartilhamento do utilitário `SqlLocalDB`.

## Iniciar o LocalDB e conectar-se ao LocalDB

### Conectar-se à instância automática

A maneira mais fácil de usar o LocalDB é conectar-se à instância automática pertencente ao usuário atual usando a cadeia de conexão `Server=(localdb)\MSSQLLocalDB;Integrated Security=true`. Para se conectar a um banco de dados específico usando o nome do arquivo, se conecte usando uma cadeia de conexão semelhante a `Server=(LocalDB)\MSSQLLocalDB;Integrated Security=true;AttachDbFileName=D:\Data\MyDB1.mdf`.

A convenção de nomenclatura e a cadeia de conexão para o formato LocalDB foram alterados no SQL Server 2014. Anteriormente, o nome da instância era um único caractere v seguido pelo LocalDB e o número de versão. A partir do SQL Server 2014, não há mais suporte para esse formato de nome de instância e a cadeia de conexão mencionada anteriormente deve ser usada.

 Observação

- A primeira vez que o usuário de um computador tenta conectar-se ao LocalDB, a instância automática deve ser criada e iniciada. O tempo adicional para a criação da instância pode causar falha durante a tentativa de conexão e exibir uma mensagem de tempo esgotado. Quando isso acontecer, espere alguns segundos para deixar o processo de criação terminar e conecte novamente.

### Criar e conectar-se a uma instância nomeada

Além da instância automática, o LocalDB também oferece suporte a instâncias nomeadas. Use o programa SqlLocalDB.exe para criar, iniciar e interromper uma instância nomeada do LocalDB. Para obter mais informações sobre o SqlLocalDB.exe, consulte [Utilitário SqlLocalDB](https://docs.microsoft.com/pt-br/sql/tools/sqllocaldb-utility?view=sql-server-ver15).

ConsoleCopiar

```console
REM Create an instance of LocalDB
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1
REM Start the instance of LocalDB
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1
REM Gather information about the instance of LocalDB
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1
```

A última linha acima, retorna informações semelhantes a estas:

| Categoria                    | Valor                                   |
| :--------------------------- | :-------------------------------------- |
| Nome                         | `LocalDBApp1`                           |
| Versão                       | <Current Version>                       |
| Nome compartilhado           | ""                                      |
| Proprietário                 | "<Your Windows User>"                   |
| Criar automaticamente        | Não                                     |
| Estado                       | executando                              |
| Hora da última inicialização | <Date and Time>                         |
| Nome do pipe da instância    | np:\\.\pipe\LOCALDB#F365A78E\tsql\query |

 Observação

Se o aplicativo usar uma versão do .NET anterior à 4.0.2, conecte-se diretamente ao pipe nomeado do LocalDB. O valor do nome do pipe da Instância é o pipe nomeado que a instância do LocalDB está ouvindo. A parte do nome do pipe da instância após LOCALDB# mudará sempre que a instância do LocalDB for iniciada. Para conectar-se à instância do LocalDB usando o SQL Server Management Studio, digite o nome do pipe da instância na caixa **Nome do servidor** da caixa de diálogo **Conectar-se a Mecanismo de Banco de Dados** . Em seu programa personalizado, você pode estabelecer uma conexão com a instância do LocalDB usando uma cadeia de conexão semelhante a `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`

### Para conectar-se a uma instância compartilhada do LocalDB

Para conectar-se a uma instância compartilhada do LocalDB, adicione `\.\` (barra invertida + ponto + barra invertida) à cadeia de conexão para fazer referência ao namespace reservado para instâncias compartilhadas. Por exemplo, para conectar-se a uma instância compartilhada do LocalDB denominada `AppData`, use uma cadeia de conexão como `(localdb)\.\AppData` parte da cadeia de conexão. Um usuário que se conecta a uma instância compartilhada do LocalDB que não pertence a ele deve ter uma Autenticação do Windows ou um logon de Autenticação do SQL Server.

## Solução de problemas

Para saber mais sobre como solucionar problemas do LocalDB, confira [Solucionar problemas do LocalDB do SQL Server 2012 Express](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx).

## Permissões

Uma instância do SQL Server Express LocalDB é criada por um usuário para uso próprio. Qualquer usuário no computador pode criar um banco de dados usando uma instância do LocalDB, armazenando arquivos sob o seu perfil do usuário e executando o processo sob suas credenciais. Por padrão, o acesso à instância do LocalDB é limitado a seu proprietário. Os dados contidos no LocalDB são protegidos pelo acesso de sistema de arquivos aos arquivos de banco de dados. Se os arquivos de banco de dados do usuário estiverem armazenados em um local compartilhado, o banco de dados poderá ser aberto por qualquer pessoa com acesso de sistema de arquivos ao local, usando uma instância de LocalDB de sua propriedade. Se os arquivos de banco de dados estiverem em um local protegido, como a pasta de dados de usuários, somente esse usuário e os administradores com acesso a essa pasta poderão abrir o banco de dados. Os arquivos do LocalDB só podem ser abertos por uma instância do LocalDB de cada vez.

 Observação

O LocalDB sempre é executado sob o contexto de segurança de usuários, ou seja, o LocalDB nunca é executado com credenciais do grupo de Administradores local. Isso significa que todos os arquivos de banco de dados usados por uma instância do LocalDB devem estar acessíveis usando a conta de Windows do usuário proprietário, sem considerar a associação no grupo de Administradores local.

## Consulte Também

[Utilitário SqlLocalDB](https://docs.microsoft.com/pt-br/sql/tools/sqllocaldb-utility?view=sql-server-ver15)