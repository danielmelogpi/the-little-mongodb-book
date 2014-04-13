\thispagestyle{empty}
\changepage{}{}{}{-1.5cm}{}{2cm}{}{}{}
![The Little MongoDB Book, By Karl Seguin](title.png)\ 

\clearpage
\changepage{}{}{}{1.5cm}{}{-2cm}{}{}{}

## Sobre este Livro ##

### Licença ###
O Pequeno Livro do MongoDB (The Little MongoDB Book) é licenciado soba licença Attribution-NonCommercial 3.0 Unported. **Você não pagou por este livro.**


Você é livre para copiar, distribuir, modificar ou exibir este livro. Porém, eu solicito que você sempre atribua este livro para mim, Karl Seguin e não o utilize para fins comerciais.

Você pode ver o texto completo da licença em:

<http://creativecommons.org/licenses/by-nc/3.0/legalcode>

### Sobre o Autor ###
Karl Seguin é um desenvolvedor com experiência em vários campos e tecnologias. É um expert em .NET e desenvolvedor Ruby. Ele é um semi-ativo contribuidor de projetos de software livre, um escritor técnico e ocasionalmente palestrante. A respeito do MongoDB, ele foi contribuidor da biblioteca C# MongoDB NoRM, escreveu o tutorial interativo [mongly](http://mongly.com) assim como o [Mongo Web Admin](https://github.com/karlseguin/Mongo-Web-Admin). Seu serviço gratuito para desenvolvedores casuais de jogos, [mogade.com](http://mogade.com/), é movido a MongoDB. 

Seu blog pode ser encontrado em <http://openmymind.net>, e seus tweets via [@karlseguin](http://twitter.com/karlseguin)

