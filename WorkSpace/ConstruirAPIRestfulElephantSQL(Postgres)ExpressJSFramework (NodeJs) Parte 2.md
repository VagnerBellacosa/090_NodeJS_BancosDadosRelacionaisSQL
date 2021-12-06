# Construir uma API Restful com Elephant SQL (Postgres) e Express JS Framework (NodeJs) Parte 2



![img](https://ichi.pro/assets/images/max/724/1*2YxANymr5luxc2_SSGKd_w.png)

Esta é a segunda parte da construção de uma API tranquila com ExpressJs e Postgres. Na primeira parte, lançamos a base e escrevemos nossa primeira API. Você pode encontrar o primeiro artigo aqui .

Nesta segunda parte, conectaremos nosso banco de dados SQL elefante ao nosso projeto e escreveremos nossos métodos de inscrição e login.

# Conecte seu banco de dados

Copie o URL do seu banco de dados do elefante SQL e cole-o no arquivo .env que você criou assim



```
DATABASE_URL= ***

      
```





```
import dotenv from 'dotenv';
dotenv.config();
export default {
database_url: process.env.DATABASE_URL,
}
```



Em pool.js, copie o seguinte



```
import { Pool } from 'pg';
import dotenv from 'dotenv';
dotenv.config();
const databaseConfig = { connectionString: process.env.DATABASE_URL };
const pool = new Pool(databaseConfig);
export default pool;
```





```
import pool from "./pool";
export default {
/**
*  Query DB
* @param {object} req
* @param {object} res
* @returns {object} object
*/
query(queryText, params){
return new Promise((resolve, reject) =>{
pool.query(queryText, params)
.then((res) => {
resolve(res);
}).catch((err) => {
reject(err);
});
});
}
};
```





```
import pool from './pool';
//POOL CONNECT
pool.on('connect', () => {
console.log('connected to database');
});
//CREATE USER TABLE
const createUserTable = () => {
const userCreateQuery = `CREATE TABLE IF NOT EXISTS users
(id SERIAL PRIMARY KEY,
email VARCHAR(100) UNIQUE NOT NULL,
name VARCHAR(100) NOT NULL,
password VARCHAR(100) NOT NULL,
created_on DATE NOT NULL)`;
pool.query(userCreateQuery)
.then((res) => {
console.log(res);
pool.end();
})
.catch((err) => {
console.log(err);
pool.end();
});
};
//DROP USER TABLE
const dropUserTable = () => {
const userDropQuery = 'DROP TABLE IF EXISTS users';
pool.query(userDropQuery)
.then((res) => {
console.log(res);
pool.end();
})
.catch((err) => {
console.log(err);
pool.end();
});
}
pool.on('remove', () => {
console.log('client removed');
process.exit(0);
});
export {
createUserTable,
dropUserTable,
};
require('make-runnable');
```





```
“create-tables”: “babel-node ./models/migration createUserTable”
```



![img](https://ichi.pro/assets/images/max/724/1*xNmOj9PU-SXgpND1Kwqd5A.png)arquivo package.json

Agora no seu terminal, execute npm run create-tables

![img](https://ichi.pro/assets/images/max/724/1*Jnj38WQIC7VbRBB4seD2Dw.png)npm executar criar tabelas

Se tudo estiver correto, você deve obter o acima.

Ufa, percorremos um longo caminho. Aqui está um copo de água gelada para um bom trabalho.

O que fizemos lá foi criar nossa estrutura de tabela no elefante SQL. Importamos o objeto pool de 'pg' para conectar ao nosso banco de dados (em pool.js). Os métodos createUserTable e dropUserTable em migration.js são usados para criar e deletar tabelas de usuário em nosso banco de dados, respectivamente.

Agora é hora de configurar nossos ajudantes.

# Ajudantes

Nossos ajudantes incluem código reutilizável, como validação e geração userToken, você pode encontrar o código aqui => https://github.com/debbsefe/ExpressApi/tree/master/helpers

# Autenticação

Nossa autenticação incluirá um método para verificar um userToken. O método userToken é gerado usando Jwt, email, senha, id e a chave secreta em nosso arquivo .env. Você pode encontrar o código aqui =>https://github.com/debbsefe/ExpressApi/tree/master/auth

# Controlador

Nosso controlador inclui dois métodos, um para login e outro para inscrição. O método de inscrição verifica se todos os parâmetros (email, senha, nome) enviados no corpo são válidos e também se o email já existe. Se existir, uma mensagem de erro será retornada. Caso contrário, a conta do usuário é criada com sucesso.

O método de login leva o e-mail e a senha como corpo e verifica se a senha está correta. Se estiver correto, o usuário foi conectado com sucesso. Porém, se o e-mail não existir no banco de dados, uma mensagem de erro será enviada.



Você pode encontrar o código para ambos os métodos aqui => https://github.com/debbsefe/ExpressApi/tree/master/controllers

# Rotas

Finalmente, configuramos as rotas para nosso controlador na pasta de rotas. Importamos expresso e nossos controladores. Uma variável de roteador é declarada para representar o roteador expresso. Verifique se o token está incluído na rota de login como autenticação, isso significa que um usuário sem um token não pode fazer login.

Encontre o código aqui =>https://github.com/debbsefe/ExpressApi/tree/master/routes

Além disso, não se esqueça de importar suas rotas em seu app.js. Você pode encontrar o arquivo atualizado aqui =>https://github.com/debbsefe/ExpressApi/blob/master/app.js

Por fim, agora podemos testar nossos endpoints com Postman ou um navegador, inicie seu aplicativo executando



```
npm run dev
```



![img](https://ichi.pro/assets/images/max/724/1*q1dTMm9sZlDP08seUejg1A.png)inscrição de carteiro

![img](https://ichi.pro/assets/images/max/724/1*Oso1Yqe8YNQJJoU3-k5uzQ.png)carteiro assinando

E é isso! Chegamos ao final deste artigo.

Você pode encontrar o código de todo o artigo aqui => https://github.com/debbsefe/ExpressApi