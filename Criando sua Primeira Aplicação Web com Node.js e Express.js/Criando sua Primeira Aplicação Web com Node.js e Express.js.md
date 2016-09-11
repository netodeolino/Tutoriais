# Criando sua Primeira Aplicação Web com Node.js e Express.js (Em Construção)

###Pré-requisitos:###
<ol>
    <li>Node.js</li>
    <li>Express.js</li>
</ol>

<br/>

## PARTE 01 - Criando um novo Projeto ##

Para criar um novo os passos são bastantes simples.

Primeiro execute o comando abaixo e onde está escrito `site` troque pelo nome que deseja dar a seu projeto:
`$ express site --ejs`

Alguns arquivos irão ser cridos, como mostra na imagem abaixo.

![Image 01]()

<br/>

Agora entre no repositório e instale as dependências do projeto com o comando abaixo:
`$ cd site && npm install`

<br/>

A pasta onde seu projeto está localizado vai/ficar ser similar a imagem abaixo:

![Image 02]()

<br/>

## PARTE 02 - Entendendo a Estrutura Básica do Express ##

#### app.js ####

![Image 03]()

Neste arquivo é configurado para nós a maioria dos recursos necessários para o início de um projeto, sendo este simples ou não. Algumas destas configurações são o tamanho da janela da aplicação, o caminho para a primeira tela, dentre outras coisas.

#### index.html ####

![Image 04]()

Este arquivo é a página, ou a tela (uma vez que estamos falando de uma aplicação desktop), inicial da aplicação. Nela você pode criar um design e alguma interação inicial para outras telas usando de recursos como CSS, Bootstrap, dentre outros, como se estivesse criando uma aplicação Web.

#### package.json ####

![Image 05]()

Todas as dependências necessárias que surgirem durante o desenvolvimento do seu projeto você pode instalar por este arquivo executando o comando `npm install`. Por exemplo, suponha que você vá trabalhar com MySQL, então você vem até este arquivo e em "devDependencies" adiciona `"mysql": "*"`, com isto a última versão do MySQL é adicionado na sua pasta `node_modules` e fica disponível para ser usado por você no projeto usando o comando <code>require("mysql");</code>.

#### node_modules ####

![Image 06]()

Nesta pasta ficam instalados todas as dependências do projeto, como por exemplo o MySQL que foi falado no tópico anterior.

<br/>



Agora chegou o momento de brincar um pouco com Electron. Vamos criar um visual mais bonito para a tela inicial da aplicação e criar um cadastro simples usando o banco MySQL. No meu exemplo vou fazer o uso de Bootstrap e JQuery mas os mesmos não são obrigatórios.

<br/>

Primeiro vamos criar duas pastas para que o projeto fique mais organizado e modularizado. As pastas são `public`, onde ficarão os arquivos de CSS e JavaScript, e `views`, onde ficarão as demais telas da aplicação.

![Image 07]()

<br/>

Também é necessário instalar o MySQL para que a conexão com o banco de dados seja possível.
Para instalar o MySQL adicione no arquivo `package.json` a dependência `"mysql": "*"`. O mesmo irá ficar como a imagem abaixo. Posteriormente execute o comando `npm install` para que a dependência enfim seja instalada.

![Image 08]()

<br/>

No arquivo `index.html` vamos criar um formulario de cadastro.

```html
<form role="form" action="" method="post" >
    <div class="col-md-6">
        <div class="form-group">
            <label for="InputName">Nome Completo</label>
            <div class="input-group">
                <input type="text" class="form-control" name="InputName" id="InputName" placeholder="Nome Completo" required>
                    <span class="input-group-addon"><i class="glyphicon glyphicon-ok form-control-feedback"></i></span>
            </div>
        </div>
        <div class="form-group">
            <label for="InputEmail">Seu Email</label>
            <div class="input-group">
                <input type="email" class="form-control" id="InputEmail" name="InputEmail" placeholder="Email" required  >
                    <span class="input-group-addon"><i class="glyphicon glyphicon-ok form-control-feedback"></i></span>
            </div>
        </div>
        <div class="form-group">
            <label for="InputLogin">Seu Login</label>
            <div class="input-group">
                <input type="text" class="form-control" id="InputLogin" name="InputLogin" placeholder="Login" required  >
                    <span class="input-group-addon"><i class="glyphicon glyphicon-ok form-control-feedback"></i></span>
            </div>
        </div>
        <div class="form-group">
            <label for="InputSenha">Sua Senha</label>
            <div class="input-group">
                <input type="password" class="form-control" id="InputSenha" name="InputSenha" placeholder="Senha" required  >
                    <span class="input-group-addon"><i class="glyphicon glyphicon-ok form-control-feedback"></i></span>
            </div>
        </div>
        <button class="btn btn-lg btn-primary btn-block" onclick="realizarCadastro()" type="button">Cadastrar</button>
    </div>
</form>
```

