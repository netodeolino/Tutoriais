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

Para que possamos utilizar o `formidable` precisamos instalar o mesmo em nossa pasta `node_modules`, e para fazer isto vamos usar o `package.json`.

![Image 09]()

Adicionando o seguinte trecho:
`$ "formidable": "*"`

E com isso temos a última versão disponível para ser utilizada.

<br/>

Por último vamos configurar o arquivo `index.js` para que quando for requisitado que uma imagem seja salva atravez da URL `/upload` o mesmo chame a função necessária para que a ação seja possível.

![Image 10]()

No arquivo vai ser adicionado duas linhas de código, as mesmas são:

```javascript
var SaveImage = require('../public/javascripts/saveImage'); /* Na linha 05 da imagem acima */
router.post('/upload', SaveImage.saveImage); /* Na linha 13 da imagem acima */
```

<br/>

## PARTE 04 - Reinstalando as dependências e Rodando a Aplicação ##

Vamos rodar novamente o comando `npm install` para que o `formidable` possa enfim ser adicionado e posteriormente vamos dar um `npm start` para que a aplicação execute.

![Image 11]()

<br/>

No navegador vamos digitar `localhost:3000` e a seguinte página irá ser aberta.

![Image 12]()

Escolha uma imagem e clique em `Upload Image` para que ela seja salva.

![Image 13]()

![Image 14]()

O retorno da ação anterior é uma mensagem na tela mostrando o local que a imagem foi salva.
> Em `saveImage.js` você pode mudar o local de upload de imagens.

![Image 15]()

Entrando na pasta `uploads` agora encontro a imagem salva.

<br/>

##FIM!##
Bom, espero que esse tutorial ajude á você a iniciar com seus primeiros projetos com Express e respectivamente Node.js. Quaisquer dúvidas pode entrar em contato comigo pelo meu email que está na página inicial do meu GitHub. Obrigado e até mais!

####Neto Deolino
<ol>
    <li> http://linkedin.com/in/netodeolino </li>
    <li> http://netodeolino.github.io </li>
</ol>