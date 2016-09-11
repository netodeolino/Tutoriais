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

Neste arquivo é configurado, praticamente, todos os recursos necessários para o projeto, sendo este simples ou não. Algumas destas configurações são rotas, favicon do website, sessão, dentre outras coisas.

#### package.json ####

![Image 04]()

Todas as dependências necessárias que surgirem durante o desenvolvimento do seu projeto você pode instalar por este arquivo executando o comando `npm install`. Por exemplo, suponha que você vá trabalhar com MySQL, então você vem até este arquivo e em "dependencies" adiciona `"mysql": "*"`, com isto a última versão do MySQL é adicionado na sua pasta `node_modules` e fica disponível para ser usado por você no projeto usando o comando <code>require("mysql");</code>.

#### index.ejs ####

![Image 05]()

Este arquivo é a página inicial do website, mas você pode adicionar uma outra em teu local alterando o valor de `response` ou `res` no index.js, mas geralmente é o mesmo não é alterado.


#### style.css ####

![Image 06]()

É o arquivo CSS que já vem como padrão quando criamos o projeto, mas assim como o `index.ejs` o mesmo pode ser alterado e, inclusive, ser adicionado vários outros.

<br/>

## PARTE 03 - Fazendo o Upload de uma Imagem ##

Agora chegou o momento de brincar um pouco com Express. Neste tutorial vou dar um exemplo de uso de Express não tão comum (digamos assim). Vou mostrar a vocês como fazer o upload de imagens e espero que consigam entender um pouco do funcionamento do Express com este processo simples.

<br/>

Vamos criar um arquivo chamado `saveImage.js` dentro da pasta `javascripts`.

![Image 07]()


E adicionar o seguinte código dentro do arquivo `saveImage.js`.


```javascript
var formidable = require('formidable');
var fs = require('fs');

exports.saveImage = function (req, res, next) {
  var form = new formidable.IncomingForm();

  form.parse(req, function(err, fields, files) {
    res.writeHead(200, {'content-type': 'text/plain'});
    res.write('received upload:\n\n');
    var image = files.image
      , image_upload_path_old = image.path
      , image_upload_path_new = './public/uploads/'
      , image_upload_name = image.name
      , image_upload_path_name = image_upload_path_new + image_upload_name
      ;

    if (fs.existsSync(image_upload_path_new)) {
      fs.rename(
        image_upload_path_old,
        image_upload_path_name,
        function (err) {
        if (err) {
          console.log('Err: ', err);
          res.end('Deu ERRO na hora de mover a imagem!');
        }
        var msg = 'Imagem ' + image_upload_name + ' salva em: ' + image_upload_path_new;
        console.log(msg);
        res.end(msg);
      });
    }
    else {
      fs.mkdir(image_upload_path_new, function (err) {
        if (err) {
          console.log('Err: ', err);
          res.end('Deu ERRO na hora de criar o diretório!');
        }
        fs.rename(
          image_upload_path_old,
          image_upload_path_name,
          function(err) {
          var msg = 'Imagem ' + image_upload_name + ' salva em: ' + image_upload_path_new;
          console.log(msg);
          res.end(msg);
        });
      });
    }
  });
}
```

Agora em `index.ejs` adicione o seguinte código.

![Image 08]()

```html
	<form action="/upload" method="POST" enctype="multipart/form-data">
        Select an image to upload:
        <input type="file" name="image">
        <input type="submit" value="Upload Image">
    </form>
```



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