Repare que no fim do formulário, mais precisamente no `button` tem uma chamada à função `realizarCadastro()` quando o botão é clicado. Vai ser essa função que vai realizar alguns procedimentos necessários para que aqueles dados digitados na tela sejam salvos no banco de dados.

> OBSERVAÇÃO: O Bootstrap está sendo utilizado neste formulário.

O próximo passo então é criar um arquivo JavaScript onde iremos implementar a função de cadastro.

Antes de criar o arquivo em si vamos criar as pastas de `CSS` e `JS` (JavaScript) assim como a imagem abaixo.

![Image 09]()

<br/>

Dentro da pasta `js` vamos criar mais duas pastas, são elas `bd`, onde vão ficar os futuros arquivos de configuração do banco, e  `controllers`, onde ficará os arquivos de controle da aplicação.

![Image 10]()

<br/>

Finalmente, dentro de `controllers` vamos criar o arquivo `controller.js` onde irá ser implementado a função de cadastro.

Na imagem abaixo mostro como a função vai ficar.

![Image 11]()

<br/>

Agora vou mostrar o passo-a-passo necessário para que seja possível o cadastro de um usuário.

Primeiro criamos o arquivo de conexão com o banco dentro da pasta `bd` chamado `ConexaoBanco.js`.

![Image 12]()

<br/>

O próximo arquivo irá se chamar `UsuarioDAO.js`. É nele que irá ser implementado todas as funções que irão se comunicar com o banco. Exemplos: Salvar, Deletar, Atualizar, Dentre outros. No nosso exemplo vamos fazer somente o Salvar.

![Image 13]()

<br/>

Para complementar o passo anterior vamos criar o arquivo `Usuario.js` que irá ser o objeto usuário do projeto (Similar ao model do MVC).

![Image 14]()

<br/>

Por último vamos fazer o arquivo e a respectiva função que é chamada na tela inicial (index.html).

![Image 15]()

<br/>

Vamos agora criar a base e uma tabela no banco MySQL.

```sql
create database tutorialelectron;

create table usuario (
    nome varchar(60),
    email varchar(60),
    login varchar(30),
    senha varchar(30)
);
```

No arquivo `index.html` é necessário importar os scripts criados por nós para que todas as funções necessárias funcionem corretamente.

```javascript
	<script src="./public/js/bd/ConexaoBanco.js"></script>
    <script src="./public/js/bd/UsuarioDAO.js"></script>
    <script src="./public/js/bd/cadastroController.js"></script>
    <script src="./public/js/bd/Usuario.js"></script>
	<script src="./public/js/controllers/controller.js"></script>
```

Vamos agora executar nossa aplicação. Para isso execute o comando `npm start`.

![Image 16]()

<br/>

Fazendo um cadastro.

![Image 17]()

![Image 18]()

<br/>

Olhando se deu certo no banco de dados.

![Image 19]()

<br/>

![Image 20]()

<br/>

##FIM!##
Bom, espero que esse tutorial ajude á você a iniciar com seus primeiros projetos com Electron e respectivamente Node.js. Quaisquer dúvidas pode entrar em contato comigo pelo meu email que está na página inicial do meu GitHub. Obrigado e até mais!

####Neto Deolino
<ol>
    <li> http://linkedin.com/in/netodeolino </li>
    <li> http://netodeolino.github.io </li>
</ol>