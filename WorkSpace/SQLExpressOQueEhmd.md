# sql express o que é?

Gostaria de saber o que é SQL EXPRESS e para que serve?

 

Venho tendo inúmeros travamentos no windows 7 ultimate conforme o visualizador de eventos vem informando. São tantos seguidos um atrás do outro que trava o sistema e preciso reiniciar várias vezes, pois, trava até mesmo a inicialização do sistema.

Nos serviços do windows está configurado da seguinte forma:

SERVIÇO:                    INICIALIZAÇÃO:

SQL ACTIVE DIRECTORY:       MANUAL

SQL SERVER(EXPRESS):       AUTOMÁTICO

SQL SERVER AGENT:          MANUAL

SQL SERVER BROWSER:       MANUAL

SQL SERVER VSS WRITER:      AUTOMÁTICO

 

OBS: SOU UM USUÁRIO QUE USO O COMPUTADOR SOMENTE PARA: ASSISITR, CRIAR E EDITAR VIDEOS, JOGOS e INTERNET. NÃO USO MEU PC COMO SERVIDOR OU COISA PARECIDA APESAR DE TER TRÊS PCS EM CASA.

 

SE NÃO TIVER UTILIDADE PARA MIM, POSSO DESINTALAR AS ATUALIZAÇÕES DO SQL(TODAS) QUE FORAM BAIXADAS AUTOMATICAMENTE PELO WINDOWS UPDATE?

 

 Esta conversa está bloqueada. Você pode acompanhar a pergunta ou votar, mas não pode responder a esta conversa.

 

Tenho a mesma pergunta (0)

 

Inscrever

 

|

 

Relatar abuso

![Resposta](https://answers.microsoft.com/static/images/answerIconInverted.svg) 

Resposta

![Anderson Pedrosa](https://filestore.community.support.microsoft.com/api/profileimages/81fcafa0-8d19-41e4-81c4-0dc521c3e531)

[Anderson Pedrosa](https://answers.microsoft.com/pt-br/profile/81fcafa0-8d19-41e4-81c4-0dc521c3e531)

Respondido em maio 30, 2012

Olá Alxmsp,

 

O SQL é um banco de dados relacional usado para armazenar e gerenciar algumas informações que são criadas em determinados programas que estão no seu computador de forma ordenada.

Por mais que não use o computador como um servidor programas como o Outlook poder necessitar do SQL, por conta disso não é recomendado que você o exclua do computador.

 

Recomendo que você tente desabilitar os programas que iniciam junto com o Windows para identificar qual pode ser o causador desses travamentos.

 

Para isso siga os procedimentos abaixo:

 

\- Clique em iniciar

\- Iniciar pesquisa. Digite: MSCONFIG e clique em Enter.

![Imagem](https://filestore.community.support.microsoft.com/api/images/ext?url=https%3a%2f%2fpublic.sn2.livefilestore.com%2fy1pJUDbY_gcW_z5HhEeczv3adR-EAq1whhfJs9jv-zPczr1Pc7t5z6xfMl2Ar-gIpxSJBTRTW6QvKYw__4tRStLJg%2fAbrir%2520msconfig.png%3fpsid%3d1)

\- Na guia Serviços, ocultar os serviços Microsoft e desativar tudo.

![Imagem](https://filestore.community.support.microsoft.com/api/images/ext?url=https%3a%2f%2fpublic.sn2.livefilestore.com%2fy1pm2EyF4GaTUM3Kj-445yg6XAkpfeXF0r-sG_qMe7-nBb-RLcIpW2OdsoBD5EsrQjKHklaVemKkmS8DNvAQcX38w%2fServi%25C3%25A7os_DesativarTudo.png%3fpsid%3d1)

\- Na guia Inicialização de Programas, desativar tudo.

![Imagem](https://filestore.community.support.microsoft.com/api/images/ext?url=https%3a%2f%2fpublic.sn2.livefilestore.com%2fy1pzlOb3l5H4pfNC2EdG4_srwKXVAI84UkfIFBtNRv9HkkFEQgAL1T5uXMcUtj-zEhhW986WLyGhhd6skFeXuWrvA%2fProgramas_DesativarTudo.png%3fpsid%3d1)

\- Será apresentado uma nova janela, clique em Reiniciar.

![Imagem](https://filestore.community.support.microsoft.com/api/images/ext?url=https%3a%2f%2fpublic.sn2.livefilestore.com%2fy1pER6rt2GldZeyCGR6Oryp5qC4gYm5-z-7Qo9vqeyfQ7yHog0T61gIsHUtt_UDwVnGASQoM6BbjPNfRcxomI1Vmg%2fReiniciar.png%3fpsid%3d1)

(OBS: Este procedimento desabilita todos serviços e programas de terceiros, bem como logon por fingerprint, antivírus dentre outros. Você pode posteriormente, se o problema for solucionado desta forma, habilitar os programas e serviços que serão inicializados com o Windows, seletivamente, ao invés de manter todos desativados. Efetue este procedimento para não ficar sem proteção antivírus por exemplo. Se o problema voltar após ativação da inicialização de um serviço ou programa em especifico, o problema está exatamente na inicialização deste software e é recomendável removê-lo.)

 