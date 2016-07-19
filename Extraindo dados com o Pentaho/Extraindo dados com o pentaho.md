# Um Simples Guia Passo-a-Passo Para Você Que Precisa Extrair Dados De Arquivos Para Seu Banco De Dados

A primeira coisa que fazemos é criar um Banco no Postgres, no meu caso foi `aulapentaho`.

![Image 01](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_01.png?raw=true)

<br />

A segunda coisa a ser feita é criar a tabela que vai receber os dados da base que você escolheu. Para isso abra com o Office Writer o arquivo `.csv` da sua base de dados, pois com ela você ver os campos (atributos/coluna) e os possíveis tipos (int, varchar, ...) necessários para criar sua tabela.

![Image 02](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_02.png?raw=true)

<br />

Minha tabela, referente ao meu arquivo `.csv`, ficou como segue a imagem. Dei ao nome da tabela o mesmo nome de meu arquivo .csv neste caso, pois pode facilitar o entendimento do mesmo. Repare também que meus atributos DISCIPLINA e GABARITO eu coloquei com um varchar maior do que aparentemente eu precisava conforme a imagem anterior. Eu fiz isto para garantir que a extração não desse erro caso no meio da minha base .csv tenha tuplas com varchar maior que os primeiros valores que vi nos campos conforme imagem anterior. Só precisa fazer isto para campos do tipo string/varchar.
**NOTA:** É mostrado os primeiros campos do arquivo!

![Image 03](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_03.png?raw=true)

<br />

Nesta imagem abro o Pentaho no diretório onde o armazenei. Ele executa com o arquivo `spoon.sh`.

![Image 04](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_04.png?raw=true)

<br />

Com o Pentaho aberto der dois cliques em Transformações.

![Image 05](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_05.png?raw=true)

<br />

Em Input clique em `CSV File Input` arraste e solte no quadro branco.

![Image 06](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_06.png?raw=true)

<br />

Vai ficar como na imagem. Faça o mesmo em Output com `Table Output`.

![Image 07](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_07.png?raw=true)

<br />

Dê um clique em Table output. Clique agora na seta dentro da caixa que fica a esquerda, arraste e solte em `CSV File Input` e clique em `Main Input...`.

![Image 08](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_08.png?raw=true)

<br />

Deve ficar como a imagem.

![Image 09](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_09.png?raw=true)

<br />

Der dois cliques sobre `CSV input file`. Vai abrir a seguinte tela.

![Image 10](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_10.png?raw=true)

<br />

Em `Filename` clique em `Navega...` e selecione o teu arquivo `.csv` que quer extrair (o mesmo que usou para criar a tabela no banco). Em `Delimiter` ponha o delimitador do arquivo que é geralmente ";" ou " " (ponto-e-vírgula ou espaço). Abra tua base com o Gedit para saber o delimitador correto. Depois clique em `Obtem Campos`.

![Image 11](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_11.png?raw=true)

<br />

Vai abrir a seguinte tela, clique em `OK`.

![Image 12](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_12.png?raw=true)

<br />

Nos tipos que forem do tipo String ponha o tamanho que colocou no teu varchar na hora de criar a tabela. Exemplo: O meu GABARITO eu coloquei varchar(2), aqui nesta tela o GABARITO aparece com tamanho 1, então eu editei para 2 na quarta coluna, conforme imagem abaixo. Depois clique em `Preview`, digite 100 e clique `OK`. Os valores da base devem ser mostrados em uma tela, depois é só fechar a tela de preview e clicar em `OK` na tela de CSV Input. Esta tela de preview somente serve para ver se tudo está indo como desejado.

![Image 13](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_13.png?raw=true)

<br />

Agora em `Table Output` der dois cliques para abrir e vá em `New...` para criar uma nova conexão.

![Image 14](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_14.png?raw=true)

<br />

Configure a conexão conforme teu banco, tabela e senha de acesso ao banco. Der um nome a conexão e clique em `Test`.

![Image 15](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_15.png?raw=true)

<br />

Se tudo ocorrer bem a mensagem a baixo irá aparecer. Agora clique em `OK` da mensagem e no `OK` de `Database Connection`.

![Image 16](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_16.png?raw=true)

<br />

Em `Target Schema` navegue e selecione public. Em `Target Table` selecione a tabela que você criou para armazenar os dados de extração. Depois selecione `Specify Database Fields` e abra a aba `Database fields`.

![Image 17](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_17.png?raw=true)

<br />

Clique em `Get Fields` e depois em `Enter Field Mapping` e clique em `OK`.

![Image 18](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_18.png?raw=true)

<br />

Clique em `SQL` e a tela abaixo irá aparecer. Depois clique em `Execute`. Feche as telas que abrirem posteriormente.

![Image 19](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_19.png?raw=true)

<br />

Agora clica em `OK` na tela de Table output.

![Image 20](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_20.png?raw=true)

<br />

Nesta tela clique na opção de `Play` para executar a transformação.

![Image 21](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_21.png?raw=true)

<br />

Nesta tela clica em `Run`.

![Image 22](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_22.png?raw=true)

<br />

Nesta em `Sim` para salvar sua transformação.

![Image 23](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_23.png?raw=true)

<br />

Salve a transformação no local que desejar.
> Nota do tutor: Meio que obrigatório!

![Image 24](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_24.png?raw=true)

<br />

Imagem da transformação finalizada. Sorria :) Este passo pode demorar muito tempo dependendo do tamanho da base!

![Image 25](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_25.png?raw=true)

<br />

De volta ao Postgres, crie novamente a chave primária da tabela, pois o Pentaho a exclui. Clique sobre a tabela com o botão direito do mouse e vá em `New Object` e `New Primary Key`. Vá até a aba `Columns` e em `Column` selecione a coluna que deve ser chave primária, clique em `Add` e depois em `OK`. Este passo pode demorar um pouco, depende do tamanho de tua base, porque o Postgres procura nesta coluna valores duplicados, pois caso haja não pode ser chave primária.

![Image 26](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_26.png?raw=true)

<br />

Por fim faça uma consulta (select) em teu banco para ver se está tudo OK com a extração. Não se esqueça de limitar a consulta, pois iria demorar bastante para o Postgres ler toda a base e imprimir na tela.

![Image 27](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_27.png?raw=true)

<br />

## FIM!
Eu espero que este tutorial tenha sido útil! O mesmo foi criado por mim com a intenção de ajudar qualquer pessoa que precise extrair dados de algum local para um Banco de Dados específico. Apesar do tutorial ter sido feito usando como exemplo o Postgres e um arquivo `.CSV`, acredito eu que fique muito mais fácil para alguns realizar o procedimento com outros SGBD's e outros arquivos como um `.TXT`, pois vai mudar somente algumas configurações simples de serem feitas.

Neto Deolino – linkedin.com/in/netodeolino
