# Construindo um servidor web com Node.js

## Veja nesse artigo como desenvolver um servidor web com Node.js, tornando comunicações HTTP muito mais rápidas. Conheça também conceitos como escalabilidade, suporte às páginas estáticas e os principais módulos da biblioteca de JavaScript.

[Este Artigo faz parte da RevistaFront-end Magazine 3Ver Revista](https://www.devmedia.com.br/construindo-um-servidor-web-com-node-js/32023#)

Por que eu devo ler este artigo:Com o intuito de apresentar os conceitos e recursos do Node.js, plataforma JavaScript que vem sendo amplamente adotada em projetos que trazem a escalabilidade como importante requisito, neste artigo vamos criar um servidor web simples com suporte a páginas estáticas. Para isso, serão demonstrados alguns módulos padrão da biblioteca, tais como file system e HTTP, e como “pensar orientado a eventos”, fundamento básico da tecnologia em estudo.

Suporte ao alunoAnotarMarcar como concluídoCódigo fonte

[Artigos](https://www.devmedia.com.br/artigos/)[Node.js](https://www.devmedia.com.br/artigos/node-js)Construindo um servidor web com Node.js

**Ao iniciar os trabalhos com [Node.js](https://www.devmedia.com.br/nodejs/)**, rapidamente nota-se que mesmo o mais simples dos códigos acaba viabilizando muitas funcionalidades. Mesmo que você seja iniciante, com poucas linhas de código conseguirá criar aplicações de troca de mensagens entre clientes e servidor, como o exemplo mais clássico de aplicações em tempo real, um chat.

Caso possua experiência em outras tecnologias como [Java](https://www.devmedia.com.br/guia/linguagem-java/38169) ou [PHP](https://www.devmedia.com.br/guia/linguagem-php/38780), pode até pensar que isso não é “algo do outro mundo”, contudo, **o grande diferencial é que o Node.js foi planejado e criado para lidar especificamente com aplicações desse tipo, em rede**. E mais, ele foi projetado para lidar com alta concorrência em tempo real. Com isso, ele é capaz de lidar com milhares de clientes conectados ao mesmo tempo, consumindo pouca memória e exigindo pouco processamento do servidor.

Em se tratando de uma tecnologia voltada para o desenvolvimento de aplicações em rede, **o Node.js foi construído para ser orientado a eventos e I/O não bloqueante, ou seja, a entrada e saída de dados não bloqueiam os processos de execução das aplicações, fazendo com que a concorrência entre vários clientes simultâneos seja mais performática e eficiente**.

Para quem está dando os **primeiros passos com o Node**, pode parecer um pouco confuso já começar com um exemplo de um servidor web, pois este envolve conceitos de rede, cliente, servidor, o protocolo HTTP, etc. Por outro lado, como o Node foi elaborado tendo como base alguns destes conceitos, a maioria das tecnologias mencionadas já são fornecidas e até gerenciadas pelos próprios módulos dele.

<iframe src="https://www.youtube.com/embed/KD2kJetfzas" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="outline: none; -webkit-tap-highlight-color: transparent; max-width: 100%; margin: auto; height: 455.062px; width: 809px;"></iframe>

Saiba mais: [Curso de Node.js: Primeiros passos](https://www.devmedia.com.br/curso/curso-de-node-js-primeiros-passos/1482)

Caso você ainda não esteja familiarizado com esta solução e seu paradigma orientado a eventos, vamos fazer uma rápida revisão.

O Node.js é, basicamente, um combinado do engine JavaScript do Google Chrome, denominado V8, com a utilização de um recurso do sistema operacional que monitora requisições de operações de entrada e saída e que dispara a resposta ao solicitante assim que uma resposta estiver de fato disponível. Em outras palavras, esse monitoramento e, consequentemente, essa resposta, é o que conhecemos popularmente como callback. Cada sistema operacional possui a sua própria implementação desse mecanismo. Em ambientes Unix, por exemplo, esse recurso é chamado de epoll.

Tendo o V8 como engine para interpretar JavaScript e o próprio sistema operacional fornecendo o I/O não bloqueante, restou aos desenvolvedores do Node.js fazerem a junção dessas funcionalidades, agregando a camada de acesso a arquivos, criptografia, rede, e outras features comuns em qualquer linguagem de programação.

### Como funcionará o servidor web

O conceito de um servidor web é relativamente simples. Como qualquer tipo de aplicação que age como um servidor, iniciamos uma socket que fica “escutando” uma determinada porta e que recebe conexões de sockets cliente que desejam trocar informações com este servidor.

Sempre que um servidor é implementado, é preciso definir um protocolo, ou seja, definir a forma como o cliente e o servidor irão se comunicar. Uma das maneiras mais convenientes de se estabelecer essa comunicação entre é definindo comandos para que o cliente solicite informações ao servidor, que por sua vez pode interpretar esses comandos, associando-os a uma função específica, executá-la e devolver uma resposta à solicitação feita pelo cliente.

[Saiba maisSérie **Programe com o Node.js**](https://www.devmedia.com.br/nodejs/)

No caso específico de um servidor web, esse protocolo já existe e já é encapsulado pelo Node.js em sua biblioteca padrão: o protocolo HTTP.

Embora ele facilite a nossa vida, fornecendo uma API completa e cheia de módulos associados, não só para o protocolo HTTP, mas também para uma gama imensa de recursos relacionados a redes, cabe ao desenvolvedor decidir o que fazer com esses recursos, ou seja, fica a seu critério estabelecer como o servidor web deve se comportar, receber e responder as requisições, controlar o acesso através de login, ou a quantidade de conexões simultâneas que ele estará apto a receber. Em outras palavras, o Node fornece as ferramentas “pré-prontas” para que você possa se concentrar nas regras de negócio da aplicação, sem precisar concentrar esforços na implementação de protocolos HTTP e outras particularidades da conexão entre cliente e servidor.

Dito isso, eis o que vamos construir para que nosso servidor web funcione como queremos:

- Definir um diretório */static*, onde ficarão os arquivos providos pelo servidor;
- Dentro do diretório */static* criaremos subdiretórios para separar os arquivos por tipo (js, css, etc.);
- Criar um arquivo *index.js*, que representará o arquivo principal de nossa aplicação;
- Criar um módulo *server.js*, que representará nosso servidor web;
- Criar um módulo filehandler, que será responsável por carregar os arquivos solicitados pelo browser (nosso cliente);
- Criar um arquivo JSON chamado *config.json*, contendo as configurações do servidor web, tais como diretórios padrão, tipos de arquivo, etc.;
- Definir um parâmetro opcional que poderá ser fornecido no momento de iniciar a aplicação, viabilizando alterar o valor da porta na qual o servidor receberá requisições.

### Preparação do ambiente

Como esse artigo tem por objetivo apresentar uma aplicação básica, não utilizaremos módulos de terceiros como Socket.IO. Porém, para propósitos de agilizar o desenvolvimento, vamos baixar, através do npm (**BOX 1**), o nodemon.



**BOX 1.** npm



É um programa que faz parte dos arquivos binários do Node.js. Sua função é baixar e instalar pacotes de módulos para o Node.js criados pela comunidade.



O nodemon é uma solução que executa qualquer aplicação escrita em Node.js e que fica “vigiando” os arquivos desta. Com isso, caso algum arquivo presente no diretório onde o nodemon foi iniciado for alterado, a aplicação é reiniciada automaticamente, o que faz com que não tenhamos que parar a execução de nossa aplicação e reiniciá-la a cada alteração no código.

Além disso, caso a aplicação “quebre”, ela continuará sendo vigiada pelo nodemon, e quando o problema que causou a interrupção da aplicação for corrigido, ou seja, o trecho de código que possuir erros for reparado, ele reiniciará a aplicação automaticamente.

Agora que você tem uma ideia de como utilizar o nodemon para favorecer a agilidade no desenvolvimento de aplicações, vamos executá-lo em nossa aplicação. Para isso, no entanto, precisamos ter algum arquivo para passar como parâmetro na linha de comando.

Esse é um bom momento para criarmos não só o arquivo principal de nossa aplicação, mas também toda a sua estrutura de diretórios. Sendo assim, vamos criar um diretório com o nome que acharmos mais apropriado para a aplicação – por exemplo: *webserver*. A partir desse diretório, crie os demais conforme a **Listagem 1**.

**Listagem 1**. Estrutura de diretórios da aplicação.

```
webserver
  └── static
      ├── css
      ├── image
      └── script
```

Nossa aplicação residirá na raiz do diretório *webserver*. Dentro deste temos o diretório *static*, que será responsável por manter os arquivos solicitados pelo browser através de [requisições HTTP](https://www.devmedia.com.br/etapas-e-tempos-de-requisicoes-http/32618). A partir do diretório *webserver* que acabamos de criar, execute o comando *npm init*. Este comando irá gerar um arquivo de nome *package.json* com informações sobre a aplicação, como: dependências, licença, autor, etc.

Quando o comando *npm init* é executado, ele solicitará algumas informações ao desenvolvedor para preencher adequadamente o *package.json*. Você deverá ver uma tela semelhante à exibida na **Figura 1**. Preencha-as como achar melhor, porém, mantenha a opção *entry point* com o valor padrão *index.js*, pois este será o arquivo principal do servidor web.

![Executando o comando npm init e respondendo às perguntas de inicialização](https://arquivo.devmedia.com.br/revistas/front_end/imagens/edicao3/2/image001.gif)**Figura 1**. Executando o comando npm init e respondendo às perguntas de inicialização.

Caso não possua o *nodemon* instalado, execute o comando *npm install -g nodemon* no seu prompt do Windows ou terminal, caso esteja trabalhando em um ambiente Unix, como Ubuntu ou MacOS. Isso fará com que o *npm* instale o nodemon de maneira global, ou seja, você estará apto a utilizá-lo de qualquer lugar do seu sistema de arquivos.

### Criando os arquivos do servidor web

Agora que já temos o nodemon instalado, vamos criar os arquivos de código para que ele possa executá-los e monitorá-los. Para tanto, a partir do diretório *webserver*, crie os seguintes arquivos:



- *index.js*: Arquivo principal da aplicação, um container que agrupará todos os módulos do sistema;
- *server.js*: Módulo que será responsável pelo servidor web;
- *filehandler.js*: Módulo que será utilizado pelo *server.js* e é responsável por manipular os arquivos solicitados pelo usuário;
- *config.json*: Arquivo de configuração cujos dados serão lidos e utilizados pela aplicação.





Caso esteja em um ambiente Unix, você pode executar o comando *touch index.js server.js filehandler.js config.json* e todos estes arquivos serão criados de uma só vez.



Neste momento seu diretório *webserver* deve possuir a mesma estrutura apresentada na **Listagem 2**.

**Listagem 2**. Estrutura final de diretórios e arquivos da aplicação.

```
webserver
  ├── config.json
  ├── filehandler.js
  ├── index.js
  ├── package.json
  ├── server.js
  └── static
      ├── css
      ├── image
      └── script
```

### O arquivo index.js

O conteúdo do arquivo principal da aplicação, *index.js*, ainda que pequeno, diz bastante coisa sobre o servidor web, pois é a partir dele que faremos a inclusão e utilização de todos os módulos da nossa solução. Sendo assim, é importante entendermos o que está acontecendo em cada linha, pois do ponto de vista da compreensão do código, o *index.js* representa uma visão macro de tudo que nosso servidor web poderá fazer. O seu conteúdo é exposto na **Listagem 3**.

A principal e real função do *index.js* é funcionar como uma espécie de *container*, centralizando a utilização dos módulos, que serão separados por responsabilidades, ou seja, cada módulo será responsável por uma parte do trabalho realizado. Note, contudo, que o arquivo principal não precisa necessariamente “saber” como os módulos fazem seu trabalho. Basta que ele saiba que esses módulos realizam as tarefas que ele precisa.

**Listagem 3**. Conteúdo do arquivo index.js.

```
process.title = 'MyWebServer';
  1. var args = process.argv,
  2.   port = args[2] || 7070,
  3.   webServer = require('./server');
  4.
  5. webServer.listen(port, function() {
  6.   console.log('Server started at port ' + port);
  7. });
```

Na primeira linha, ainda que não seja uma instrução fundamental para a aplicação, modificando o atributo process.title, definimos um nome para o processo do servidor no sistema operacional. Assim, quando você estiver executando sua aplicação em um sistema operacional derivado do Linux, por exemplo, será possível ver o nome do processo, bem como seu id. Um exemplo disso pode ser verificado na **Figura 2**.

![Comando ps demonstrando o nome associado ao processo da aplicação](https://arquivo.devmedia.com.br/revistas/front_end/imagens/edicao3/2/image002.gif)**Figura 2**. Comando ps demonstrando o nome associado ao processo da aplicação.

Na declaração das variáveis vemos o módulo process sendo usado novamente, desta vez para recuperar os argumentos da linha de comando, através do atributo argv. Este objeto (args) é um atributo especial do módulo process que preserva todos os parâmetros passados quando o comando *node* (ou *nodemon*, no nosso caso, já que estamos em fase de desenvolvimento) é executado.

Por motivos de organização do código, criamos uma variável chamada args para armazenarmos uma referência do objeto argv do módulo process. argv funciona como um array, contendo uma lista dos argumentos passados para o programa na linha de comando do prompt do sistema operacional. Seu primeiro elemento representará o executável *node* (ou o *nodemon*, como já explicado). O segundo argumento representará o nome do arquivo sendo executado (no nosso caso o *index.js*), e a partir do terceiro elemento (args[2]) temos os argumentos opcionais da aplicação, que no nosso caso será a porta na qual o servidor deve ser inicializado, caso seja fornecida.

Logo após a declaração do objeto args, armazenamos o primeiro argumento opcional, ou seja, o terceiro elemento de args, assumindo que este é o valor da porta pela qual o servidor web “escutará” por requisições do browser. Caso nenhum argumento seja encontrado, utilizamos o valor padrão 7070.

A terceira e última variável declarada, webServer, é o objeto que representa o servidor web propriamente dito e que discutiremos em breve. Nesse momento basta entendermos com que tipo de conteúdo e como a variável webServer está sendo carregada, o que nos leva à instrução require, do Node.js, que será explicado a seguir.

Para carregar um módulo em uma aplicação, seja ele criado pelo próprio desenvolvedor, seja ele um módulo importado pelo *npm*, como o Socket.IO ou um driver de banco de dados como o MySQL ou MongoDB, ou ainda, um módulo da biblioteca padrão do Node.js, como o módulo fs, é preciso utilizar a instrução require, passando como argumento uma String com o nome do arquivo correspondente ao módulo que queremos usar. Se quisermos carregar um módulo criado por nós, o nome do arquivo precisa começar com o caminho relativo “./” e não é necessário adicionar o prefixo .js ao final. Assim, o require irá carregar o módulo e associá-lo à variável webServer.

Por fim, utilizamos o método listen() do objeto webServer. Este método recebe como argumento a porta na qual o servidor deve receber conexões dos clientes, e como segundo argumento opcional, uma função de callback que será disparada assim que o servidor for iniciado. No nosso caso, a função apenas exibe uma mensagem no console, dizendo que o servidor foi iniciado na porta especificada.

A única dependência do *index.js*, como vocês podem notar, é o módulo importado pelo require, chamado server, ou seja, o arquivo *server.js*, apresentado na **Listagem 4** e encontrado no mesmo diretório do arquivo principal. Este arquivo é o responsável por implementar o servidor web propriamente dito.

**Listagem 4**. Conteúdo do arquivo server.js, implementação do servidor web

```
1. var http = require('http'),
2.   config = require('./config'),
3.   fileHandler = require('./filehandler'),
4.   parse = require('url').parse,
5.   types = config.types,
6.   rootFolder = config.rootFolder,
7.   defaultIndex = config.defaultIndex,
8.   server;
9.
10. module.exports = server = http.createServer();
11.
12. server.on('request', onRequest);
13.
14. function onRequest(req, res) {
15.  var filename = parse(req.url).pathname,
16.      fullPath,
17.      extension;
18.
19.  if(filename === '/') {
20.      filename = defaultIndex;
21.  }
22.
23.  fullPath = rootFolder + filename;
24.  extension = filename.substr(filename.lastIndexOf('.') + 1);
25.
26.  fileHandler(fullPath, function(data) {
27.      res.writeHead(200, {
28.           'Content-Type': types[extension] || 'text/plain',
29.           'Content-Length': data.length
30.      });
31.      res.end(data);
32.
33.  }, function(err) {
34.      res.writeHead(404);
35.      res.end();
36.  });
37. }
```

Nas oito primeiras linhas do *server.js* podemos identificar a inicialização de variáveis e a importação de alguns módulos, como já vimos anteriormente. Contudo, é possível notar algumas peculiaridades em relação à importação do módulo *server.js*, visto no *index.js*.

A primeira coisa a se notar é que, na importação do módulo http, não foi utilizado o caminho relativo “./”. Isso porque, diferente do módulo *server.js* que nós mesmos escrevemos, o módulo http faz parte da biblioteca do Node.js. Para qualquer módulo da API padrão, este deve ser chamado sem a necessidade de se especificar qualquer caminho.

A segunda peculiaridade, ainda que não seja muito visível nesse momento, é a importação do objeto config. Este se trata de um arquivo com a extensão e formato JSON. Isso mesmo, o require é capaz de importar módulos escritos para o Node, assim como pode converter automaticamente arquivos JSON em um objeto literal JavaScript. No contexto de nossa aplicação, isso quer dizer que, assim como alguns programas utilizam arquivos .ini ou .xml para ler configurações do sistema, estamos utilizando um arquivo JSON para essa finalidade. Vamos discutir esse arquivo com mais detalhes mais à frente.

Perceba também, falando ainda sobre a importação de módulos, a importação do método parse(), que pertence ao objeto url, cujo papel é separar cada trecho de qualquer URL e retornar um objeto com cada um deles. Note que, ao invés de importar todo o objeto url, com todos os seus métodos e atributos, importamos apenas o método que precisamos utilizar, semelhante à importação de [métodos no Python](https://www.devmedia.com.br/python-tutorial/33274) ou a utilização de métodos estáticos do Java, ainda que esse último tenha uma filosofia e finalidade bem diferentes.

Além dessas novidades, podemos ver a importação do módulo filehandler e o uso de variáveis para guardar a referência de alguns atributos do objeto config, como o content type do arquivo solicitado, o diretório padrão dos arquivos providos pelo servidor web (rootFolder) e o nome do arquivo padrão quando nenhum arquivo for especificado ao chamar a URL do servidor (defaultIndex).

Na linha 10 usamos module.exports, cujo valor atribuído a ele é exatamente o que o require irá importar, seja lá onde for chamado. module.exports, como o próprio nome sugere, é a maneira como o sistema de módulos do Node.js exporta módulos e outros objetos a partir de algum arquivo, de forma que esses módulos possam ser importados e utilizados por outros módulos da aplicação.

Como na maioria das linguagens de programação, nós acabamos separando nosso código por responsabilidades lógicas, cada qual em um arquivo, classe ou módulo diferentes, para manter a modularidade da aplicação. Isso é geralmente uma boa prática, pois além de mantermos a aplicação organizada em responsabilidades lógicas, esses módulos podem ser reaproveitados por outros trechos do código. Por exemplo, um módulo responsável por se conectar a um banco de dados pode ser construído de forma a se conectar com um ou mais bancos diferentes. Paralelamente a isso, é possível ter vários módulos com propósitos específicos que precisam se conectar a bancos de dados. Logo, não faz sentido replicar esse código em cada um desses módulos, sendo mais interessante importar o módulo que já fornece tal recurso.

No nosso caso, estamos “exportando” a variável server, atribuindo a ela uma instância de nosso servidor web, através do método createServer() do módulo http.

Embora tenhamos escrito essa linha com múltiplas atribuições ao mesmo tempo, com o formato module.exports = server = http.createServer(), visando manter o código mais enxuto, ela pode não ser tão legível, chegando a ser confusa para algumas pessoas. Para contornar esse problema, poderíamos, por exemplo, instanciar o servidor web, atribui-lo à variável server e então, na linha seguinte, atribuir server a module.exports. Você pode atribuir qualquer coisa que quiser ao module.exports, como funções, variáveis e objetos literais.

Na linha 12 podemos observar uma das mais notáveis e significantes características do Node: os tão famosos eventos!

Na maioria dos casos, eventos são passados como o primeiro argumento de uma função, em forma de string contendo seu nome, como por exemplo, “onload”, “onclick”, “request”, ou simplesmente “on”. Uma vez que o nome do evento é fornecido como argumento de uma função, informa-se a função de callback como segundo argumento, representando a ação a ser executada quando o evento passado no primeiro argumento for disparado.

Para facilitar a compreensão, vamos pegar como exemplo o evento click, comumente utilizado em páginas web. Podemos atribuir o evento click a um botão, a um link ou a qualquer outro elemento HTML que quisermos, mas vamos utilizar um botão por ser o exemplo mais natural.

Uma vez que temos a referência a um botão, através da atribuição da instância deste a uma variável como myButton (por exemplo: var myButton = document.querySelector(“#myButton”)), teremos acesso à função addEventListener(), que recebe como argumentos uma String com o nome do evento e uma função, a ser executada sempre que o evento descrito no primeiro argumento for disparado, como: myButton.addEventListener('click', triggerEvent). A partir desse registro, toda vez que o usuário clicar no botão, a função triggerEvent será executada.

O mesmo conceito se aplica a programas escritos com Node.js. Contudo, ao invés de usarmos o método addEventListener() do JavaScript para páginas HTML, temos o método on() do objeto server, que também recebe dois argumentos. O primeiro argumento é uma String com o nome do evento que queremos “escutar” e o segundo argumento é uma função de callback com os argumentos res (*response*) e req (*request*) com a ação a ser realizada a cada vez que o evento for disparado.

No caso da nossa aplicação estamos chamando a função on do objeto server, passando como primeiro argumento o evento request, que é um evento pré-definido pelo servidor HTTP do Node.js, sendo disparado toda vez que uma nova requisição do cliente for enviada ao servidor (o que normalmente ocorre através de um browser).

Para o segundo argumento da função on(), passamos a função onRequest(), declarada na linha 14. Esta corresponde a todas as ações a serem realizadas para cada nova requisição de um cliente. Outra opção seria passar uma função anônima diretamente no segundo argumento. Porém, para manter o código mais didático, este argumento foi declarado com uma *named function*, ou seja, uma função declarada com um nome, podendo ser reusada em outros trechos do código.

A função onRequest() recebe dois argumentos (res e req) e é executada quando o evento request é disparado. O argumento res representa a resposta (*response*) a ser enviada ao cliente, tais como códigos HTTP de erro ou sucesso, e o conteúdo da resposta, como um código HTML a ser interpretado pelo browser, um JSON, XML, uma imagem e assim por diante.

O argumento req (*request*) representa a requisição recebida pelo servidor, enviada pelo cliente. Este objeto possui todas as informações relacionadas ao cliente, tais como IP, informações do browser, que arquivo está sendo solicitado (páginas HTML, imagens, etc.), entre outras informações que precisam ser de conhecimento do servidor.

Na linha 15 utilizamos o método parse() para interpretar o endereço HTTP solicitado pelo browser e transformá-lo em um objeto JSON, para facilitar o manuseio. Quando o endereço é submetido ao método parse(), este retorna um objeto contendo atributos da URL separados convenientemente para que possamos trabalhar com os valores da URL, como pathname, hostname, port, search e outros. No nosso caso utilizaremos o atributo pathname, pois ele contém o caminho e o nome do arquivo solicitado pelo browser. Em seguida, atribuímos o caminho do arquivo à variável filename que, mais tarde, será fornecida ao nosso módulo de leitura de arquivos.

Na linha 19, caso o valor da variável filename seja a string “/”, quer dizer que o usuário não especificou nenhum arquivo ao enviar a requisição ao servidor, o que nos leva a carregar o arquivo padrão, representado pela variável defaultIndex. Lembre-se que defaultIndex possui o valor que foi carregado do arquivo de configuração *config.json*.

Na linha 23 atribuímos à variável fullPath o caminho completo do arquivo solicitado pelo usuário, juntando o conteúdo da variável de configurações rootFolder, que assim como a variável defaultIndex, foi carregada a partir do arquivo de configuração *config.json*, somado ao conteúdo da variável filename, que acabamos de analisar.

Já na linha 24 utilizamos a função substr() do módulo String do JavaScript para capturar apenas a extensão do arquivo solicitado pelo usuário. A partir dessa informação podemos saber qual será o tipo de conteúdo (*Content Type*) a ser entregue ao usuário.

Caso você não esteja familiarizado com o protocolo HTTP, cada arquivo oferecido pelo servidor web é entregue com uma série de outras informações, sendo uma delas o tipo de conteúdo e o seu tamanho em bytes. Isso informa ao browser como ele deve lidar com o arquivo. Por exemplo, se o servidor web informar que o tipo de conteúdo é *text/plain*, o browser saberá que se trata de um texto simples. Por outro lado, se o servidor informar que o tipo de conteúdo é *image/png*, o browser saberá que se trata de uma imagem, e que ele deve tratar o conteúdo como uma imagem e “pintá-la” na tela.

Alguns desses tipos de conteúdo também estão armazenados no arquivo *config.json*, para que possam ser lidos e interpretados pela aplicação, fornecendo o tipo de conteúdo correto de acordo com a solicitação de arquivo feita pelo usuário. Esses tipos de conteúdo foram carregados na variável types, um subobjeto do objeto config. Mais adiante iremos entender a estrutura de dados do arquivo *config.json* e como ele está organizado.

Agora que sabemos qual arquivo devemos carregar para enviar ao usuário e qual é o *content type*, ou seja, com qual tipo de arquivo o browser deve interpretar os dados recebidos, podemos utilizar a função fileHandler() para realizar a tarefa de ler este arquivo do diretório static para nós. Portanto, da linha 26 ao fim do arquivo, podemos ver a função fileHandler(), outro módulo de nossa aplicação cujo conteúdo analisaremos mais à frente.

A função fileHandler() é importada na linha 3 através da instrução require do Node.js. Como verificado, o sistema de exportação e importação de módulos do Node.js pode exportar qualquer coisa, seja essa coisa um objeto, uma variável ou mesmo uma função, como é caso de fileHandler(). Isso serve de exemplo para mostrar que podemos importar diferentes tipos de dados, como quando importamos o módulo server, por exemplo, que é um objeto mais complexo, composto de variáveis e funções.

Assim como *index.js* apenas precisava fazer uso do módulo server, o módulo server apenas precisa saber usar a função fileHandler(), e é por isso que a isolamos em um novo arquivo. Recapitulando o que foi abordado no começo do artigo, lembre-se que dividimos os módulos do sistema em responsabilidades lógicas. Nosso *index.js* é responsável por iniciar a aplicação, servindo como um container da aplicação, e por isso depende do arquivo *server.js* para fazer todo o trabalho associado ao servidor web.

O arquivo *server.js*, por sua vez, é responsável por toda a lógica associada ao servidor web e por interpretar requisições (requests) e respostas (responses) HTTP, porém ele depende de um módulo responsável pela leitura de arquivos, e é aqui que entra a dependência do fileHandler().

A função fileHandler() recebe três argumentos: o caminho completo de onde o arquivo deve ser lido, uma função de callback de sucesso e uma função de callback de erro.

A função de sucesso possui um argumento que representa os dados carregados do arquivo solicitado, e o corpo da função (note que dessa vez utilizamos uma função anônima, para mostrar que você tem liberdade de trabalhar da maneira que achar melhor) utiliza o método writeHead() do objeto res. O primeiro argumento passado a esse método é o código HTTP (200 quer dizer que a resposta está Ok) e o segundo argumento é um objeto com informações do cabeçalho HTTP; no caso, o tipo de conteúdo (*Content-Type*) e o tamanho dos dados em bytes (*Content-length*).

Note que foi usado o formato types[extension] para capturar o valor da extensão do objeto types. Caso não esteja familiarizado com essa notação, em JavaScript é possível recuperar o valor do atributo de um objeto usando-se o ponto seguido do nome do atributo, ou utilizar colchetes envolvendo o nome do atributo entre aspas. Por exemplo: objeto.atributo ou objeto['atributo']. Como capturamos a extensão em forma de string, faz mais sentido utilizar o formato com colchetes, ou seja, types[extension].

Após configurarmos todos os parâmetros a serem enviados no cabeçalho HTTP de volta ao cliente, temos na linha 31 o método end() que encerra a comunicação com o cliente, enviando os dados solicitados. Na linha 33 utilizamos a mesma técnica empregada para enviar o conteúdo solicitado ao cliente; porém, por se tratar de uma função de callback de erro, informamos o código HTTP 404, que quer dizer que o arquivo solicitado não foi encontrado, e o método end() é passado sem qualquer argumento.

Obviamente existem muitos outros códigos HTTP, como 500, 304, 401, entre outros, cada qual com seu significado e interpretado de forma diferente pelo browser.

Agora que entendemos como nosso servidor está funcionando, vamos detalhar o funcionamento da função fileHandler(), utilizada nas últimas linhas deste. A implementação desta função é realizada no arquivo *filehandler.js*,

**Listagem 5**. filehandler.js – responsável por ler os arquivos solicitados pelo cliente.

```
1. var fs = require('fs');
2.
3. module.exports = function(filename, successFn, errorFn) {
4.   fs.readFile(filename, function(err, data) {
5.       if(err) {
6.            errorFn(err);
7.       } else {
8.            successFn(data);
9.       }
10.  });
11. };
```

Com o Node.js é possível exportar qualquer coisa, até mesmo funções, e é justamente uma função que é exportada a partir do arquivo *filehandler.js*.

Na linha 1 importamos o módulo fs (filesystem) da API padrão do Node, e como o próprio nome diz, serve para manipulação de arquivos e diretórios, sendo responsável por quase todo o trabalho de nosso módulo.

Já sabemos o que está acontecendo na linha 3 e já sabemos para que servem os argumentos da função, mas recapitulando rapidamente, temos o nome do arquivo a ser lido, uma função de callback caso a leitura do arquivo ocorra com sucesso e outra função de callback caso a leitura do arquivo falhe.

O único método que usaremos do módulo fs é o readFile(). Este recebe uma string como primeiro argumento, contendo o caminho e nome do arquivo a ser lido, e o segundo argumento é uma função de callback que recebe outros dois argumentos: um objeto de erro e os bytes do arquivo lido, caso a leitura seja bem sucedida.

O simples fato do argumento err possuir alguma informação que represente um valor válido, isto é, o valor da variável for diferente de null, undefined, uma string vazia, 0 ou false, significa que um erro ocorreu, como arquivo não encontrado, acesso negado ou qualquer outro tipo de problema ao recuperar os dados do arquivo solicitado.

Em nosso código, se qualquer erro ocorrer, disparamos a função de callback errorFn(), que deve ser fornecida pelo “usuário” da função filehandler(), no nosso caso, o nosso módulo server. Caso não haja erro, o conteúdo do arquivo é recuperado e passado como argumento à função de callback successFn(), também declarada no módulo server.

Na **Listagem 6** é exibido o conteúdo do arquivo *config.json*.

**Listagem 6**. Conteúdo de config.json – configurações utilizadas pela aplicação.

```
{
       "rootFolder": "./static",
       "defaultIndex": "/index.html",
       "types" : {
           "htm": "text/html",
           "html": "text/html",
           "jpg": "image/jpeg",
           "jpeg": "image/jpeg",
           "png": "image/png",
           "css": "text/css",
           "js": "text/javascript",
           "json": "application/json"
       }
  }
```

O arquivo *config.json* conta com três atributos: rootFolder, defaultIndex e types, referentes às variáveis que carregamos no *server.js*.

Note que, para que possa ser carregado corretamente pelo Node, *config.json* precisa ser um JSON válido, ou seja, deve respeitar as regras de um JSON, expostos a seguir:



- As chaves devem estar entre aspas duplas;
- Os valores que são strings precisam estar entre aspas duplas;
- Os valores numéricos não precisam estar compreendidos entre aspas;
- Os subobjetos devem estar entre chaves;
- As listas devem estar entre colchetes.



O atributo rootFolder contém o caminho a partir de onde o servidor web deve ler arquivos – no nosso caso, o diretório */static*. Já o atributo defaultIndex contém o nome do arquivo padrão, caso o cliente não especifique o arquivo desejado, e o atributo types contém um objeto cujas chaves são extensões de arquivos, como por exemplo, “html”, e o valor para cada chave é o *content type*, como por exemplo, “text/html” como valor da chave “html”. Lembre-se que é através do objeto types que conseguimos saber o *content type* dos arquivos.

Você pode verificar exemplos da utilização do atributo types na linha 28 do arquivo *server.js*, onde isolamos a extensão do arquivo (ex.: html) e, a partir dessa extensão, obtemos o tipo do conteúdo, através da expressão types[extension], onde, na ocasião, extension representa o valor *html*.

Uma vez que você tenha implementado todos os arquivos, podemos executar a aplicação com o comando *nodemon index.js*; ou, se você já havia executado o nodemon desde o começo, pode notar que ele recarrega a aplicação a cada vez que um arquivo é modificado.

Caso tudo ocorra como esperado, você verá uma tela parecida com a mostrada na **Figura 3**.

![Nodemon executando a aplicação](https://arquivo.devmedia.com.br/revistas/front_end/imagens/edicao3/2/image003.gif)**Figura 3**. Nodemon executando a aplicação.

Para ver o resultado de nosso desenvolvimento, basta abrir seu browser e acessar *http://localhost:7070*, preferencialmente, com as ferramentas de desenvolvedor habilitadas na seção de rede. Para isso, no Google Chrome, por exemplo, navegue até o menu *Tools > Developer Tools*, onde teremos acesso a uma porção de informações sobre a página sendo visualizada, bem como os arquivos que foram baixados, tempo de download de cada um, verificar se algum arquivo falhou por qualquer motivo que seja e assim por diante.

Muitas vezes, enquanto estamos desenvolvendo uma aplicação web, pode ocorrer de não termos nenhuma informação visual no browser em si. Porém, mantendo as ferramentas do desenvolvedor habilitadas, temos acesso a muitas informações por trás dos bastidores da comunicação entre browser e servidor web.

Dando continuidade, após ter habilitado as ferramentas do desenvolvedor e acessado a URL do seu servidor, você deverá ver uma tela semelhante à exibida na **Figura 4**.

![Primeiro teste do servidor, com resposta HTTP 404 – arquivo não encontrado](https://arquivo.devmedia.com.br/revistas/front_end/imagens/edicao3/2/image004.gif)**Figura 4**. Primeiro teste do servidor, com resposta HTTP 404 – arquivo não encontrado.

Caso você também tenha visto uma tela em branco com uma informação em vermelho no log de rede, por mais estranho que seja, o servidor web funcionou! Contudo, como não temos nenhum arquivo na pasta *static*, o servidor retornou um erro 404, conforme codificamos no *server.js*, o que é bastante recompensador, porém, frustrante ao mesmo tempo, já que não exibimos nenhum conteúdo no browser.

Para resolver esse problema, vamos criar algum conteúdo a partir da pasta *static*, lembrando que já havíamos criado a estrutura de diretórios dentro dessa pasta. Deste modo, crie o arquivo *index.html* em *static* com o código demonstrado na **Listagem 7**.

**Listagem 7**. Conteúdo da página index.html.

```
<!DOCTYPE html>
  <html>
  <head>
       <link rel="stylesheet" type="text/css" href="css/style.css">
       <title>My web server</title>
  </head>
  <body>
       <h1>Index</h1>
       Go to <a href="teste.html">test</a>
  </body>
  </html>
```

Como você pode notar nesse pequeno arquivo HTML, importamos o estilo *css/style.css* e definimos um link com a famosa tag <a> para outra página HTML, chamada *teste.html*. Nesse momento, se recarregarmos o browser, seremos capazes de visualizar algum conteúdo, que seria todo o conteúdo da página *index.html* que acabamos de criar. Porém, como ainda não criamos o estilo *style.css*, nossa página aparecerá sem nenhuma formatação, como pode ser observado na **Figura 5**. Também, se tentarmos clicar no link, nenhum conteúdo será exibido, pois também ainda não criamos a página *teste.html*.

![Página index.html sem o estilo CSS](https://arquivo.devmedia.com.br/revistas/front_end/imagens/edicao3/2/image005.gif)**Figura 5**. Página index.html sem o estilo CSS.

Agora já é possível ver o conteúdo de *index.html* que, embora não tenhamos especificado ao chamar a URL *http://localhost:7070*, declaramos em nossa aplicação que, na ausência deste, o *index.html* seria automaticamente escolhido pelo servidor web.

Nas ferramentas do desenvolvedor do browser, localizadas na parte inferior do browser, se você acessar a aba de rede, poderá notar que temos o código de sucesso 200, referente ao *index.html*, e um erro 404, referente ao arquivo *style.css*, que ainda não definimos. Para solucionar esse problema, crie o arquivo *style.css* na pasta *css* com o conteúdo da **Listagem 8**.

**Listagem 8**. Conteúdo do arquivo style.css.

```
body {
       font-family: arial, helvetica;
       font-size: 16px;
  }
```

Como pode ser notado, este CSS é um arquivo bem simples, apenas para modificar o estilo da fonte, visto que nosso objetivo aqui é testar o servidor web. Ao carregar a página novamente, você verá algo semelhante ao demonstrado na **Figura 6**.

![Resultado completo do acesso ao servidor web, com o estilo CSS carregado](https://arquivo.devmedia.com.br/revistas/front_end/imagens/edicao3/2/image006.gif)**Figura 6**. Resultado completo do acesso ao servidor web, com o estilo CSS carregado.

Agora que definimos o estilo CSS para nossa página *index.html* e vimos que a página ficou mais bonita, tendo seu texto formatado, resta criar o conteúdo de *teste.html*. Com esta pendência, já sabemos que o link que aponta para *teste.html* irá falhar, então, antes de clicar no link, crie o arquivo *teste.html* na pasta *static*. Seu conteúdo pode ser visualizado na **Listagem 9**.

**Listagem 9**. Arquivo teste.html, chamado por um link da página index.html.

```
<!DOCTYPE html>
  <html>
   <head>
       <title>My test page</title>
       <link rel="stylesheet" type="text/css" href="css/style.css">
   </head>
   <body>
       <h1>Hello world</h1>
       <img src="image/logo.jpg">

       <p>Go back to <a href="index.html">the index page</a>.</p>

       <script type="text/javascript" src="script/app.js"></script>
   </body>
  </html>
```

Note que assim como em *index.html*, a página *teste.html* importa o estilo *style.css.* Porém, além de importar tal arquivo de estilo, para demonstrar que nossa aplicação está pronta para carregar mais tipos de arquivo além de arquivos HTML e CSS, *teste.html* também importa um arquivo JavaScript, do caminho *script/app.js*, e ainda carrega uma imagem (disponível em *image/logo.png*), com a tag <img>.

Para que seja possível carregar a imagem mencionada, copie-a para a pasta *image*. O código do script importado por *teste.html* pode ser visualizado na **Listagem 10**.

**Listagem 10**. Conteúdo do arquivo app.js

```
(function(window) {

       var d = window.document,
           b = d.body,
           bStyle = b.style;
       bStyle.backgroundColor = 'silver';

  }(this));
```

Mais uma vez o arquivo JavaScript é bastante simples, pois serve apenas para testarmos se nosso servidor web está funcionando corretamente. Nesse caso, nosso script pinta o fundo da tela de cinza claro.

Agora que criamos um conteúdo simples para testar as funcionalidades do servidor web, volte ao browser, recarregue a tela e então clique no link para ver se a página de teste funcionou, conforme a **Figura 7**.

![Resultado da exibição da página teste.html](https://arquivo.devmedia.com.br/revistas/front_end/imagens/edicao3/2/image007.gif)**Figura 7**. Resultado da exibição da página teste.html.

Ao constatar que tudo correu bem, nosso teste estará completo e nosso servidor web estará pronto.

Esta é uma aplicação simples em Node.js, porém, que pode não parecer tão simples para iniciantes devido ao número de tecnologias e conhecimentos prévios que o desenvolvedor precisa ter. Além disso, mesmo sendo uma aplicação básica, ela demonstra diversos aspectos e recursos da tecnologia que você utilizará no dia a dia, caso siga em frente com o desenvolvimento com Node.js.

Caso esteja começando ou já teve algum contato inicial básico, uma boa sugestão é prestar bastante atenção nos seguintes pontos: primeiramente, a programação orientada a eventos, que como reforçamos diversas vezes ao decorrer do artigo, é o coração do Node.js; o sistema de carregamento de módulos, observando como exportar e importar corretamente módulos, objetos e funções, conteúdo demonstrado na importação e exportação dos módulos server e fileHandler(); e procure conhecer mais a fundo a biblioteca padrão do Node.js, todos os seus recursos, como as facilidades que economizam a implementação de coisas que já estão prontas, como os módulos *http* e *fs*, conforme abordado no decorrer do nosso estudo.

### Explorando outros recursos do Node.js

Agora que você já tem uma noção da capacidade do Node.js e da quantidade de possibilidades que a tecnologia oferece, tente aprimorar o seu servidor web. Antes disso, no entanto, uma boa sugestão é começar realizando uma cópia de segurança do código desenvolvido. Feito isso, tente deixar o servidor mais sofisticado. Aqui vão algumas sugestões:



- Cadastre novos tipos de conteúdo no *config.json* e verifique se funcionou corretamente;
- Implemente outros códigos HTTP;
- Tente criar um sistema de log utilizando o módulo fs. Pesquise os métodos do módulo na documentação oficial.



Outra sugestão é tentar criar uma aplicação do zero, como um servidor de echo (você envia uma mensagem a um servidor e ele te responde com a mesma mensagem), ou faça experiências no CLI (*Command Line Interface*) do Node.js. Para isso, basta abrir um terminal e digitar o comando *node.* Você verá que o prompt de seu sistema operacional mudará para o CLI do Node.js, onde você pode começar a escrever qualquer código em JavaScript, que é a linguagem natural do Node,js. Para sair do CLI, basta digitar *CTRL+C* duas vezes.

Assim, você notará que o Node.js é uma tecnologia muito divertida de aprender e fácil de testar, e quanto mais você aprende, mais se interessa e acaba se aprofundando nos estudos.

- [Fullstack JavaScript: API RESTful com Node.js e React](https://www.devmedia.com.br/exemplo/fullstack-javascript-api-restful-com-node-js-e-react/89)
- [Documentação do Node.js](https://nodejs.org/en/docs/)

Tecnologias:

- [CSS](https://www.devmedia.com.br/css/)
- [HTML](https://www.devmedia.com.br/html/)
- [JavaScript](https://www.devmedia.com.br/javascript/)
- [Node.js](https://www.devmedia.com.br/node-js/)
- NPM