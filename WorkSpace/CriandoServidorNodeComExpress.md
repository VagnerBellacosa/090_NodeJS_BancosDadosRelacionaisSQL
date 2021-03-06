## Criando Um Servidor Em Node Com Express

Muito se fala sobre utilizar JavaScript para criar servidores de *back-end*, mas afinal, por onde podemos começar? Para exemplo do *post* vou estar utilizando o [NodeJS](https://nodejs.org/en/).

Para quem não conhece, o NodeJS é um interpretador de código JavaScript que funciona no lado no servidor (*back-end*), com isso é possível criar servidores baseando-se apenas em JavaScript, sim, podemos trocar nossos *back’s* escritos em [Java](https://www.java.com/pt_BR/), [PHP](https://secure.php.net/) ou [Ruby](https://www.ruby-lang.org/en/) por NodeJS.

## Instalando o NodeJS

Como a instalação pode estar sendo realizada de diferentes maneiras, baseado no sistema operacional da máquina não irei estar abordando esse assunto (talvez em um *post* específico para isso).

Para realizar a instalação podemos acessar o link: [download](https://nodejs.org/en/download/), escolha o seu sistema operacional e faça o *download*, após a conclusão do *download* prossiga com a instalação.

## Criando nosso primeiro projeto com NodeJS

Agora, se tudo deu certo, já podemos começar a criar nosso primeiro projeto em NodeJS, para exemplo do *post* vamos utilizar o terminal ou *cmd* (no windows).

Para começarmos o nosso primeiro projeto, vamos criar uma pasta em nossa área de trabalho (*desktop*) chamada `meu-primeiro-servidor-nodejs`.

**Obs:** Eu escolhi esse nome apenas para exemplo do *post*, vocês podem estar optando pelo nome que quiserem.

Em seguida, através do terminal, devemos navegar até a pasta criada:

<iframe src="https://asciinema.org/a/urS5iIoeAd1qGDtzVPQw2sm6o/embed?" id="asciicast-iframe-urS5iIoeAd1qGDtzVPQw2sm6o" name="asciicast-iframe-urS5iIoeAd1qGDtzVPQw2sm6o" scrolling="no" allowfullscreen="true" style="box-sizing: border-box; display: inline-block; margin: 0px; max-height: 400px; max-width: 100%; width: 0px; overflow: hidden; border: 0px; float: none; visibility: visible; height: 0px;"></iframe>

Pronto, até o momento estamos dentro de uma pasta chamada `meu-primeiro-servidor-nodejs`, porém, em nenhum momento informamos do que se trata a mesma, e como vocês já devem estar imaginando, o NodeJS não é um Jedi para adivinhar que essa pasta vai ser nosso primeiro projeto.

Mas afinal, o que podemos fazer para transformar essa pasta normal em um projeto Node?

![Técnico da Roma pensativo](https://res.cloudinary.com/mahenrique94/image/upload/v1549719880/tecnico-pensativo-roma_zw1onh.gif)

Para isso devemos executar o comando `npm init`:

<iframe src="https://asciinema.org/a/kR9TwE4hXxo6cug2F89ftAHtu/embed?" id="asciicast-iframe-kR9TwE4hXxo6cug2F89ftAHtu" name="asciicast-iframe-kR9TwE4hXxo6cug2F89ftAHtu" scrolling="no" allowfullscreen="true" style="box-sizing: border-box; display: inline-block; margin: 0px; max-height: 400px; max-width: 100%; width: 0px; overflow: hidden; border: 0px; float: none; visibility: visible; height: 0px;"></iframe>

Veja que informamos apenas a *description* (descrição) e *author* (autor), o resto apenas deixamos o valor padrão que o Node informa e no fim, confirmamos que tudo estava certo.

Tudo certo, mas da onde veio esse tal de `npm`? Pois é, acabei não falando antes pois preferí descrevê-lo apenas no momento do seu uso.

## Conhecendo o gerenciador de pacotes do NodeJS

Assim como o Java possuí o [Maven](https://maven.apache.org/) para gerenciar as dependências de forma ágil dos seus projetos o NodeJS possuí seu próprio gerenciador, o famoso NPM (*Node Package Manager*), com ele conseguimos atualizar dependências ou instalá-las.

Para conferir todas as possibilidades de *download* podemos ver através do seu site: [npm](https://www.npmjs.com/)

## Package.json, o que é isso?

Caso você seja uma pessoa curiosa já deve ter visto que o `npm` criou um arquivo na raiz da nossa pasta chamado `package.json`, mas afinal, para que ele serve? É nele que fica todas as informações do nosso projeto, tais como: nome, versão, palavras chaves, autor, repositório, etc…

```json
{
  "name": "meu-primeiro-servidor-nodejs",
  "version": "1.0.0",
  "description": "Meu primeiro servidor",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Matheus Castiglioni",
  "license": "ISC"
}
```

JSON

Copy

Este é o exemplo do `package.json` criado para o meu projeto.

## Criando o nosso servidor

Agora que já temos nosso projeto criado e configurado, vamos começar a criar nosso servidor, o primeiro passo é criar o arquivo responsável por configurar e subir o servidor, podemos criar um arquivo chamado `servidor.js` na raiz do nosso projeto.

Para subir e configurar o servidor, vamos utilizar um módulo do NodeJS chamado `http`, podemos começar fazendo o `require` (importação) dele:

```js
const http = require("http");
```

JavaScript

Copy

O módulo `http` é responsável por criar e subir um servidor, mas, qual servidor ele irá subir? Sim, até agora não criamos nenhum servidor, como essa é uma tarefa um tanto quanto chata, vamos utilizar um *framework* chamado `Express`, ele facilita muito nossa vida quanto estamos trabalhando com servidores para a *web*.

O primeiro passo, assim como fizemos com o `http` devemos fazer o `require` dele também:

```js
const express = require("express");
```

JavaScript

Copy

Estamos realizando o `require` tanto do `http` quanto do `express`, mas de onde eles estão vindo? Será que existe alguma mágica para eles aparecem em nosso projeto?

![Jogador de Futebol Americano pensativo](https://res.cloudinary.com/mahenrique94/image/upload/v1549719900/pensativo-jogador-futebol-americano_nyl6zy.gif)

Lembra quando falamos sobre o `npm`? Pois é, ele é o responsável por realizar o download de nossas dependências, mas, até agora não informamos elas em nenhum lugar, como podemos fazer isso?

## Baixando dependências

Para realizar o download e instalação de nossas dependências, podemos fazer através do comando `npm install` seguido pelo nome da mesma:

```bash
npm install express --save
```

Bash

Copy

**Poderíamos utilizar um atalho de install para apenas i**

```bash
npm i express --save
```

Bash

Copy

<iframe src="https://asciinema.org/a/vZpaGfSEy4UXigOUjRvzbxLiT/embed?" id="asciicast-iframe-vZpaGfSEy4UXigOUjRvzbxLiT" name="asciicast-iframe-vZpaGfSEy4UXigOUjRvzbxLiT" scrolling="no" allowfullscreen="true" style="box-sizing: border-box; display: inline-block; margin: 0px; max-height: 400px; max-width: 100%; width: 572px; overflow: hidden; border: 0px; float: none; visibility: visible; height: 420px;"></iframe>

Mas afinal, que treco é esse de `--save`? Simples, quando adicionamos o `--save` estamos dizendo para o `npm`:

> Olha npm, baixa e instala para mim a dependência que se chama express e salva ela em nosso package.json

Lembram do `package.json`? Sim, ele é o responsável por manter todas as informações de nosso projeto, reparem agora que ele terá um valor a mais *dependencies* (dependências), onde são informadas todas as dependências que o projeto precisa para rodar.

```json
{
  "name": "meu-primeiro-servidor-nodejs",
  "version": "1.0.0",
  "description": "Meu primeiro servidor",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Matheus Castiglioni",
  "license": "ISC",
  "dependencies": {
    "express": "^4.16.2"
  }
}
```

JSON

Copy

## Conhecendo o node_modules

Se novamente você foi curioso e deu uma olhada na estrutura do nosso projeto, deve ter reparado que foi criado uma pasta chamada **node_modules**, afinal, qual a utilidade dela? É nela que contém os módulos que podem ser importados (ou requerídos através do *require*) para serem utilizados em nosso projeto.

Agora nosso *require* já deve funcionar porque baixamos e instalamos o `express`, não baixamos ou instalamos o `http` porque por padrão ele já vem com o NodeJS.

## Subindo o servidor

Agora que já temos tudo que precisamos vamos de fato subir nosso servidor.

Conforme dito anteriormante, para subir nosso servidor vamos utilizar o módulo do `http`, através dele temos uma função chamada `createServer` onde devemos passar um servidor para ele, mas, quem será nosso servidor? Sim, se você pensou no `express` parabéns, você acertou.

```js
http.createServer(express);
```

JavaScript

Copy

Será que só isso é suficiente para subir nosso servidor?

<iframe src="https://asciinema.org/a/6TPM5rZZeOa4KSh3EQjpJoDKg/embed?" id="asciicast-iframe-6TPM5rZZeOa4KSh3EQjpJoDKg" name="asciicast-iframe-6TPM5rZZeOa4KSh3EQjpJoDKg" scrolling="no" allowfullscreen="true" style="box-sizing: border-box; display: inline-block; margin: 0px; max-height: 400px; max-width: 100%; width: 572px; overflow: hidden; border: 0px; float: none; visibility: visible; height: 420px;"></iframe>

Reparem que através do comando `node` pediso para ele interpretar arquivos JavaScript, passando como argumento (parâmetro) o nome do arquivo. Porque nosso comando executou e já finalizou?

![Servidor rodou e parou](https://res.cloudinary.com/mahenrique94/image/upload/v1549719914/gif-nao-acredito-computador_llvlm1.gif)

O que está acontecendo é que o NodeJS esta interpretando nosso arquivo de forma correta, ele cria o servidor e logo em seguida o derruba, porque não pedimos para o servidor ficar rodando.

## Rodando o servidor

Como podemos fazer para que nosso servidor fique rodando eternamente até o mesmo ser parado? Para isso temos a função `listen` do `http`, ela recebe como primeiro parâmetro a porta que o servidor ficará escutando (aguardando requisições) e como segundo parâmetro devemos passar uma função de *callback* (que será executada após o servidor estiver rodando).

```js
http.createServer(express).listen(3000, () => console.log("Servidor rodando local na porta 3000"));
```

JavaScript

Copy

Vejam que foi passado a porta **3000** para nosso servidor ficar escutando e como segundo parâmetro foi passado uma [arrow function](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Functions/Arrow_functions) responsável apenas por fazer um log nos informando que o servidor está rodando na máquina local na porta 3000.

Nosso arquivo `servidor.js` completo fica da seguinte maneira;

```js
const http = require("http");
const express = require("express");

http.createServer(express).listen(3000, () => console.log("Servidor rodando local na porta 3000"));
```

JavaScript

Copy

Agora quando pedimos para o NodeJS rodar nosso arquivo, teremos a seguinte saída:

<iframe src="https://asciinema.org/a/VkoM3trF6WIJM6gPTn7wFKsOm/embed?" id="asciicast-iframe-VkoM3trF6WIJM6gPTn7wFKsOm" name="asciicast-iframe-VkoM3trF6WIJM6gPTn7wFKsOm" scrolling="no" allowfullscreen="true" style="box-sizing: border-box; display: inline-block; margin: 0px; max-height: 400px; max-width: 100%; width: 572px; overflow: hidden; border: 0px; float: none; visibility: visible; height: 420px;"></iframe>

Reparem que o servidor ficou rodando, para pará-lo eu tive que executar o comando **CTRL+C**.

## Testando o servidor

Pronto, até o momento nosso servidor já esta subindo localmente na porta 3000, vamos testá-lo?

![Testando servidor express](https://res.cloudinary.com/mahenrique94/image/upload/v1549719928/testando-servidor-express_hswhvy.gif)

Ué, porque deu esse erro:

> Cannot GET /

Até o momento criamos e subimos nosso servidor, porém, em qual momento definimos as rotas, ou seja, as URL’s que podemos acessar? Pois é, não definimos, então vamos resolver o problema.

## Definindo a rota de nosso servidor

Para exemplo do *post* vamos definir apenas a rota principal, em outras palavras, a rota raiz, que é acessada quando informamos apenas a porta.

O primeiro passo será criar uma `app`, podemos fazer isso executando uma função que o `express` possuí:

```js
const app = express();
```

JavaScript

Copy

Com isso já temos nossa `app`, agora precisamos configurar nossa primeira rota, para essa necessidade temos a função `.get`, que recebe dois parâmetros, sendo eles: o *path* que será acessado e uma função de *callback* para processar a requisição:

```js
app.get("/", function(req, res) {
    res.send("<h1>Servidor rodando com ExpressJS</h1>");
});
```

JavaScript

Copy

Aqui estamos dizendo:

> Olha Express, quando alguém realizar uma requisição do tipo *get* para a raiz (informando apenas a porta), pegue a resposta (*res*) e envie (*send*) uma tag h1 com o conteúdo “Servidor rodando com ExpressJS”.

Agora por último, na função `createServer` devemos passar agora o `app` e não mais o `express`:

```js
http.createServer(app).listen(3000, () => console.log("Servidor rodando local na porta 3000"));
```

JavaScript

Copy

Nosso arquivo `servidor.js` completo fica com a seguinte estrutura;

```js
const http = require("http");
const express = require("express");
const app = express();

app.get("/", function(req, res) {
    res.send("<h1>Servidor rodando com ExpressJS</h1>");
});

http.createServer(app).listen(3000, () => console.log("Servidor rodando local na porta 3000"));
```

JavaScript

Copy

Agora, vamos testar nosso servidor novamente:

![Testando servidor com rota](https://res.cloudinary.com/mahenrique94/image/upload/v1549719943/testando-servidor-express-com-rota_wrjqlx.gif)

E ta lá, tudo funcionando corretamante \o/

Para mais opções de criação de rota, confira a [documentação de roteamento](http://expressjs.com/pt-br/guide/routing.html)

O projeto de exemplo pode ser encontrado [aqui](https://github.com/mahenrique94/meu-primeiro-servidor-nodejs).