### Tradução para Português Brasileiro ###
A tradução foi feita inicialmente por [Daniel Melo](https://github.com/danielmelogpi) depois de ter se beneficiado pelo conhecimento contido na versão em inglês. O tradutor pede contribuições caso erros de gramática sejam encontrados no decorrer dessa versão. Vamos ajudar a comunidade brasileira que tem voltado os olhos para essa ferramenta tão interessante.

### Agradecimentos ###
Agradecimento especial a [Perry Neal](http://twitter.com/perryneal) por emprestar-me os olhos, mente e paixão. Você me proveu uma ajuda incomensurável. Obrigado.

### Última Versão ###
Os fontesd da última versão deste livro estão disponíveis em: 

<http://github.com/karlseguin/the-little-mongodb-book>.

\clearpage

## Introdução ##
 > Não é minha culta dos capítulos serem tão curtos, MongoDB é simplesmente fácil de aprender.

É comumente dito que a tecnologia se move a velocidades absurdas. É fato que existe uma crescente lista de novas tecnologias e técnicas sendo lançadas. Entretanto, eu tenho tido há muito a opinião de que tecnologias fundamentais usadas por programadores se movem a um paço mais lento. Alguém poderia passar anos aprendendo pouco e ainda ser relevante. Mas o que acaba sendo supreendente, na verdade, é a velocidade em que tecnologias consolidadas são substituídas. Meio que de repente, tecnologias estabelecidas à muito tempo podem se encontrar ameaçadas pelas mudanças no foco dos desenvolvedores.

Nada poderia representar melhor essa mudança repentida que o progresso das tecnologias NoSQL contra as bases de dados relacionais, amplamente estabelecidas. É quase como se num dia a web fosse movida por alguns poucos RDBMS e no dia seguinte, umas cinco soluções NoSQL se estabeleceram como soluções plausíveis.

Apesar de essas transições parecerem ocorrer de um dia para o outro, a realidade é que pode levar anos até que essas práticas se tornem aceitáveis. O entusiasmo inicial é movido por um pequeno conjunto de desenvolvedores e companias. Soluções são refinadas, lições aprendidas e, ao ver que a solução veio pra ficar, outros lentamente a tentam por si mesmos. Novamente, isso é particularmente verdadeiro no caso do NoSQL onde muitas soluções não são substitutas para formas mais tradicionais de armazenamento, mas, na verdade, focam uma necessidade específica em algo além do que se poderia esperar de formas convencionais.

Tendo dito tudo isso, a primeira coisa que podemos fazer é explicar o que significa NoSQL. É um termo amplo que significa coisas diferentes para pessoas diferentes. Pessoalmente, eu o uso de maneira generalizada significando um sistema que tem uma participação no armazenamento de dados. Explicando de outra forma, NoSQL (novamente, como eu vejo), é a crença de que a sua camada de persistência não é necessariamente responsabilidade de um único sistema. Num ambiente em que os fornecedores de bancos de dados relacionais historicamente tantaram colocar seu softwares em uma posição de uma-ferramenta-para-tudo, NoSQL foca na direção de pequenas unidades de responsabilidade onde a melhor ferramenta para uma certa função pode ser melhorada. Logo, o uso de NoSQL pode conseguir melhorar o uso de bancos de dados relacionais, como o MySQL, mas você ainda poderá usar o Redis como uma alternativa para persistência para partes específicas assim como Hadoop para seu processamento de dados intensivo. De maneira simples, NoSQL se trata de se manter aberto e ciente de padrões e ferramentas alternativas, existentes e adicionais para gerenciar seus dados.

Você deve estar se perguntando onde o MongoDB se encaixa nisso tudo. Como um banco de dados orientado a documentos, Mongo é uma solução NoSQL mais generalizada. Ele deve ser visto como uma tecnolocia alternativa em relação as bases de dados relacionais. Assim como elas, ele também pode representar um benefício ao ser usado com outras soluções NoSQL mais especializadas. MongoDB tem vantagens e desvantagens, que nós cobriremos mais tarde neste livro.

Assim como você deve ter notado, nos usamos os termos MongoDB e Mongo de maneira equivalente.


## Começando ##

A maior parte desse livro focará nas funcionalidades do núcleo do MongoDB. Nós iremos, portanto, fazer uso do shell do MongoDB. Apesar de o shell ser útil para estudar e também como uma ferramenta administrativa, seu software usará um driver para o MongoDB.

Isso nos traz a primeira coisa que você deverá saber sobre o MongoDB: os seus drivers. MongoDB tem [vários drivers oficiais](http://www.mongodb.org/display/DOCS/Drivers) para várias linguagens. Esses drivers podem ser imaginados como os vários drivers de banco de dados com os quais você provavelmente já está familiarizado. Sobre esses drivers, a comunidade construido bibliotecas e frameworks mais específicos para as linguagens. Por exemplo, [NoRM](https://github.com/atheken/NoRM) é uma biblioteca em C# que implementa LINQ e [MongoMapper](https://github.com/jnunemaker/mongomapper) é uma biblioteca para Ruby que interopera com o ActiveRecord. Se você prefere construir sua aplicação sobre os drivers do núcleo do MongoDB ou sobre bibliotecas de de mais alto nível é uma escolha sua. Eu citei esse assunto por que muito novatos com o MongoDB se confundem com a existência de drivers oficiais e bibliotecas desenvolvidas pela comunidade - as primeiras focam em comunicação/conectividade com o MongoDB e as últimas com a linguagem ou implementações específicas dos frameworks.

Ao longo da sua leitura, eu te encorajo a brincar com o MongoDB para replicar o que eu demonstrarei assim como explorar algumas dúvidas que apareçam para você. É fácil ter o Mongo rodando, então vamos dedicar alguns minutos para ajustar as coisas.

1. Vá para a [página oficial de download](http://www.mongodb.org/downloads) e baixe os binários da primeira linha (eu recomendo a versão estável) para o seu sistema operacional. Para propósitos de desenvolvimento você pode usar tanto a versão de 32 quanto a de 64 bit.

2. Extraia o arquivo (onde quer que você queira) e nevegue até a pasta `bin`. Não execute nada ainda, mas saiba que `mongod` é o processo do servidor que `mongo` é o cliente shell - esse são os dois executáveis com os quais nós passaremos a maior parte do tempo trabalhando.

3. Crie um novo arquivo de texto na pasta `bin` chamado `mongodb.config`

4. Adicione uma única linha à esse arquivo: `dbpath=PATH_TO_WHERE_YOU_WANT_TO_STORE_YOUR_DATABASE_FILES`. No caso do Windows, por exemplo, você talvez queira usar `dbpath=c:\mongodb\data` e no Linux provavelmente `dbpath=/etc/mongodb/data`

5. Tenha certeza de que a pasta que você apontou no passo anterior de fato existe.

6. Execute mongod com o parâmetro `--config /path/to/your/mongodb.config`

Como um exemplo para usuários do Windows, se você extraiu o arquivo baixado em `c:\mongodb` e criou `c:\mongodb\data\`, então dentro do arquivo `c:\mongodb\bin\mongodb.config` você especificaria `dbpath=c:\mongodb\data\`. Você poderia rodar `mongod` do prompt de comando usando `c:\mongodb\bin\mongod --config c:\mongodb\bin\mongodb.config`.

Sinta-se a vontade para adicionar a pasta `bin` ao seu PATH para evitar toda essa verbosidade. Usuários de MacOSX e Linux podem seguir praticamente as mesmas instruções. A única coisa a se modificar seriam os caminhos das pastas/arquivos.

Com alguma sorte você agora tem  MongoDB rodando. Se você tem um erro, leia a saída cuidadosamente - o servidor é bom em explicar o que saiu errado.

Você pode agora executar `mongo` (sem o *d*) que conectará o shell ao seu servidor em execução. Tente usar `db.version()` para verificar se tudo está funcionando da forma que deveria. Com sorte você verá a versão instalada.

\clearpage

## Capítulo 1 - O básico ##

Nós começamos nossa jornada pelos mecanismos básicos de trabalho com o MongoDB. Obviamente esse é o foco principal para entender o Mongo, mas deve nos ajudar a responder questões de alto nível sobre onde o MongoDB se encaixa.

Para começar, há seis conceitos simples que nós precisamos entender.

1 . MongoDB tem o mesmo conceito de "base de dados" (database) com o qual você provavelmente já é familiar (ou um schema, para os colegas do Oracle). Dentro de uma instância do MongoDB você pode ter zero ou mais bases de dados, cada uma agindo como um espaço para o resto.

2. Uma base de dados pode ter zero ou mais 'coleções'. A coleção compartilha o suficiente em comum com as `tabelas` tradicionais e você pode pensar nas duas como a mesma coisa.

3. Coleções são feitas de zero ou mais `documentos`. Novamente, um documento pode ser imaginado como uma `linha`

4. Um documento é feito de um ou mais `campos`, que você pode provavelmente já percebeu que se parecem com as `colunas`.

5. `Indices` no MongoDB funcionam basicamente como seus pares nas bases relacionais.

6. `Cursores` são diferentes de que os outros 5 conceitos mas são importantes o suficiente, e comumente explorados, que eu acho que eles valem a discussão. A coisa importante a se aprender sobre cursores é que quando você pode dados ao MongoDB, ele retorna um cursor, com o qual você pode realizar operações, como contar ou pular alguns registros, sem necessariamente ter de recuperar os dados.

Para lembrar, MongoDB é feito de `base de dados` que contém `coleções`. Uma `coleção` é feita de `documentos`. Cada `documento` é composto por `campos`. `Coleções` pode ser `indexadas`, o que melhora a performance  da busca e ordenação. Por último, quando temos dados vindos do MongoDB, nos os temos por meio de um `cursor` cuja execução de fato é atrasada até que seja necessária.

Você ja deve estar se questionando, por que usar terminologia nova (coleção vs. tabela, documento vs. linha e campo vs. coluna). É só pra fazer as coisas mais complicadas? A verdade é que apesar de esses conceitos serem similares aos seus pares nas bases relacionais, eles não são idênticos. A diferença mais marcante vêm do fato de bancos relacionais definirem as colunas no nível da tabela, enquanto uma base de dados orientada a documentos os define no nível dos documentos. Isso quer dizer que cada documento, dentro da mesma coleção pode ter seu único conjunto de campos. Assim sendo, coleção é um container burro em comparação com a tabela, enquanto um documento tem bem mais informação que uma linha.

Apesar de isso ser importante de entender, não se preocupe se as coisas não estão claras agora. Não vai levar mais que dois inserts para ver o que isso realmente significa. No final disso tudo, o ponto é que a coleção não restrige o que acontece dentro dela (é sem schema). Campos são ligados a cada documento, individualmente. Os benefícios e problemas disso serão explorados num capítulo futuro.

Vamos por a mão na massa. Se você ainda não tem o mongo rodando, inicie o servidor `mongod` assim como o shell do mongo. O shell executa Javascript. Existem alguns comandos globais que nós podemos executar, como `help` ou `exit`. Comandos executados sobre a base de dados atual são executados sobre o objeto `db`, como `db.help()` ou `db.stats()`. Comandos executados sobre uma coleção específica, operação esta que faremos bastante, são executadas sobre o objeto `db.NOME_DA_COLECAO`, como `db.unicorns.help()` ou `db.unicorns.count()`.

Vá em frente e use `db.help()`. Você terá uma lista de comandos que você pode executar no objeto `db`;

Uma pequena nota: por isso rodar em um shell Javascript, se você executar o método sem os parênteses `()`, você terá o corpo do método em vez de o executar. Eu só mencionei isso por que da primeira vez que você faz isso e tem uma resposta começando com `function ( .... ) { ...` você não levará um susto. Por exemplo, se você usar `db.help` (sem parênteses), você verá a implementação interna do método `help`.


Em um primeiro momento, nós usaremos o método `use` para mudar de bases de dados. Vá em frente e execute `use learn`. Não importa que ela ainda não exista. A primeira coleção que nós criaremos também criará a base de dados em si. Agora que estamos dentro da base de dados, você pode começar a executar os comandos, como `db.getCollectionsName()`. Se você fizer isso, você receberá um array fazio (`[ ]`). Uma vez que coleções não possuem schema, nós não precisamos criá-las explicitamente. Nós podemos simplesmente inserir um documento em uma nova coleção. Para isso, use o comando `insert`, dando a ele o documento à inserir: 

	db.unicorns.insert({name: 'Aurora', gender: 'f', weight: 450})

A linha acima está excutando `insert` sobre a coleção `unicorns`, lhe passando um único argumento. Internamente o MongoDB usa um JSON serializado binariamente. Externamente isso significa que nós usamos bastante JSON, como é o caso dos nossos parâmetros. Se nós executarmos `db.getCollectionsNames()` agora, nós teremos duas coleções: `unicorns` e `system.indexes`. `system.indexes` é criado uma vez para cada base de dados e contém informação sobre os índices delas.

Você pode usar o `find` em `ùnicorns` para retornar uma lista de documentos:

	db.unicorns.find()

Perceba que, além dos dados que você especificou, existe um campo `_id`. Todo documento deve ter um campo `_id`. Você pode tanto gerar um você mesmo ou deixar o MongoDB gerar um ObjectId para você. Na maior parte do tempo você provavelmente preferirá deixar o MongoDB gerá-los. Por padrão, o campo  `_id` é indexado - o que exploca o por que da coleção `system.indexes` ser criado. Você pode dar uma olhada em `system.indexes`:

	db.system.indexes.find()

O que você está vendo é o nome do índice, a base de dados e a coleção correspondentes e os campos incluídos no índice.

Agora, vamos voltar à nossa discussão sobre coleções sem schema. Insira um novo documento totalmente diferente dentro de `unicorns`, como:

	db.unicorns.insert({name: 'Leto', gender: 'm', home: 'Arrakeen', worm: false})

Use novamente o `find` para listar os documentos. Assim que virmos um pouco mais, nós discutiremos esse comportamento interessante do MongoDB, mas por agora você já deve estar entendendo o por que da terminologia convencional não ser muito adequada.


### Dominando seletores ###

Complemento os seis conceitos explorados, existe um aspecto prático do MongoDB sobre o qual você deve ter um bom entendimento antes de prosseguirmos para tópicos mais avançados: seletores de query/consulta. Um seletor do MongoDB é como a cláusula `where` de um comando SQL. Sendo assim, você pode usá-lo quando quer encontrar, contar, atualizar e remover documentos de uma coleção. Um seletor é um objeto JSON, sendo o mais simples possível o bom e velho `{}` que bate com todos os elementos (`null` também funciona assim).  Se nós quisessemos encontrar todas as unicórnios fêmeas nós poderíamos usar `{gender: 'f'}`.

Antes de mergular muito fundo nos seletores, vamos adicionar alguns dados para podermos brincar. Primeiramente remova o que nós já adicionamos à coleção `unicorns` usando `db.unicorns.remove()` (uma vez que não estamos fornecendo um seletor, isso removerá todos os documentos). Agora, execute os seguintes inserts para termos alguns dados à mão (sugiro que você copie e cole isso, com algum cuidado com as aspas): 

	db.unicorns.insert({name: 'Horny', dob: new Date(1992,2,13,7,47), loves: ['carrot','papaya'], weight: 600, gender: 'm', vampires: 63});
	db.unicorns.insert({name: 'Aurora', dob: new Date(1991, 0, 24, 13, 0), loves: ['carrot', 'grape'], weight: 450, gender: 'f', vampires: 43});
	db.unicorns.insert({name: 'Unicrom', dob: new Date(1973, 1, 9, 22, 10), loves: ['energon', 'redbull'], weight: 984, gender: 'm', vampires: 182});
	db.unicorns.insert({name: 'Roooooodles', dob: new Date(1979, 7, 18, 18, 44), loves: ['apple'], weight: 575, gender: 'm', vampires: 99});
	db.unicorns.insert({name: 'Solnara', dob: new Date(1985, 6, 4, 2, 1), loves:['apple', 'carrot', 'chocolate'], weight:550, gender:'f', vampires:80});
	db.unicorns.insert({name:'Ayna', dob: new Date(1998, 2, 7, 8, 30), loves: ['strawberry', 'lemon'], weight: 733, gender: 'f', vampires: 40});
	db.unicorns.insert({name:'Kenny', dob: new Date(1997, 6, 1, 10, 42), loves: ['grape', 'lemon'], weight: 690,  gender: 'm', vampires: 39});
	db.unicorns.insert({name: 'Raleigh', dob: new Date(2005, 4, 3, 0, 57), loves: ['apple', 'sugar'], weight: 421, gender: 'm', vampires: 2});
	db.unicorns.insert({name: 'Leia', dob: new Date(2001, 9, 8, 14, 53), loves: ['apple', 'watermelon'], weight: 601, gender: 'f', vampires: 33});
	db.unicorns.insert({name: 'Pilot', dob: new Date(1997, 2, 1, 5, 3), loves: ['apple', 'watermelon'], weight: 650, gender: 'm', vampires: 54});
	db.unicorns.insert({name: 'Nimue', dob: new Date(1999, 11, 20, 16, 15), loves: ['grape', 'carrot'], weight: 540, gender: 'f'});
	db.unicorns.insert({name: 'Dunx', dob: new Date(1976, 6, 18, 18, 18), loves: ['grape', 'watermelon'], weight: 704, gender: 'm', vampires: 165});

Agora que nós temos dados, nós podemos dominar os seletores. `{campo: valor}` é o formato usado para encontrar documentos onde `campo` é igual à `valor`. `{campo1: valor1, campo2: valor2}` é a forma como nós fazemos um `and`. Os campos especiais `$lt`, `$lte`, `$gt`, `$gte` e `$ne` são usados para as operações 'menor que', 'menor ou igual à', 'maior que', 'maior ou igual à' e 'diferente'. Por exemplo, para ter todos os unicórnis machos que pesam mais de 700 quilos, nós poderíamos executar:

	db.unicorns.find({gender: 'm', weight: {$gt: 700}})
	//or (not quite the same thing, but for demonstration purposes)
	db.unicorns.find({gender: {$ne: 'f'}, weight: {$gte: 701}})

O operador `$exists` é usado para acertar com a existência ou não do campo, como por exemplo:

	db.unicorns.find({vampires: {$exists: false}})

Deverá retornar um único documento, sendo esse aquele que não tempo o campo `vampires`. Se quiséssemos usar OR em vez de um AND, nós usaríamos o operador $or e seu valor seria um arrau dos valores que queremos no OR (OU) lógico.

	db.unicorns.find({gender: 'f', $or: [{loves: 'apple'}, {loves: 'orange'}, {weight: {$lt: 500}}]})

A consulta acima retornará todas as unicórnios fêmeas que gostam de maçãs (apple) ou laranjas ou pesam manos de 500 quilos.

Existe algo bem interessante acontecendo no último exemplo. Você já deve ter notado, mas o campo `loves` (gosta) é um array. O MongoDB suporta arrays como objetos de primeira classe. Isso é um recurso muito poderoso. Uma vez que que você comece a usá-lo, você se perguntará como chegou a viver sem isso. O que é mais interessante é quão fácil é recuperar registros usando um array como valor: `{loves: 'watermelon'}` vai retornar todos os documentos que tenham `watermelon` (melão) como valor de `loves` (gosta).

Existem mais operadores do que os que nós vimos até agora. O mais flexível deles é o `$where` que nós permite enviar Javascript para execução do lado do servidor. Eles são descritos na seção [Seletores avançados (Advanced Queries)](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries) do site do MongoDB. O que nós vimos até agora é o básico do que vamos precisar pra começar. São também o que você provavelmente vai usar a maior parte do tempo.

Nós vimos como esses seletores podem ser usados com o comando `find`. Eles também podem ser usados com o comando `remove` que nós demos uma olhada, o `count` que nós ainda não vimos mas que você provavelmente vai adivinhar, e o comando `update`, com o qual nós vamos passar um tempo mais à frente.

O  `ObjectId` que o MongoDB gera para o nosso campo `_id` pode ser selecionado assim:

	db.unicorns.find({_id: ObjectId("TheObjectId")})


### Nesse capítulo ###
Nós ainda não aprendemos sobre o comando `update` ainda ou sobre algumas coisas mais bonitinhas que podemos fazer com o `find`. Entretanto, nós fizemos o MongoDB rodar, vimos superficialmente o `insert` e o `remove` (sobre eles não tem muito mais além do que vimos). Nós também introduzimos o `find` e vimos do que se tratam os seletores do MongoDB. Nós começamos bem e construímos uma fundação sólida para as coisas que estão por vir. Acredite ou não, você já sabe muito do que há pra saber sobre o MongoDB - ele realmente foi feito para ser rápido de usar e simples de aprender. Eu realmente te aconselho a explorar e brincar um pouco com os comandos que vimos até agora antes de prosseguir. Insira mais documentos, talvez em outras coleções, e se acostume mais com os diferentes seletores. Use o `find`, `count` e `remove`. Depois de agumas tentativas as coisas que podem ter parecido estranhas no começo devem se encaixar.

\clearpage

## Capítulo 2 - Atualizando ##
No capítulo 1 nós introduzimos três das 4 operações CRUD (create/criar, read/ler, update/atualizar and delete/apagar). Esse capítulo é dedicado àquela que nós pulamos: `update`. `Update` tem alguns comportamentos curiosos, sendo esse o motivo pelo qual nós dedicamos um capítulo à ele.

### Update: Substituição Versus $set ###
Na sua forma mais simples, `update` leva dois argumentos: o seletor (where/onde) à ser usado e com qual campo atualizar. Se o Roooooodles tiver ganho algum peso, nós poderíamos executar:

	db.unicorns.update({name: 'Roooooodles'}, {weight: 590})

(Se você já brincou com a coleção `unicorns` e já não mais tem os dados originais, vá em frente e use o `remove` para apagar todos os documentos e reinserí-los do trecho de código do capítulo 1.)

Se nós estivéssemos lidando com código real, você provavelmente atualizará seus registros por `_id`, mas uma vez que eu não tenho o `_id` que o MongoDB gerou pra mim, nós faremos isso pelo campo `names`. Agora, se nós olhassemos no registro modificado:

	db.unicorns.find({name: 'Roooooodles'})

Você vai descobrir a primeira surpresa do `update`. Nenhum documento é encontrado por que o segundo parâmetro que nós fornecemos é usado para **substituir** o original. Em outras palavras, `update` encontrou um documento pelo nome e sustituiu o documento inteiro com o documento novo (nosso segundo parâmetro). Isso é diferente e como o `update` do SQL funciona. Em algumas situações isso pode ser extendido para updates muito dinâmicos. Entretando, quando o que você realmente quer fazer é modificar alguns poucos campos, é melhor usar o modificador `$set` do MongoDB:

	db.unicorns.update({weight: 590}, {$set: {name: 'Roooooodles', dob: new Date(1979, 7, 18, 18, 44), loves: ['apple'], gender: 'm', vampires: 99}})

Isso vai restaurar os campos perdidos. Isso não vai sobrescrever o novo `weight` (peso) uma vez que nós não o especificamos. Agora nós podemos executar:

	db.unicorns.find({name: 'Roooooodles'})

Lá está o nosso resultado esperado. Por sim, o jeito certo de atualizar o peso na nossa primeira tentiva seria:

	db.unicorns.update({name: 'Roooooodles'}, {$set: {weight: 590}})

### Modificadores de atualização ###
Complementarmente ao `$set`, nós podemos utilizar outros modificadores para fazer algumas coisas interesantes. Todos os modificadores do `update` funcionam sobre campos - para o seu documento permanecer intacto. Por exemplo, o modificador `$inc` é usado para incrementar em uma certa quantidade, para mais ou para menor. Se, por exemplo, nós déssemos incorretamente ao Pilot o crédito pela morte de dois vampiros, nós poderíamos corrigir esse erro executando:

	db.unicorns.update({name: 'Pilot'}, {$inc: {vampires: -2}})

Se Aurora derrepente desenvolvesse um gosto por doces, nós poderíamos adicionar um valor para o campo `loves` do seu documento, usando o modificador `$push`.

	db.unicorns.update({name: 'Aurora'}, {$push: {loves: 'sugar'}})

A seçao [Atualizando (Updating)](http://www.mongodb.org/display/DOCS/Updating) do site do MongoDB tem mais informação sobre outros modificadores disponíveis.


### Upserts ###
Uma das surpresas mais legais do `update` é que ela suporta `upserts`. Um `upsert` atualiza um documento se o encontra ou insere em caso contrário. Upserts são úteis em certas situações e, quando você se deparar com uma delas você saberá. Para habilitá-lo nós utilizamos o terceiro parâmetro para `true`.

Um exemplo mundano é um contador de visitas para o site. Se nós quisermos manter um contador em tempo real, nós teríamos de observar se o registro já existe para a página e, baseado nisso decidimos se desejamos inserir ou atualizar. Com o terceiro parâmetro omitido (ou com `false`), executar o seguinte trecho não faria nada:

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}});
	db.hits.find();

Entretanto, se habilitarmos o upsert, os resultados são bem diferentes:

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, true);
	db.hits.find();

Já que não existe nenhum documento com o campo `page` igual à `unicorns`, um novo documento é inserido. Se nós executarmos uma segunda vez, o documento existe é incrementado e `hits` é incrementado para 2.

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, true);
	db.hits.find();

### Atualização em vários registros ###
A última surpresa que o `update` tem a oferecer é que, por padrão, ele atualizará um único documento. Até então, para os exemplos que nós estudamos, isso pode parecer lógico. Entretando, se utilizarmos algo como:

	db.unicorns.update({}, {$set: {vaccinated: true }});
	db.unicorns.find({vaccinated: true});

Você deve estar esperando que teremos vacinado todos os nossos unicórnios. Para ter o comportamento que você deseja, um quarto parâmetro deve ser passado como `true`.
 
	db.unicorns.update({}, {$set: {vaccinated: true }}, false, true);
	db.unicorns.find({vaccinated: true});

### Nesse capítulo ###
Esse capítulo concluiu nossa introdução ao básico das chamadas operações de CRUD que está disponíveis nas coleções. Nós vimos o `update` em detalhes e observamos três comportamentos interessantes. Primeiramente, ao contrário do update do SQL, o `update` do MongoDB substitui o documento por inteiro. Por causa disso o modificador `$set` é bem útil. Em segundo lugar, `update` suporta o intuitivo `upsert` que é particularmente útil quando usado com o modificador `$inc`. Finalmente, por padrão, `update` apenas atuailza o primeiro documento encontrado.

Lembre-se de que nós estamos aprendendo MongoDB do ponto de vista do shell. O driver e a biblioteca que você poderá usar altera esses comportamentos ou expõe uma API diferente. Por exemplo, o driver do Ruby funde os últimos dois parâmetros dentro de um único hash: `{:upsert => false, :multi => false}`.

\clearpage

## Capítulo 3 - Dominando o find ##
O capítulo 1 nós deu uma visão superficial do comando `find`. Existe, entretando, mais do `find` para aprender do que somente os seletores. Nos já mencionamos que o resultado de `find` é um `cursor`. Nós vamos agora explorar exatamente o que isso significa.

### Seleção de campos ###
Antes de entrarmos no assunto dos cursores, você deve saber que `find` leva um segundo parâmetro, que é opcional. Esse parâmetro é a lista de campos que queremos obter. Por exemplo, nós podemos ter todos os nomes dos unicórnios executando:

	db.unicorns.find(null, {name: 1});

Por padrão, o campo `id` é sempre retornado. Nós podemos explicitamente excluí-lo especificando `{name:1, _id: 0}`.

Além do campo `_id`, você não pode misturar e casar inclusão e exclusão. Se você parar pra pensar sobre isso, vai ver que faz sentido. Você ou quer selecionar ou quer excluir um ou mais campos explicitamente.


### Ordenação ###
A pouco tempo atrás eu mencionei que `find` retorna um `cursor` cuja execução é atrasada até que seja necessário. Entretando, se tem uma coisa sobre a qual você não deve ter dúvida sobre o shell, é que o `find` executa imediatamente. Esse é um comportamento exclusivo do shell. Nós podemos observar o comportamento verdadeiro dos cursores observando um ou mais métodos que possamos chamar logo após o `find`. O primeiro que analisaremos é o `sort`. `ort` funciona de forma muito selemelhante com a seleção por campos da seção anterior. Nós especificamos que campos nós queremos usar na ordenação (sorting), usando 1 para 'ascendente' e -1 para 'descendente'. Por exemplo:

	//heaviest unicorns first
	db.unicorns.find().sort({weight: -1})
	
	//by vampire name then vampire kills:
	db.unicorns.find().sort({name: 1, vampires: -1})

Assim como em um banco de dados relacional, o MongoDB pode usar um índice para a ordenação. Nós daremos uma olhada nos índices com mais detalhes um pouco mais a frente. Entretanto, você deve saber que o MongoDB limita o tamanho da sua ordenação se não houver um índice. Isso quer dizer que se você tentar ordenar um resultado grande que não pode usar um índice, você receberá um erro. Algumas pessoas vêem isso como uma limitação. Na verdade, eu gostaria que mais base de dados tivesses a capacidade de rejeitar queries não otimizadas. (Eu não vou transformar todos os pontos negativos do MongoDB em um positivo, mas eu já vi bases de dados suficientemente mal otimizadas e sinceramente eu gostaria que elas tivessem um modo strict / strict-mode).

### Paginação ###
Paginação pode ser conseguida usando os métodos `limit` e `skip`. Para ter o segundo unicórnio mais pesado, nós poderíamos usar:

	db.unicorns.find().sort({weight: -1}).limit(2).skip(1)

Usar `limit` junto com o `sort` é uma boa forma de evitar incorrer em problemas quando tentar ordenar campos não indexados. 

### Contando ###
O shell torna possível executar um `count` diretamente numa coleção, dessa forma:

	db.unicorns.count({vampires: {$gt: 50}})

Na verdade, `count` é, na verdade, um método de `cursor`, sendo que o shell simplemente fornece um atalho. Drivers que não possuem tal atalho pprecisa ser executados da seguinte forma (que também funcionará no shell):

	db.unicorns.find({vampires: {$gt: 50}}).count()

### Nesse capítulo ###

Usar o `find` e os `cursors` é uma proposta interessante. Existem alguns comandos adicionais que nós ou cobriremos nos pŕoximos capítulos ou que servem somente em casos isolados. Por hora, você deve se sentir confortável trabalhando com o mongo no shell e entendendo os fundamentos do MongoDB.

\clearpage

## Capítulo 4 - Modelagem de dados ##
Vamos mudar a direção das rodas na para algo mais abstrato sobre o MongoDB. Explicar alguns termos novos e um pouco de sintax é uma tarefa simples. Conversando sobre modelagem com um paradigma novo não é assim tão simples. A verdade é que a maioria ainda está aprendendo o que funciona e o que não quando falamos de modelagem com essas tecnologias novas. É uma conversa que nós podemos começar a ter, mas que no final das contas você vai ter de praticar e aprender com código real.

Comparadas com a maioria das soluções NoSQL, as bases de dados orientadas a documentos são provavelmente as menos constrastantes, comparadas com bases de dados relacionais, quando falamos de modelagem. As diferenças que existem são pequenas mas isso não quer dizer que não sejam importantes.

### No Joins ###
O primeira e mais fundamental diferença com a qual você precisará se acostumar é a falta dos `joins` no MongoDB. Eu não sei dizer uma razão específica para o fato de nenhum tipo de sintaxe de join não ser suportada, mas eu sei que `joins` são usualmente vistos como não escaláveis. Isso quer dizer que, uma vez que você comece a partir seus dados horizontalmente, você acaba fazendo os `joins` do lado do cliente (o servidor de aplicação) de uma forma ou de outra. Sejam quais forem as razões, o fato de que dados são relacionais continua existindo e o MongoDB não suporta `joins`.

Sem saber de mais nada, para viver em mundo sem joins, nós temos de fazer-los nós mesmos dentro do código da nossa aplicação. Essencialmente nós precisamos executar uma segunda query para encontrar (`find`) dados relevantes. Organizar nossos dados não é tão diferente do que declarar uma chave estrangeira numa base relacional. Vamos dar um pouco menos de foco aos nossos unicórnios e alguns minutos aos nossos empregados (`employees`). A primeira coisa que nós faremos é criar um empregado (eu vou fornecer um `_id` explicitamente para que tenhamos exemplos coerentes).

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d730"), name: 'Leto'})

Agora vamos adicionariar alguns empregados e o seu gerente, o `Leto`.

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d731"), name: 'Duncan', manager: ObjectId("4d85c7039ab0fd70a117d730")});
	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d732"), name: 'Moneo', manager: ObjectId("4d85c7039ab0fd70a117d730")});

Vale a pena lembrar que o `_id` pode ser qualquer valor único. Uma vez que você deva querer usar um `ObjetoId` na vida real, nós os usaremos aqui também.

Está claro que para encontrarmos todos os empregados do Leto, nós podemos simplesmente executar:

	db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})

Não existe nada mágico aqui. No pior dos casos, na maioria das vezes, a falta do join meramente exigirá uma query a mais (com sorte uma indexada).

#### Arrays e documentos incorporados ####
Só por que o MongoDB não suporta joins isso não quer dizer que ele não tenha alguns truques ao seu favor. Lembra-se de que nós vimos que o MongoDB suporta arrays como objetos de primeira classe? Isso é extremamente útil quando lidamos com relacionamentos de muitos-pra-um ou de muitos-pra-muitos. Como um exemplo simples, se um empregado pudesse ter dois gerentes, nós poderiamos lidar com eles usando um array:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d733"), name: 'Siona', manager: [ObjectId("4d85c7039ab0fd70a117d730"), ObjectId("4d85c7039ab0fd70a117d732")] })

Nos estamos interessandos em que, para alguns documentos, `manager` (gerente) possa ser um valor escalar, enquanto para outros ele possa ser um array.

	db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})

Você vai logo notar que arrays de valores são bem mais convenientes do que lidar com tabelas intermediárias dos relacionamentos de muitos-pra-muitos.

Além dos arrays, o MongoDB suporta documentos incorporadas. Vá em frente e tente inserir um documento com um documento embutido, mais ou menos assim:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d734"), name: 'Ghanima', family: {mother: 'Chani', father: 'Paul', brother: ObjectId("4d85c7039ab0fd70a117d730")}})

No caso de você estar imaginando, documentos incorporados pode ser recuperados usando uma "notação de ponto" (dot notation):

	db.employees.find({'family.mother': 'Chani'})

Nós exploraremos rapidamente esse assunto dos documentos incorporados para que você veja como utilizá-los.

#### DBRef ####
O MongoDB suporta algo chamado `DBRef` que é uma convenção de vários drivers. Quando um driver encontra um `DBRef` ele pode rapidamente recuperar o documento referenciado. Um `DBRef` inclui a coleção e o id do documento referenciado. Isso geralmente serve para propósitos muito específicos: quando documentos da mesma coleção talvez referenciem documentos de uma coleção diferente um do outro. Isso significa que, o `DBRef` do `document1` pode apontar para um documento em `managers` enquando o `DBRef` para do document2 pode apontar para um documento em `employees`.


#### Desnormalização ####
Uma outra alternativa ao uso dos joins é desnormalizar seus dados. Historicamente, desnormalização se reservou a código sensível à performance, ou quando os dados deveriam ser mantidos conforme um ponto no tempo (como um log para auditoria). Entretanto, com a popularidade do NoSQL crescendo constantemente, sendo várias dessas tecnologias sem joins, desnormalização como parte da modelagem comum está se tornando algo comum. Isso não significa que você agora deve duplicar cada pedaço dos seus dados em cada documento. Entretanto, em vez de deixar o medo da duplicação dos dados dirigir suas decisões quanto ao design, considere modelar seus dados baseado em que informação pertence a que documento.

Por exemplo, digamos que você esteja escrevendo uma aplicação de um fórum. O modo tradicional de associar um `user` com um `post` é usando uma coluna chamada `userid` na tabela `posts`. Com esse formato você não pode modelar `posts` sem recuperar (join) `users`. Uma outra possibilidade é simplesmente guardar o `name` assim como o `userid` para cada `post` Você poderia até fazer isso com um documento incorporado, como `user: {id: ObjectId('Something'), name: 'Leto'}`. Sim, sim, se você deixar os usuários mudarem seus nomes, você terá de atualizar cada documento (o que é uma query extra).


Ajustar-se a esse tipo de estratégia não é algo que vem fácil para alguns. Em muitos casos isso nem faria sentido. Apesar disso, não sinta medo de experimentar algo assim. Não só é viável em algumas circunstâncias, mas também pode ser a coisa certa a se fazer.

#### Qual você deveria escolher? ####
Arrays de ids são sempre uma estratégia útil quando lidamos com relacionamentos de um-para-muitos ou muitos-para-muitos. Provavelmente é seguro dizer que `DBRef's` não são usados com muita frequência mas, ainda sim, você com certeza pode brincar e fazer testes com eles.

Primeiramente, você deve saber que um documento individual é limitado a 4 megabytes de tamanho. Saber que documentos tem um tamanho limitado, apesar de bastante generoso, te dá alguma ideia de como eles devem ser usados. Aparentemente muitos desenvolvedores preferem usar referências manuais para a maioria dos relacionamentos. Documentos incorporados são frequentemente interessantes, mas para pequenos pedaços de dados que sempre queremos recuperar com seu documento-pai. Um exemplo de mundo real que eu costumo usar é o de guardar o documento `accounts` (contas) com cada usuário, mais ou menos assim:

	db.users.insert({name: 'leto', email: 'leto@dune.gov', account: {allowed_gholas: 5, spice_ration: 10}})

Isso não quer dizer que você deva subestimar o poder dos documentos incorporados ou escrevê-los à parte, como algo de utilidade menor. Ter o seu modelo mapeando seus dados em seus objetos torna as coisas mais simples e constantemente reduz a necessidade de um join. Isso é especialmente verdade quando se considera que o MongoDB te deixa consultar e indexar campos de um documento incorporado.

### Poucas ou muitas coleções ###
Uma vez que coleções não forçam nenhum schema, é perfeitamente possivel construir um sistema usando uma única coleção com uma diversidade de documentos. O que eu costumo encontrar por ai é que a maioria dos sistemas usando MongoDB se organizam mais ou menos como o que você vai encontrar em um sistema relacional. Em outras palavras, se fosse uma tabela na base de dados relacional, provavelmente seria uma coleção no MongoDB (tabelas intermediárias dos relacionamentos muitos-para-muitos seriam uma exceção notável a essa ideia).

A conversa fica ainda mais interessante quando se consideram os documentos incorporados. Um exemplo frequentemente citado é o de um blog. Devemos ter uma coleção `posts` e uma `comments` ou cada `post` deve ter um array de `comments` dentro dos seus registros? Se desconsiderarmos o limite de 4MB por enquanto (Hamlet tem, ao todo, menos de 200KB. Seu blog é tão popular assim?), muitos desenvolvedores ainda preferem separar as coisas. É simplesmente mais limpo e mais explícito.

Não existe nenhuma regra fixa (fora o limite de 4MB). Experimento com formatos diferentes e você vai adquirir um senso do que parece ou não estar correto.

### Nesse capítulo ###
Nosso objetivo nesse capítulo foi de tentar mostrar algumas estratégias úteis para modelar seus dados no MongoDB. Um ponto de partida, se assim preferir. Modelar uma base de dados orientada a documentos é diferente, mas não tão diferente do que existe no mundo relacional. Você tem um pouco mais de flexibilidade e uma limitação, mas para um sistema novo, as coisas tendem a se encaixar até bem. A única coisa em que você pode errar é não tentando.


\clearpage

## Capítulo 5 - Quando usar o MongoDB ##
Por agora você ja deve ter entendimento suficiente do MongoDB para ter a sensação de onde e como ele deve servir no seu sistema existente. Existem tantas novas tecnologias para armazenamento que as vezes ficamos sem rumo para escolhas novas.

Para mim, a lição mais importante, que nada tem a ver com o MongoDB, é que você não mais tem de depender de uma única solução para lidar com seus dados. Sem dúvidas, uma solução unificada tem vantagens óbivias para vários projetos e, possivelmente a maioria, uma única solução é uma ideia interessante. A ideia não é a de que você deve usar tecnologias diferentes, mas que você pode. Somente você saberá quando os benefícios de introduzir uma tecnologia nova superam os custos.

Tendo dito isso, espero que o que você viu até agora tenha te dado a visão de que o MongoDB é uma solução generalizada. Tem sido mencionado frequentemente que bases de dados orientadas a documentos compartilham muitas características em comum com bases de dados relacionais. Além disso, em vez de ficarmos rodeando, vamos simplesmente assumir que o MongoDB deve ser visto como uma alternativa direta às bases relacionais. Onde alguém pode estar vendo o Lucene como uma melhoria para bases de dados relacionais com seu indexamento de textos longos, ou o Redis como uma forma de persistência usando chave-valor, MongoDB é um repositório central para seus dados.

Perceba que eu não disse que o MongoDB *substitui* bases de dados relacionais, mas que, em vez disso, disse que ele é uma *alternativa*. É uma ferramenta que pode fazer o que várias ferramentas podem fazer. Algumas coisas o MongoDB faz melhor, algumas faz pior. Vamos dissecar um pouco mais as coisas.

### Sem schema (Schema-less) ###
Um benefício repetidamente citado das bases de dados orientadas a documentos é que elas não tem schema. Isso faz delas ferramentas muito mais flexíveis do que bases de dados com tabelas. Eu concordo que ficar sem um schema é um recurso interessante, mas não pelas razões que as pessoas costuma apontar.

As pessoas falam de schema-less como se você de repente começasse a guardar dados como na casa da mãe Joana. Existem domínios e conjuntos de dados que realmente podem ser um problema para modelar usando o modelo relacional, mas eu os vejo como casos de exceção. Sem-schema é legal, mas a maior parte dos seus dados vai acabar altamente estruturada. É verdade que ter diferenças ocasionais entre os registros pode ser útil, especialmente quando você vai adicionar recursos novos, mas na verdade não é nada que um campo NULLABLE não pudesse resolver tão bem quanto.

Para mim, o principal benefício de ficar sem um design usando schema é a falta de configurações a baixa fricção com o POO. Isso é particularmente verdade quando você está trabalhando com uma linguagem estática. Eu trabalhei com MongoDB usando C# e Ruby e a diferença é gritante. O dinamismo do Ruby e sua popular implementação do ActiveRecord já resolvem muitos dos problemas de lidar com objetos e relacionamentos. Isso não quer dizer que o MongoDB não seja uma boa pedida com o Ruby, por que de fato ele é. Em vez disso, tente ver que a maioria dos desenvolvedores Ruby veriam o MongoDB como uma melhoria a mais, enquanto desenvolvedores C# e Java veriam uma mudança nos fundamentos de como eles lidam com seus dados.

Pense sobre isso da perspectiva do desenvolvedor do driver. Quer salvar um objeto? Serialize ele em JSON (tecnicamente BSON, mas é parecido o suficiente) e o envie ao MongoDB. Não existem mapeamentos de propriedades ou de tipos. Essa facilidade definitivamente chega até você, o desenvolvedor final.

### Escrita ###
Um ponto em que o MongoDB pode se encaixar realizando uma tarefa especializada é na escrita de logs. Inserção no MongoDB é, por padrão, assíncrona. Escritas no MongoDB já são realmente rápidas, e fazer delas algo assíncrono realmente torna o processo mais rápido. Adicionalmente, os dados dos logs pertencem aquele conjunto que frequentemente se beneficia de coleções sem schema. Por fim, MongoDB tem algo chamado ["coleções limitadas" (capped collections)](http://www.mongodb.org/display/DOCS/Capped+Collections). Até agora, todas as coleções criadas são apenas coleções normais. Nós podemos criar uma coleção com limite usando o comando `db.createCollection` e indicando que ela terá um limite.

	//limit our capped collection to 1 megabyte
	db.createCollection('logs', {capped: true, size: 1048576})

Quando essa coleção alcança 1MB de limite, documentos velhos são automaticamente eliminados. Um limite no número de documentos, em vez do tamanho, pode usar feito usando `max`. Coleções com limites tem algumas propriedades interessantes. Por exemplo, você pode atualizar um documento mas não ele não pode aumentar de tamanho. Além disso, a ordem de inserção é preservada, então você não precisa adicionar um novo índice para ter uma ordenação cronológica correta.

Aqui é um bom momento para dizer que se você não quer a sua escrita assíncrona você pode usar o comando `db.getLastError()`. A maioria dos drivers usa isso como uma *gravação segura*, como usando algo como `{:safe=>true}` como um segundo parâmetro para o `insert`.

### Durabilidade ###
Antes da versão 1.8, o MongoDB não tinha durabilidade em um servidor único. Isso quer dizer que uma falha no servidor iria provavelmente gerar uma perca de dados. A solução sempre foi rodar o MongoDB em uma configuração multi-server (o MongoDB suporta replicação). Um dos principais recursos adicionados na versão 1.8 foi o journaling. Para ativá-lo adicione uma linha com `journal=true` ao arquivo `mongodb.config` que criamos quando configuramos o MongoDB (e reinicie seu servidor se você quiser isso ativo de imediato). Você provavelmente quer o journaling ativado (isso será padrão nos lançamentos futuros). Apesar disso, a dose extra de rendimento que você vai receber com ele desativado pode ser um risco que você esteja disposto a correr. (É o caso de citar que alguns tipos de aplicação pode facilmente viver com alguma perca de dados).

Durabilidade só é mencionada aqui por que muito trabalho foi feito sobre essa questão no MongoDB. Isso provavelmente aparecerá nas buscas do Google daqui algum tempo. Informações que apontem isso como um recurso não existente estão simplesmente desatualizadas.

### Busca em texto longo ###
Busca real nos textos extensos é algo que que deverá vir no MongoDB em uma versão futura. Com seu suporte à arrays, uma busca nos textos é facilmente implementável. Para algo mais poderoso você provavelmente irá querer uma solução como  Lucene/Solr. Claro: o mesmo vale para muitas bases de dados relacionais.


### Transações ###
O MongoDB não tem transações. Ele traz duas alternativas, uma muito boa mas com uso limitado, e outra que é meio estranha mas flexível. 

A primeira é suas várias operações atômicas. Isso é excelente, mas só quando isso resolve o problema todo. Nós já vimos algumas das mais simples, como `$inc` e `set`. Existem também comandos como `findAndModify` que podem ser atualizar ou apagar um documento e retorná-lo atômicamente. 

O segundo, para quando operações atômicas não são o suficiente, é voltar ao commit de duas fases. Um comit de duas fazes é para as transações o que desfazer referenciação é para os joins. É uma uma solução independente do armazenamento que vocÊ faz no código. Um commit de duas fazes são na verdade bem populares no mundo relacional como uma forma de implementar transações em múltiplas bases de dados. O site do MongoDB [tem um exemplo](http://www.mongodb.org/display/DOCS/two-phase+commit) ilustrando o cenário mais comum (uma transferência de fundos). A ideia geral é que você guarda o estado da transação no documento atual que está sendo atualizado e passa pelos passos de inicio-pendente-terminado manualmente.

O suporte do MongoDB à documentos incorporados e a falta de schema fazem desse processo algo um pouco menos doloroso, mas ainda não é um processo interessante, especialmente quando você está começando com ele.

### Processamento de dados ###
O MongoDB faz uso do MapReduce para a maioria das tarefas de processamento de dados. Ele tem algumas capacidades de [agregação simples](http://www.mongodb.org/display/DOCS/Aggregation), mas para alguma coisa séria, você vai querer usar o MapReduce. No próximo capítulo, nos daremos uma olhada no MapReduce com mais detalhes. Por agora, você pode pensar nele em uma forma diferente e muito poderosa de `group by` (falando de maneira atenuada). Uma das vantagens do MapReduce é que ele pode ser paralelizado para trabalhar com grandes conjuntos de dados. Entretanto, a implementação do MongoDB faz uso de Javascript, que é single-thread. Qual o ponto disso? Para processar conjuntos grandes de dados você provavelmente precisará de algo mais, como o Hadoop. Por sorte, uma vez que os dois sistemas complementam bem um ao outro, existe um [Adaptador do MongoDB para Hadoop](https://github.com/mongodb/mongo-hadoop).

Claro, paralelizar dados não é algo que as bases de dados relacionais também não é algo que as bases de dados relacionais não façam também. Existem planos para futuras versões do MongoDB que façam melhor as tarefas relacionadas com grandes conjuntos de dados.

### Geospacial ###
Uma caracterísitica poderosa do MongoDB é o seu suporte para índices geoespaciais. Isso permite que você guarde coordenadas x e y nos documentos e então encontre os documentos que estejam perto (`$near`) de outra coordenadas ou dentro (`$within`) de um cículo ou um quadrilátero. Isso é um recurso melhor entendido com algum auxílio visual, então eu te convido a tentar o [tutorial geoespacial interativo de 5 minutos](http://mongly.com/geo/index), se você quer aprender mais.


### Ferramentas e maturidade ###
Você provavelmente já sabe a resposta para isso, mas o MongoDB é obviamente mais jovem que a maioria das bases de dados relacionais. Isso é algo que com certeza você deve considerar. Quanto isso afeta depende do que você está fazendo e como está fazendo. Seja como for, uma avaliação honesta simplesmente não pode ignorar o fato de que o MongoDB é jovem e que a gama de ferramentas disponíveis não é excelente (apesar de que as ferramentas para as bases de dados relacionais ser bem ruinzinha também). Como exemplo, a falta de suporte para ponto flutuante na base 10 certamente será algo a considerar (apesar de não ser necessariamente um impedimento) para sistemas lidando com dinheiro.

Como ponto positivo, drivers existem para uma grande quantidade de linguagens, o protocolo é moderno e simples e o desenvolvimento acontece a velocidades altas. MongoDB está em produção em companhias suficientes que se preocupam com maturidade e a preocupação com isso está se tornando uma coisa do passado.


### Nesse capítulo ###
A mensagem desse capítulo é que o MongoDB, na maioria dos casos, pode substituir uma base de dados relacional. É muito mais simples e direto; é rápido e geralmente impõe poucas restrições aos desenvolvedores da aplicação A falta das transações pode ser um problema sério e legítimo. Entretanto, quando as pessoas perguntam *onde fica o MongoDB no que diz respeito ao novo cenário de armazenamento de dados?* a resposta é simplesmente **exatamente no meio**.


\clearpage

## Capítulo 6 - MapReduce ##


MapReduce is an approach to data processing which has two significant benefits over more traditional solutions. The first, and main, reason it was development is performance. In theory, MapReduce can be parallelized, allowing very large sets of data to be processed across many cores/CPUs/machines. As we just mentioned, this isn't something MongoDB is currently able to take advantage of. The second benefit of MapReduce is that you get to write real code to do your processing. Compared to what you'd be able to do with SQL, MapReduce code is infinitely richer and lets you push the envelope further before you need to use a more specialized solution.

MapReduce is a pattern that has grown in popularity, and you can make use of it almost anywhere; C#, Ruby, Java, Python and so on all have implementations. I want to warn you that at first this'll seem very different and complicated. Don't get frustrated, take your time and play with it yourself. This is worth understanding whether you are using MongoDB or not.

### A Mix of Theory and Practice ###
MapReduce is a two-step process. First you map and then you reduce. The mapping step transforms the inputted documents and emits a key=>value pair (the key and/or value can be complex). The reduce gets a key and the array of values emitted for that key and produces the final result. We'll look at each step, and the output of each step.

The example that we'll be using is to generate a report of the number of hits, per day, we get on a resource (say a webpage). This is the *hello world* of MapReduce. For our purposes, we'll rely on a `hits` collection with two fields: `resource` and `date`. Our desired output is a breakdown by `resource`, `year`, `month`, `day` and `count`. 

Given the following data in `hits`:

	resource     date
	index        Jan 20 2010 4:30
	index        Jan 20 2010 5:30
	about        Jan 20 2010 6:00
	index        Jan 20 2010 7:00
	about        Jan 21 2010 8:00
	about        Jan 21 2010 8:30
	index        Jan 21 2010 8:30
	about        Jan 21 2010 9:00
	index        Jan 21 2010 9:30
	index        Jan 22 2010 5:00

We'd expect the following output:

	resource  year   month   day   count
	index     2010   1       20    3
	about     2010   1       20    1
	about     2010   1       21    3
	index     2010   1       21    2
	index     2010   1       22    1

(The nice thing about this type of approach to analytics is that by storing the output, reports are fast to generate and data growth is controlled (per resource that we track, we'll add at most 1 document per day.)

For the time being, focus on understanding the concept. At the end of this chapter, sample data and code will be given for you to try on your own.

The first thing to do is look at the map function. The goal of map is to make it emit a value which can be reduced. It's possible for map to emit 0 or more times. In our case, it'll always emit once (which is common). Imagine map as looping through each document in hits. For each document we want to emit a key with resource, year, month and day, and a simple value of 1:

	function() {
		var key = {
		    resource: this.resource, 
		    year: this.date.getFullYear(), 
		    month: this.date.getMonth(), 
		    day: this.date.getDate()
		};
		emit(key, {count: 1}); 
	}

`this` refers to the current document being inspected. Hopefully what'll help make this clear for you is to see what the output of the mapping step is. Using our above data, the complete output would be:

	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}, {count:1}]
	{resource: 'about', year: 2010, month: 0, day: 20} => [{count: 1}]
	{resource: 'about', year: 2010, month: 0, day: 21} => [{count: 1}, {count: 1}, {count:1}]
	{resource: 'index', year: 2010, month: 0, day: 21} => [{count: 1}, {count: 1}]
	{resource: 'index', year: 2010, month: 0, day: 22} => [{count: 1}]

Understanding this intermediary step is the key to understanding MapReduce. The values from emit are grouped together, as arrays, by key. .NET and Java developers can think of it as being of type `IDictionary<object, IList<object>>` (.NET) or `HashMap<Object, ArrayList>` (Java).

Let's change our map function in some contrived way:

	function() {
		var key = {resource: this.resource, year: this.date.getFullYear(), month: this.date.getMonth(), day: this.date.getDate()};
		if (this.resource == 'index' && this.date.getHours() == 4) {
			emit(key, {count: 5});
		} else {
			emit(key, {count: 1}); 
		}
	}

The first intermediary output would change to:

	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 5}, {count: 1}, {count:1}]

Notice how each emit generates a new value which is grouped by our key.

The reduce function takes each of these intermediary results and outputs a final result. Here's what ours looks like:

	function(key, values) {
		var sum = 0;
		values.forEach(function(value) {
			sum += value['count'];
		});
		return {count: sum};
	};

Which would output:

	{resource: 'index', year: 2010, month: 0, day: 20} => {count: 3}
	{resource: 'about', year: 2010, month: 0, day: 20} => {count: 1}
	{resource: 'about', year: 2010, month: 0, day: 21} => {count: 3}
	{resource: 'index', year: 2010, month: 0, day: 21} => {count: 2}
	{resource: 'index', year: 2010, month: 0, day: 22} => {count: 1}

Technically, the output in MongoDB is:

	_id: {resource: 'home', year: 2010, month: 0, day: 20}, value: {count: 3}

Hopefully you've noticed that this is the final result we were after.

If you've really been paying attention, you might be asking yourself *why didn't we simply use `sum = values.length`?* This would seem like an efficient approach when you are essentially summing an array of 1s. The fact is that reduce isn't always called with a full and perfect set of intermediate data. For example, instead of being called with:

	{resource: 'home', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}, {count:1}]

Reduce could be called with:

	{resource: 'home', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}]
	{resource: 'home', year: 2010, month: 0, day: 20} => [{count: 2}, {count: 1}]

The final output is the same (3), the path taken is simply different. As such, reduce must always be idempotent. That is, calling reduce multiple times should generate the same result as calling it once. 

We aren't going to cover it here but it's common to chain reduce methods when performing more complex analysis. 

### Pure Practical ###
With MongoDB we use the `mapReduce` command on a collection. `mapReduce` takes a map function, a reduce function and an output directive. In our shell we can create and pass a JavaScript function. From most libraries you supply a string of your functions (which is a bit ugly). First though, let's create our simple data set:

	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 4, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 5, 30)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 20, 6, 0)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 7, 0)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 8, 0)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 8, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 21, 8, 30)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 9, 0)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 21, 9, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 22, 5, 0)});

