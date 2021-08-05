# :coffee: Tutorial JavaEE
https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white
## :boom: Instalando e Configurando o Ambiente de Desenvolvimento de Aplicações Web
- Antes de prosseguir tenha previamente instalado o SGBD (Sistema de Gerenciamento de Banco de Dados) MySql

- Instale o Netbeans 8.2 com plugin JavaEE

- Dowload da versão 10 do WildFly no site http://wildfly.org/
- Descompacte e armazene em um diretório de sua escolha (ex: WildFly10) no drive C

- Dentro da pasta do WildFly10 crie um arquivo .bat para facilitar o start do server

- Defina o script `WildFly10/iniciar-servidor.bat`
<pre>
    cd bin
    standalone.bat --server-config=standalone-full.xml -b 0.0.0.0
</pre>

Por alguns relatos de problemas com a porta padrão, altere a porta no arquivo de configuração do WildFly de 9990 para 9991 (`WildFly10/standalone/configuration/standalone-full.xml`)
~~~xml
   <socket-binding name="management-http" interface="management" port="${jboss.management.http.port:9991}"/>
~~~

 No arquivo `WildFly10/domain/configuration/host.xml`
 ~~~xml
    <socket interface="management" port="${jboss.management.http.port:9991}"/>
 ~~~

Configure o WildFly como o servidor de aplicações do NetBeans
 - NetBeans : Ferramentas → Servidores → Adicionar Servidor
 - Selecione o WildFly
 - Localize o diretório do WildFly
 - Altere a porta para 9991

## :round_pushpin: Acesso ao WildFly
ative o WildFly e execute seu console no navegador → localhost:/9991

Na primeira vez, será necessário cadastrar um nome de usuário e uma senha, acesse `wildfly10/bin` execute o arquivo add-user.bat e siga os passos adicionando usuário e senha

## :rocket: Executando a aplicação
Crie a table:
~~~sql
    CREATE TABLE Filmes(
    Sequencial int(11) NOT NULL PRIMARY KEY AUTO_INCREMENT,
    Titulo varchar(100) NOT NULL,
    Diretor varchar(100) NOT NULL,
    Ano varchar(100) NOT NULL,
    Genero varchar(100) NOT NULL,
    OscarMelhorFilme varchar(100) NOT NULL
    );
~~~

 Foi utilizado o conector mysql-connector-java-5.1.39-bin.jar
 - Copie o .jar para dentro de `wildfly10/standalone/deployments`
 - Ative o servidor de aplicações WildFly (script iniciar-servidor.bat)
 - Aguarde a inicialização do WildFly até visualizar uma mensagem finalizando com o texto "<i>services are lazy, passive or on-demand</i>"

Gere a versão executável da aplicação web
 - NetBeans : Executar → Limpar e Construir Projeto
 - Distribua o executável de seu projeto no servidor de aplicações
 - Copie o arquivo com extensão war (Web application Archive) gerado no subdiretório dist (distribution) do seu projeto para o diretório `WildFly10/standalone/deployments`

Abra o navegador e execute o seu projeto
 - localhost:/8080/ClubeCinema

OBS: para qualquer alteração no seu projeto gere novamente o arquivo war e repita o processo de distribuição e execução

## :camera: Prints da Aplicação
<hr>
<img alt="tela" src="https://ik.imagekit.io/cleber/filmes-cadastrados_nu1byTdjc.PNG?updatedAt=1628131892724">

<hr>
<img alt="tela" src="https://ik.imagekit.io/cleber/cadastro-filmes_wfFOsDRCb.PNG?updatedAt=1628131892657">

<hr>
<img alt="tela" src="https://ik.imagekit.io/cleber/pesquisar_vEgg3VTHxH.PNG?updatedAt=1628131892713">

