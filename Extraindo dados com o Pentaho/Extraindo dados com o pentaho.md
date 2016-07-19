# Um Simples Guia Passo-a-Passo Para Você Que Precisa Extrair Dados De Arquivos Para Seu Banco De Dados

A primeira coisa que fazemos é criar um Banco no Postgres, no meu caso foi “aulapentaho”.

![Image 01](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_01.png?raw=true)

A segunda coisa a ser feita é criar a tabela que vai receber os dados da base que você escolheu. Para isso abra com o Office Writer o arquivo .csv da sua base de dados, pois com ela você ver os campos (atributos/coluna) e os possíveis tipos (int, varchar, etc.) necessários para criar sua tabela.

![Image 02](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_02.png?raw=true)

Minha tabela, referente ao meu arquivo .csv, ficou como segue a imagem. Dei ao nome da tabela o mesmo nome de meu arquivo .csv neste caso, pois pode facilitar o entendimento do mesmo. Repare também que meus atributos DISCIPLINA e GABARITO eu coloquei com um varchar maior do que aparentemente eu precisava conforme a imagem anterior. Eu fiz isto para garantir que a extração não der erro caso no meio da minha base .csv tenha tuplas com varchar maior que os primeiros valores que vi nos campos conforme imagem anterior (ali vejo os primeiros campos do arquivo). Só precisa fazer isto para campos do tipo string/varchar.

![Image 03](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_03.png?raw=true)

Nesta imagem abro o Pentaho no local onde o deixei. Ele abre executando este spoon.sh!

![Image 04](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_04.png?raw=true)

Com o pentaho aberto der dois cliques em Transformações.

![Image 05](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_05.png?raw=true)

Em input clique em 'CSV file input' arraste e solte no quadro branco.

![Image 06](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_06.png?raw=true)

Vai ficar como na imagem. Faça o mesmo em Output com 'Table output'.

![Image 07](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_07.png?raw=true)

Dê um clique em Table output. Clique agora na “setinha” dentro da “caixinha” que fica a esquerda, arraste e solte em 'CSV file input' e clique em 'Main input...'. A opção de cima*

![Image 08](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_08.png?raw=true)

Deve ficar como a imagem.

![Image 09](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_09.png?raw=true)


Der dois cliques sobre 'CSV input file'. Vai abrir esta tela.

![Image 10](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_10.png?raw=true)

Em 'Filename' clique em navegar e selecione o teu arquivo .csv que quer extrair (o mesmo que usou para criar a tabela no banco). Em 'Delimiter' ponha o delimitador do arquivo que é geralmente ; ou espaço. Abra tua base com o gedit para saber o delimitador correto. Depois clique em 'Obtem Campos'.

![Image 11](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_11.png?raw=true)

Vai abrir esta tela, clique em OK.

![Image 12](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_12.png?raw=true)

Nos tipos que forem do tipo String ponha o tamanho que colocou no teu varchar na hora de criar a tabela. Exemplo: O meu gabarito eu coloquei varchar(2), aqui nesta tela o gabarito aparece com tamanho 1, então eu editei para 2 na quarta coluna, conforme imagem. Depois clique em 'Preview', coloque 100 e clique OK. Os valores da base devem ser mostrados em uma tela, depois é só fechar a tela de preview e clicar em OK na tela de CSV Input. (O preview é só para ver se tá tudo OK).

![Image 13](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_13.png?raw=true)

Agora em 'Table output' (da dois cliques para abrir) vá em 'New...' para criar uma nova conexão.

![Image 14](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_14.png?raw=true)

Configure a conexão conforme teu banco, tabela e senha de acesso ao banco. Der um nome a conexão e clique em 'Test'.

![Image 15](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_15.png?raw=true)

Se tudo ocorrer bem a mensagem a baixo irá aparecer. Agora clica em OK da mensagem e no OK da 'Database Connection'.

![Image 16](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_16.png?raw=true)

Em 'Target schema' navegue e selecione public. Em 'Target table' selecione a tabela que você criou para armazenar os dados de extreção. Depois selecione 'Specify database fields' e abra a aba 'Database fields'.

![Image 17](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_17.png?raw=true)

Clique em 'Get fields' e depois em 'Enter field mapping' e clique em OK.

![Image 18](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_18.png?raw=true)


Clique em 'SQL' e esta tela irá aparecer. Depois clica em 'Execute'. Feche as telas que abrirem.

![Image 19](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_19.png?raw=true)

Agora clica em 'OK' na tela de Table output.

![Image 20](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_20.png?raw=true)

Nesta tela clica no “triangulo” de play (digamos assim) para executar a transformação.

![Image 21](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_21.png?raw=true)

Nesta tela clica em 'Run'.

![Image 22](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_22.png?raw=true)

Nesta em 'Sim'.

![Image 23](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_23.png?raw=true)

Salve a transformação em algum local. (Meio que obrigatório).

![Image 24](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_24.png?raw=true)

Imagem da transformação finalizada. Sorria :) Pode demorar muito tempo! Depende do tamanho da base é claro.

![Image 25](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_25.png?raw=true)

De volta ao postgres, crie novamente a chave primaria da tabela, pois o pentaho a exclui. Clica sobre a tabela com o botão direito e vai em 'New Object' e 'New Primary Key'. Vai até a aba 'Columns' e em 'Column' selecione a a coluna que deve ser chave primária, clica em 'Add' e depois em 'OK'. Este passo pode demorar um pouco, depende do tamanho de tua base, porque o postgres procura nesta coluna valores duplicados, pois caso haja não pode ser chave primária.

![Image 26](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_26.png?raw=true)

Por fim de um select em teu banco para ver se está tudo ok com a extração. Não se esqueça de limitar a consulta, pois iria demorar bastante para o postgres ler toda a base e imprimir na tela.

![Image 27](https://github.com/netodeolino/Tutoriais/blob/master/Extraindo%20dados%20com%20o%20Pentaho/Images/img_27.png?raw=true)