Now we can create our map and reduce functions (the MongoDB shell accepts multi-line statements, you'll see *...* after hitting enter to indicate more text is expected):

	var map = function() {
		var key = {resource: this.resource, year: this.date.getFullYear(), month: this.date.getMonth(), day: this.date.getDate()};
		emit(key, {count: 1}); 
	};
	
	var reduce = function(key, values) {
		var sum = 0;
		values.forEach(function(value) {
			sum += value['count'];
		});
		return {count: sum};
	};

Which we can use the `mapReduce` command against our `hits` collection by doing:

	db.hits.mapReduce(map, reduce, {out: {inline:1}})

If you run the above, you should see the desired output. Setting `out` to `inline` means that the output from `mapReduce` is immediately streamed back to us. This is currently limited for results that are 16 megabytes or less. We could instead specify `{out: 'hit_stats'}` and have the results stored in the `hit_stats` collections:

	db.hits.mapReduce(map, reduce, {out: 'hit_stats'});
	db.hit_stats.find();

When you do this, any existing data in `hit_stats` is lost. If we did `{out: {merge: 'hit_stats'}}` existing keys would be replaced with the new values and new keys would be inserted as new documents. Finally, we can `out` using a `reduce` function to handle more advanced cases (such an doing an upsert). 

The third parameter takes additional options, for example we could filter, sort and limit the documents that we want analyzed. We can also supply a `finalize` method to be applied to the results after the `reduce` step.

### In This Chapter ###
This is the first chapter where we covered something truly different. If it made you uncomfortable, remember that you can always use MongoDB's other [aggregation capabilities](http://www.mongodb.org/display/DOCS/Aggregation) for simpler scenarios. Ultimately though, MapReduce is one of MongoDB's most compelling features. The key to really understanding how to write your map and reduce functions is to visualize and understand the way your intermediary data will look coming out of `map` and heading into `reduce`.

\clearpage

## Chapter 7 - Performance and Tools ##
In this last chapter, we look at a few performance topics as well as some of the tools available to MongoDB developers. We won't dive deeply into either topic, but we will examine the most import aspects of each.

### Indexes ###
At the very beginning we saw the special `system.indexes` collection which contains information on all the indexes in our database. Indexes in MongoDB work a lot like indexes in a relational database: they help improve query and sorting performance. Indexes are created via `ensureIndex`:

	db.unicorns.ensureIndex({name: 1});

And dropped via `dropIndex`:

	db.unicorns.dropIndex({name: 1});

A unique index can be created by supplying a second parameter and setting `unique` to `true`:

	db.unicorns.ensureIndex({name: 1}, {unique: true});

Indexes can be created on embedded fields (again, using the dot-notation) and on array fields. We can also create compound indexes:

	db.unicorns.ensureIndex({name: 1, vampires: -1});

The order of your index (1 for ascending, -1 for descending) doesn't matter for a single key index, but it can have an impact for compound indexes when you are sorting or using a range condition.

The [indexes page](http://www.mongodb.org/display/DOCS/Indexes) has additional information on indexes.

### Explain ###
To see whether or not your queries are using an index, you can use the `explain` method on a cursor:

	db.unicorns.find().explain()

The output tells us that a `BasicCursor` was used (which means non-indexed), 12 objects were scanned, how long it took, what index, if any was used as well as a few other pieces of useful information.

If we change our query to use an index, we'll see that a `BtreeCursor` was used, as well as the index used to fulfill the request:

	db.unicorns.find({name: 'Pilot'}).explain()

### Asynchronous Writes ###
We previously mentioned that, by default, writes in MongoDB are asynchronous. This can result in some nice performance gains at the risk of losing data during a crash. An interesting side effect of asynchronous writes is that an error is not returned when an insert/update violates a unique constraint. In order to be notified about a failed write, one must call `db.getLastError()` after an insert. Many drivers abstract this detail away and provide a way to do a *safe* write - often via an extra parameter.

Unfortunately, the shell automatically does safe inserts, so we can't easily see this behavior in action.

### Sharding ###
MongoDB supports auto-sharding. Sharding is an approach to scalability which separates your data across multiple servers. A naive implementation might put all of the data for users with a name that starts with A-M on server 1 and the rest on server 2. Thankfully, MongoDB's sharding capabilities far exceed such a simple algorithm. Sharding is a topic well beyond the scope of this book, but you should know that it exists and that you should consider it should your needs grow beyond a single server.

### Replication ###
MongoDB replication works similarly to how relational database replication works. Writes are sent to a single server, the master, which then synchronizes itself to one or more other servers, the slaves. You can control whether reads can happen on slaves or not, which can help distribute your load at the risk of reading slightly stale data. If the master goes down, a slave can be promoted to act as the new master. Again, MongoDB replication is outside the scope of this book.

 While replication can improve performance (by distributing reads), its main purpose is to increase reliability. Combining replication with sharding is a common approach. For example, each shard could be made up of a master and a slave. (Technically you'll also need an arbiter to help break a tie should two slaves try to become masters. But an arbiter requires very few resources and can be used for multiple shards.)

### Stats ###
You can obtain statistics on a database by typing `db.stats()`. Most of the information deals with the size of your database. You can also get statistics on a collection, say `unicorns`, by typing `db.unicorns.stats()`. Again, most of this information relates to the size of your collection.

### Web Interface ###
Included in the information displayed on MongoDB's startup was a link to a web-based administrative tool (you might still be able to see if if you scroll your command/terminal window up to the point where you started `mongod`). You can access this by pointing your browser to <http://localhost:28017/>. To get the most out of it, you'll want to add `rest=true` to your config and restart the `mongod` process. The web interface gives you a lot of insight into the current state of your server.

### Profiler ###
You can enable the MongoDB profiler by executing:

	db.setProfilingLevel(2);

With it enabled, we can run a command:

	db.unicorns.find({weight: {$gt: 600}});

And then examine the profiler:

	db.system.profile.find()

The output tells us what was run and when, how many documents were scanned, and how much data was returned.

You can disable the profiler by calling `setProfileLevel` again but changing the argument to `0`. Another option is to specify `1` which will only profile queries that take more than 100 milliseconds. Or, you can specify the minimum time, in milliseconds, with a second parameter:

	//profile anything that takes more than 1 second
	db.setProfilingLevel(1, 1000);

### Backups and Restore ###
Within the MongoDB `bin` folder is a `mongodump` executable. Simply executing `mongodump` will connect to localhost and backup all of your databases to a `dump` subfolder. You can type `mongodump --help` to see additional options. Common options are `--db DBNAME` to back up a specific database and `--collection COLLECTIONAME` to back up a specific collection. You can then use the `mongorestore` executable, located in the same `bin` folder, to restore a previously made backup. Again, the `--db` and `--collection` can be specified to restore a specific database and/or collection. 

For example, to back up our `learn` collection to a `backup` folder, we'd execute (this is its own executable which you run in a command/terminal window, not within the mongo shell itself):

	mongodump --db learn --out backup

To restore only the `unicorns` collection, we could then do:

	mongorestore --collection unicorns backup/learn/unicorns.bson

It's worth pointing out that `mongoexport` and `mongoimport` are two other executables which can be used to export and import data from JSON or CSV. For example, we can get a JSON output by doing:

	mongoexport --db learn -collection unicorns

And a CSV output by doing:

	mongoexport --db learn -collection unicorns --csv -fields name,weight,vampires

Note that `mongoexport` and `mongoimport` cannot always represent your data. Only `mongodump` and `mongorestore` should ever be used for actual backups.

### In This Chapter ###
In this chapter we looked a various commands, tools and performance details of using MongoDB. We haven't touched on everything, but we've looked at the most common ones. Indexing in MongoDB is similar to indexing with relational databases, as are many of the tools. However, with MongoDB, many of these are to the point and simple to use.

\clearpage

## Conclusion ##
You should have enough information to start using MongoDB in a real project. There's more to MongoDB than what we've covered, but your next priority should be putting together what we've learned, and getting familiar with the driver you'll be using. The [MongoDB website](http://www.mongodb.com/) has a lot of useful information. The official [MongoDB user group](http://groups.google.com/group/mongodb-user) is a great place to ask questions.

NoSQL was born not only out of necessity, but also out of an interest to try new approaches. It is an acknowledgement that our field is ever advancing and that if we don't try, and sometimes fail, we can never succeed. This, I think, is a good way to lead our professional lives.
