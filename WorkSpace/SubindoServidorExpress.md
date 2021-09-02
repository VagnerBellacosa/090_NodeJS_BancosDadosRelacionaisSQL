# Subindo servidor com Express

[![Felipe Batista](https://miro.medium.com/fit/c/56/56/1*jHnXLkz_R7g4Zq_xocX9tQ.jpeg)](https://medium.com/@febatista107?source=post_page-----a1868795e366-----------------------------------)

[Felipe Batista](https://medium.com/@febatista107?source=post_page-----a1868795e366-----------------------------------) - [Apr 15, 2018·7 min read](https://medium.com/@febatista107/subindo-servidor-com-express-a1868795e366?source=post_page-----a1868795e366-----------------------------------)



![img](https://miro.medium.com/max/11014/1*xAFAiAxqZVrOVLBTo9tf6w.jpeg)

No último post, falei um pouco sobre [como instalar o Node.js](https://medium.com/@febatista107/preparando-o-ambiente-para-o-node-js-3dd43dce0280) e conhecemos o nvm, um gerenciador de versões que nos ajudou bastante no processo de instalação da plataforma.

E, agora que já temos o Node.js instalado, podemos começar a trabalhar no nosso projeto.

## Que projeto?

Nosso objetivo é desenvolver um aplicativo semelhante ao Instagram, com cadastro de usuário, postagem de fotos e outras funcionalidades que essa aplicação famosa possui.

Mas, como as telas ainda estão nas mãos do designer, vamos começar a trabalhar no server-side do projeto. E, para desacoplar o front-end do back-end, vamos desenvolver uma API que poderá ser consumida por qualquer aplicação cliente.

# Então… Por onde começamos?

Antes de qualquer coisa, é sempre bom criar uma pastinha para o projeto, para deixar as coisas mais organizadas. Por isso, tenho um diretório no meu Desktop, chamado *pixel-api.*

![img](https://miro.medium.com/max/60/1*Ne-OVvj0ADKj-puj-VRGcQ.png?q=20)

![img](https://miro.medium.com/max/630/1*Ne-OVvj0ADKj-puj-VRGcQ.png)

Diretório do projeto

Dentro dessa pasta, vamos criar um novo arquivo chamado *index.js*, que será o ponto de entrada do nosso projeto. E, para a felicidade de todos, vamos começar a codar!

O editor que usarei durante toda a série, e que uso no meu dia-a-dia, é o Visual Studio Code, mas sinta-se a vontade para usar o de sua preferência. Ou, caso tenha acesso, você pode usar uma IDE, como o Web Storm, que recomendo bastante por sinal.

# O módulo http

Vamos colocar a mão na massa! O Node.js possui, por padrão, um módulo chamado *http*, que, como o próprio nome já diz, serve para lidar com questões do protocolo HTTP.

Como ele é um módulo, para conseguirmos usá-lo, temos que importá-lo. Para isso, usaremos a função *require*, do Javascript. Nossa primeira linha de código ficará assim.

```
var http = require('http')
```

## Criando o servidor

Agora que temos o módulo, queremos criar um servidor. Justamente para isso que o *http* possui um método chamado *createServer*.

Esse método recebe uma função de *callback*, que será executada sempre que uma requisição for feita para nosso servidor. E o *callback*, por sua vez, recebe dois parâmetros: o *request*, que possui informações sobre a requisição, e o *response*, que usaremos para responder as requisições.

```
var http = require('http')var server = http.createServer(function(request, response) {
  console.log('Request!')
})
```

## Rodando o servidor

Já temos o servidor configurado, que deverá exibir uma mensagem no console sempre que for acessado. Porém, ele ainda não está ouvindo as requisições. Portanto, vamos chamar o método *listen*, passando o número da porta onde queremos que o servidor rode.

```
var http = require('http')var server = http.createServer(function(request, response) {
  console.log('Request!')
})server.listen(3000)
```

Já podemos testar nosso código. Para isso, basta abrir seu terminal, navegar até o diretório do projeto e rodar o seguinte comando.

```
node index.js
```

Se nenhum erro for acusado, podemos abrir o navegador e fazer uma requisição para *localhost:3000*.

![img](https://miro.medium.com/max/60/1*6f103TQwCFBnGlji37IH0w.png?q=20)

![img](https://miro.medium.com/max/630/1*6f103TQwCFBnGlji37IH0w.png)

Requisição para o servidor

Ao fazer isso, a mensagem “Request!” deverá surgir no seu console.

![img](https://miro.medium.com/max/60/1*NrtncUmkSywHn2yaFp-nGQ.png?q=20)

![img](https://miro.medium.com/max/630/1*NrtncUmkSywHn2yaFp-nGQ.png)

Mensagem no console

# E as tais rotas?

Pois é. Qualquer API trabalha com rotas, que são os endereços que usamos para acessar um recurso específico. É através das rotas que o servidor sabe o que você está esperando como resposta para sua requisição.

Portanto, vamos sim configurar rotas no nosso servidor.

## Mas como?

Lembra do request? Então… Ele possui um atributo chamado *url*, que podemos usar para saber qual rota está sendo requisitada. Uma maneira de fazer isso é com os *ifs*.

```
var http = require('http')var server = http.createServer(function(request, response) {
  if(request.url = '/teste') {
    console.log('Rota de teste!')
  } else {
    console.log('Rota padrão!')
  }
})server.listen(3000)
```

Vamos parar o Node.js, com *Ctrl+C* no terminal, e rodá-lo novamente. Agora, no navegador, podemos fazer uma requisição para *localhost:3000/teste* e teremos o seguinte resultado.

![img](https://miro.medium.com/max/60/1*XkbKKNpO89KUm6v_iGvtnA.png?q=20)

![img]()

Mensagem da rota de teste

E, se fizermos outra requisição, mas desta vez para *localhost:3000* apenas, teremos o seguinte resultado.

![img](https://miro.medium.com/max/60/1*xO_B-tORiQ1r0t9IPlx71g.png?q=20)

![img]()

Mensagem da rota padrão

## Funcionou, certo?

Até funciona, mas percebe o problema dessa implementação? Usamos *ifs* para diferenciar as rotas. Isso pode não parecer um problema agora, mas imagine configurar dezenas de rotas usando *ifs*. Nem um pouco divertido, né?

Além de não nos permitir modularizar muito nosso projeto, já que todas as rotas tem que ser configuradas no arquivo *index.js*.

Essa parece ser uma situação bastante comum no mundo do desenvolvimento, certo? Será que não existe um módulo para resolver nosso problema?

# O módulo Express

Sim! Existem módulos para lidar com configurações de servidor e rotas. Um dos mais famosos é o [Express](http://expressjs.com/), que é tão completo que chega a ser um framework.

Mas relaxa, ele é super simples e minimalista, o que o torna uma ótima opção, pois se integra muito fácil com outros módulos. E o que mais vamos usar nesse projeto é módulo.

## Preparando o projeto

Antes de instalar qualquer módulo e sair usando, é importante preparar o diretório do projeto para receber esses módulos. Basicamente o que temos fazer é criar o arquivo *package.json*, que irá conter algumas informações sobre o projeto.

Para isso, basta abrir o terminal, navegar até a pasta do projeto e chamar o npm para criar o arquivo para nós.

```
npm init
```

Após rodar o comando acima, o npm irá nos fazer algumas perguntas, mas não se preocupe com isso agora, é só apertar *Enter* até o arquivo ser gerado.

![img](https://miro.medium.com/max/60/1*WFAdQIXTyf67vK4i8YogAg.png?q=20)

![img](https://miro.medium.com/max/630/1*WFAdQIXTyf67vK4i8YogAg.png)

Arquivo package.json

## Mas e o Express?

Agora sim, podemos instalar o módulo e, para isso, vamos usar outro comando do npm.

```
npm install --save express
```

Como o Express será uma dependência do nosso projeto, usamos o parâmetro `--save` para adicioná-lo em nosso arquivo *package.json*.

![img](https://miro.medium.com/max/60/1*kem5K2GskBNRExCbpTt6aw.png?q=20)

![img](https://miro.medium.com/max/630/1*kem5K2GskBNRExCbpTt6aw.png)

Arquivo package.json com dependência

## Usando o Express

Já podemos usar o Express! Portanto, vamos apagar todo o código do arquivo *index.js*, já que não vamos mais usar o módulo *http*. Ao invés disso, vamos importar o Express, da mesma forma que fizemos com o módulo anterior.

```
var express = require('express')
```

Também vamos criar uma variável para representar a porta.

```
var express = require('express')
var port = 3000
```

Em seguida, a partir do *express*, vamos criar a variável *app*, que irá representar nossa aplicação.

```
var express = require('express')
var port = 3000var app = express()
```

## Configurando rota padrão

Agora, vamos configurar a rota padrão do servidor, chamando o método *get,* passando a rota e uma função de *callback*, que será executada ao requisitarmos essa rota.

```
var express = require('express')
var port = 3000var app = express()app.get('/', function(req, res) {
  console.log('Rota padrão!')
})
```

Dentro da função de *callback* da rota, vamos usar o *res* para devolver um *json* como resposta da requisição.

```
var express = require('express')
var port = 3000var app = express()app.get('/', function(req, res) {
  res.json({status: 'Server is running!'})
})
```

Por fim, vamos subir o servidor na porta definida, usando o método *listen*, passando a porta e uma função de *callback*.

```
var express = require('express')
var port = 3000var app = express()app.get('/', function(req, res) {
  res.json({status: 'Server is running!'})
})app.listen(port, function() {
  console.log(`Server is running at localhost:${port}`)
})
```

## Tudo pronto?!

Pronto! Já podemos testar o que fizemos até aqui, rodando o Node.js novamente.

```
node index.js
```

Se tudo correr como o desejado, teremos o seguinte resultado no console.

![img](https://miro.medium.com/max/60/1*pyY9l9WupZQILagLgmAm_w.png?q=20)

![img](https://miro.medium.com/max/630/1*pyY9l9WupZQILagLgmAm_w.png)

Mensagem no console

E ao abrir o navegador e chamar o endereço *localhost:3000*, temos o seguinte resultado.

![img](https://miro.medium.com/max/60/1*NWFJpUxisBic13HG7hJZ5A.png?q=20)

![img](https://miro.medium.com/max/630/1*NWFJpUxisBic13HG7hJZ5A.png)

Resposta do servidor

## Eaí, o que achou?

O legal dessa abordagem é que para cada rota temos uma função de *callback* específico. Isso facilita o processo de desenvolvimento, já que não precisamos mais de *ifs* para diferenciar rotas, e nos permite modularizar o projeto, separando as rotas em arquivos diferentes, o que veremos em um post futuro.

Claro que, tudo o que vimos hoje é apenas o básico do Express. E sim, ainda tem bastante coisa para vermos sobre esse carinha e, durante toda a série de posts sobre Node.js, ainda vamos ouvir falar muito sobre ele.

Ficou alguma dúvida? Esqueci de comentar algo extremamente importante? Tem alguma crítica? Se a resposta para alguma dessas perguntas for sim, sinta-se a vontade para deixar um comentário. Eaí, te vejo semana que vem?

[Felipe Batista](https://medium.com/@febatista107?source=post_sidebar--------------------------post_sidebar--------------)

