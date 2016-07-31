# Um tutorial de uma simples aplicação usando Electron

###Pré-requisitos:###
<ol>
    <li>Node.js</li>
    <li>MySQL</li>
</ol>

<br/>

## PARTE 01 - Instalação, Configuração e Entendimento do Projeto ##

Primeiro vamos usar o <b>Quick Start</b> para criar uma aplicação rápida do Electron. Essa aplicação nos fornecerá uma estrutura inicial para o projeto.

Clone o repositório Quick Start:
`$ git clone https://github.com/electron/electron-quick-start`

Entre no repositório:
`$ cd electron-quick-start`

Instale as dependências e Execute pela primeira vez a aplicação:
`$ npm install && npm start`

A instalação das dependências vai ser igual ou similar a imagem abaixo:

![Image 01](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img01.png?raw=true)

<br/>

A execução da aplicação vai ser similar a imagem abaixo:

![Image 02](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img02.png?raw=true)

<br/>

Se analisarmos, alguns arquivos foram baixados no projeto, dentre eles estão `main.js`, `index.html`, `package.json` e a pasta `node_modules`. Vamos falar um pouco sobre cada um deles agora.

#### main.js ####

![Image 03](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img03.png?raw=true)

Neste arquivo é configurado para nós a maioria dos recursos necessários para o início de um projeto, sendo este simples ou não. Algumas destas configurações são o tamanho da janela da aplicação, o caminho para a primeira tela, dentre outras coisas.

#### index.html ####

![Image 04](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img04.png?raw=true)

Este arquivo é a página, ou a tela (uma vez que estamos falando de uma aplicação desktop), inicial da aplicação. Nela você pode criar um design e alguma interação inicial para outras telas usando de recursos como CSS, Bootstrap, dentre outros, como se estivesse criando uma aplicação Web.

#### package.json ####

![Image 05](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img05.png?raw=true)

Todas as dependências necessárias que surgirem durante o desenvolvimento do seu projeto você pode instalar por este arquivo executando o comando `npm install`. Por exemplo, suponha que você vá trabalhar com MySQL, então você vem até este arquivo e em "devDependencies" adiciona `"mysql": "*"`, com isto a última versão do MySQL é adicionado na sua pasta `node_modules` e fica disponível para ser usado por você no projeto usando o comando <code>require("mysql");</code>.

#### node_modules ####

![Image 06](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img06.png?raw=true)

Nesta pasta ficam instalados todas as dependências do projeto, como por exemplo o MySQL que foi falado no tópico anterior.

<br/>

## PARTE 02 - Criando uma aplicação simples ##

Agora chegou o momento de brincar um pouco com Electron. Vamos criar um visual mais bonito para a tela inicial da aplicação e criar um cadastro simples usando o banco MySQL. No meu exemplo vou fazer o uso de Bootstrap e JQuery mas os mesmos não são obrigatórios.

<br/>

Primeiro vamos criar duas pastas para que o projeto fique mais organizado e modularizado. As pastas são `public`, onde ficarão os arquivos de CSS e JavaScript, e `views`, onde ficarão as demais telas da aplicação.

![Image 07](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img07.png?raw=true)

<br/>

Também é necessário instalar o MySQL para que a conexão com o banco de dados seja possível.
Para instalar o MySQL adicione no arquivo `package.json` a dependência `"mysql": "*"`. O mesmo irá ficar como a imagem abaixo. Posteriormente execute o comando `npm install` para que a dependência enfim seja instalada.

![Image 08](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img08.png?raw=true)

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

![Image 09](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img09.png?raw=true)

<br/>

Dentro da pasta `js` vamos criar mais duas pastas, são elas `bd`, onde vão ficar os futuros arquivos de configuração do banco, e  `controllers`, onde ficará os arquivos de controle da aplicação.

![Image 10](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img10.png?raw=true)

<br/>

Finalmente, dentro de `controllers` vamos criar o arquivo `controller.js` onde irá ser implementado a função de cadastro.

Na imagem abaixo mostro como a função vai ficar.

![Image 11](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img11.png?raw=true)

<br/>

Agora vou mostrar o passo-a-passo necessário para que seja possível o cadastro de um usuário.

Primeiro criamos o arquivo de conexão com o banco dentro da pasta `bd` chamado `ConexaoBanco.js`.

![Image 12](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img12.png?raw=true)

<br/>

O próximo arquivo irá se chamar `UsuarioDAO.js`. É nele que irá ser implementado todas as funções que irão se comunicar com o banco. Exemplos: Salvar, Deletar, Atualizar, Dentre outros. No nosso exemplo vamos fazer somente o Salvar.

![Image 13](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img13.png?raw=true)

<br/>

Para complementar o passo anterior vamos criar o arquivo `Usuario.js` que irá ser o objeto usuário do projeto (Similar ao model do MVC).

![Image 14](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img14.png?raw=true)

<br/>

Por último vamos fazer o arquivo e a respectiva função que é chamada na tela inicial (index.html).

![Image 15](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img15.png?raw=true)

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

![Image 16](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img16.png?raw=true)

<br/>

Fazendo um cadastro.

![Image 17](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img17.png?raw=true)

![Image 18](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img18.png?raw=true)

<br/>

Olhando se deu certo no banco de dados.

![Image 19](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20uma%20aplica%C3%A7%C3%A3o%20Desktop%20com%20o%20Electron/Images/img19.png?raw=true)

<br/>

##FIM!##
Bom, espero que esse tutorial ajude á você a iniciar com seus primeiros projetos com Electron e respectivamente Node.js. Quaisquer dúvidas pode entrar em contato comigo pelo meu email que está na página inicial do meu GitHub. Obrigado e até mais!