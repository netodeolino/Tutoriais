# Criando sua Primeira Aplicação Web com Node.js e Express.js

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

Alguns arquivos irão ser criados, como mostra na imagem abaixo.

![Image 01](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_01.png?raw=true)

<br/>

Agora entre no repositório e instale as dependências do projeto com o comando abaixo:
`$ cd site && npm install`

<br/>

A pasta onde seu projeto está localizado vai/ficar ser similar a imagem abaixo:

![Image 02](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_02.png?raw=true)

<br/>

## PARTE 02 - Entendendo a Estrutura Básica do Express ##

#### app.js ####

![Image 03](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_03.png?raw=true)

Neste arquivo é configurado, praticamente, todos os recursos necessários para o projeto, sendo este simples ou não. Algumas destas configurações são rotas, favicon do website, sessão, dentre outras coisas.

<br/>

#### package.json ####

![Image 04](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_04.png?raw=true)

Todas as dependências necessárias que surgirem durante o desenvolvimento do seu projeto você pode instalar por este arquivo executando o comando `npm install`. Por exemplo, suponha que você vá trabalhar com MySQL, então você vem até este arquivo e em "dependencies" adiciona `"mysql": "*"`, com isto a última versão do MySQL é adicionado na sua pasta `node_modules` e fica disponível para ser usado por você no projeto usando o comando <code>require("mysql");</code>.

<br/>

#### index.ejs ####

![Image 05](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_05.png?raw=true)

Este arquivo é a página inicial do website, mas você pode adicionar uma outra em teu local alterando o valor de `response` ou `res` no index.js, mas geralmente é o mesmo não é alterado.

<br/>

#### index.js ####

![Image 06](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_06.png?raw=true)

Este arquivo é onde você faz o controle de suas páginas. Por exemplo, quando abrimos a primeira página do website, que é geralmente tratado como sendo somente uma barra `/`, o local que vai olhar qual arquivo `.ejs` deve tratar essa requisição é alguma função que está em `index.js`.

<br/>

#### style.css ####

![Image 07](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_07.png?raw=true)

É o arquivo CSS que já vem como padrão quando criamos o projeto, mas assim como o `index.ejs` o mesmo pode ser alterado e, inclusive, ser adicionado vários outros.

<br/>

## PARTE 03 - Fazendo o Upload de uma Imagem ##

Agora chegou o momento de brincar um pouco com Express. Neste tutorial vou dar um exemplo de uso de Express não tão comum (digamos assim). Vou mostrar a vocês como fazer o upload de imagens e espero que consigam entender um pouco do funcionamento do Express com este processo simples.

<br/>

Vamos criar um arquivo chamado `saveImage.js` dentro da pasta `javascripts`.

![Image 08](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_08.png?raw=true)


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

![Image 09](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_09.png?raw=true)

```html
<form action="/upload" method="POST" enctype="multipart/form-data">
    Select an image to upload:
    <input type="file" name="image">
    <input type="submit" value="Upload Image">
</form>
```

<br/>

Para que possamos utilizar o `formidable` precisamos instalar o mesmo em nossa pasta `node_modules`, e para fazer isto vamos usar o `package.json`.

![Image 10](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_10.png?raw=true)

Adicionando o seguinte trecho:
`$ "formidable": "*"`

E com isso temos a última versão disponível para ser utilizada.

<br/>

Por último vamos configurar o arquivo `index.js` para que quando for requisitado que uma imagem seja salva atravez da URL `/upload` o mesmo chame a função necessária para que a ação seja possível.

![Image 11](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_11.png?raw=true)

No arquivo vai ser adicionado duas linhas de código, as mesmas são:

```javascript
var SaveImage = require('../public/javascripts/saveImage'); /* Na linha 05 da imagem acima */
router.post('/upload', SaveImage.saveImage); /* Na linha 13 da imagem acima */
```

<br/>

## PARTE 04 - Reinstalando as dependências e Rodando a Aplicação ##

Vamos rodar novamente o comando `npm install` para que o `formidable` possa enfim ser adicionado e posteriormente vamos dar um `npm start` para que a aplicação execute.

![Image 12](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_12.png?raw=true)

<br/>

No navegador vamos digitar `localhost:3000` e a seguinte página irá ser aberta.

![Image 13](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_13.png?raw=true)

<br/>

Escolha uma imagem e clique em `Upload Image` para que ela seja salva.

![Image 14](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_14.png?raw=true)

![Image 16](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_15.png?raw=true)

O retorno da ação anterior é uma mensagem na tela mostrando o local que a imagem foi salva.
> Em `saveImage.js` você pode mudar o local de upload de imagens.

<br/>

Entrando na pasta `uploads` agora encontro a imagem salva.

![Image 16](https://github.com/netodeolino/Tutoriais/blob/master/Criando%20sua%20Primeira%20Aplica%C3%A7%C3%A3o%20Web%20com%20Node.js%20e%20Express.js/Images/img_16.png?raw=true)


<br/>

##FIM!##
Bom, espero que esse tutorial ajude á você a iniciar com seus primeiros projetos com Express e respectivamente Node.js. Quaisquer dúvidas pode entrar em contato comigo pelo meu email que está na página inicial do meu GitHub. Obrigado e até mais!

####Neto Deolino
<ol>
    <li> http://linkedin.com/in/netodeolino </li>
    <li> http://netodeolino.github.io </li>
</ol>