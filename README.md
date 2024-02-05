# Projeto de Price Rent
Projeto de ciência de dados utilizando a  base de dados indicada no github, com o intuito de fazer predições para precificar alugueis em Nova Iorque, NY, assim como fazer uma análise exploratória para entender o mercado de alugueis da cidade.
Uma descrição completa dos atributos está abaixo.

|Campo|Descrição|
|:-|:-|
|host_id| Representa o id do usuário que hospedou o anúncio|
|host_name| Contém o nome do usuário que hospedou o anúncio|
|bairro_group| Contém o nome do bairro onde o anúncio está localizado|
|bairro| Contém o nome da área onde o anúncio está localizado|
|latitude| Contém a latitude do local|
|longitude| Contém a longitude do local|
|room_type| Contém o tipo de espaço de cada anúncio|
|price| Contém o preço por noite em dólares listado pelo anfitrião|
|minimo_noites| Contém o número mínimo de noites que o usuário deve reservar|
|numero_de_reviews| Contém o número de comentários dados a cada listagem|
|ultima_review| Contém a data da última revisão dada à listagem|
|reviews_por_mes| Contém o número de avaliações fornecidas por mês|
|calculado_host_listings_count| Contém a quantidade de listagem por host|
|disponibilidade_365| Contém o número de dias em que o anúncio está disponível para reserva|

# Utilização
Este projeto tem como objetivo utilizar dados de outros alugueis para entender como funciona a precificação de alugueis na cidade de Nova Iorque, além de entender o cenário imobiliário para possíveis investimentos, para tal foram realizadas Análies Exploratórias. Além dissotambém busca-se predizer o preço de um aluguel com base em dados nteriores.

### Dependencias

Bibliotecas necessárias:

pandas == 1.5.3

numpy == 1.23.5

matplotlib.pyplot == 3.6.0

seaborn == 0.12.2

sklearn.metrics == 1.2.2

sklearn.tree == 1.2.2

statsmodels.formula.api == 0.13.5

statsmodels.api == 0.13.5

pickle == 0.7.5

# Storytelling

A partir da análise exploratória foi-se utilizando das variáveis para compreender como funciona o negócio de alugueis dentro de Nova Iorque. A partir disto foram elaborados diversos gráficos com cruzamentos de dados de diversas variáveis, a partir disto foram levantadas as seguintes hipóteses:

- A maioria dos locais se concentram em Manhattan e no Brooklyn, com mais de 20.000 locais;
- A média de preço é mais cara em Manhattan, sendo US00,00, bem maior que as demais, inclusive do brooklyn que fica em segundo com uma média de US125,00;
- Dentro de cada “região” ou  grupo de bairros (como Manhattan e Brooklyn) existem bairros, neste há uma concentração maior no bairro de Williamsburg, que é justamente no brooklyn, em segundo fica Bedford-stuyvesant também no brooklyn;
- Os dois mais frequentados não estão entre os 40 bairros com média mais alta;
- O bairro mais caro é na verdade um monumento de Nova York Fort Wadsworth, logo não entra no mérito apenas da localzação;
- O segundo bairro com média mais cara fica em staten island, e em Manhattan que apesar de ter a maior frequência vem apenas em terceiro que é a Tribeca;
- A maioria dos hosts alugam apartamentos inteiros (25.000), mas boa parte aluga um comodo apenas (+-22.000), e uma parte quase inexpressiva de menos de 2000 aluga quartos compartilhados;
- Um apartamento inteiro é em média US200,00 enquanto um comodo separado é US85,00. Em contrapartida, apesar de ter pouco oferecimento, quartos compartilhados são pouca coisa mais baratos do que comodos inteiros separados sendo US65,00;
- Grande maioria dos hosts aceita um mínimo de uma noite de hospedagem (mais de 12.000) deles, enquanto pouco menos de 12.000 aceita a partir de 2 noites e 8000 aceitam a partir de 3 noites;
- Os grupos de bairros que mais possuem alugueis minimos de pelo menos 365 noites (1 ano) são Manhattan e o Brooklyn;
- Todos mantém uma maior média de no minimo 1 noite de hospedagem;
- Apesar de possuir uma maior frequência de locais para se alugar, Manhattan não possui um maior número de reviews, a região com maior número de reviews é o Brooklyn, e o com menor número de reviews Staten Island;
- Maioria dos hosts possui apenas um local para aluguel, pouco mais de 5000 possuem 2, e assim sucessivamente diminuindo hosts com uma maior quantidade de alugueis disponíveis;
- Os locais no Brooklyn ficam disponíveis em média 100 dias por ano, em Manhattan 70 dias por ano, no Queens 145 dias por ano, no Bronx 165 dias por ano e em Staten Island 200 dias por ano;
- Podemos perceber que apesar da frequência alta, Brooklyn e Manhattan possuem os locais com disponibilidade mais curta por ano, indicando que possivelmente possuem um aluguel por temporada de férias ou feriados, o que também talvez pudesse aumentar o preço.
- O local ais indicado seria Manhattan, poi sé um bairro que possui uma frequência de aluguel maior junto de uma média de preço maior.
- Maioria dos bairros aceitam uma quantidade minima de 1 noite, porém os locais com uma disponibilidade durante o ano menor tendem a ter uma média de preço maior.  O que pode indicar que por ser uma cidade turistica, tais locais alguem para datas festivas e feriados, gerando uma incidência menor de dias disponíveis mas com preços mais altos.
- Palavras como Luxury, ou huge, ou outros indicativos de luxo indicam um preço mais alto, porém o que mais indica é o nome da região, como Manhattan, Manhattan east side e afins, tal nome seguido de vista ou algo do gênero possuem um preço mais caro (o nome ja explicao porquê). Ou seja, os nomes indicam determinado valor, não somente pela caracteristica, mas também por uma indicação de local.

Método utilizado e modelo escolhido:

- Como será uma previsão de valor, algo que não poderá ser colocado em binario 1 e 2, optarei por utilizar DecisionTreeRegressor, já que é um problema de classificação. A partir disso preciso transformar minhas variáveis em dummies então optei por descartar qualqer variável que tivesse algum valor único não numérico, como nome, ou até mesmo variáveis como o bairro, pois deixaria o modelo extremamente pesado então utilizei as seguintes variáveis: latitude, longitude, price, minimo_noites, numero_de_reviews, reviews_por_mes, calculado_host_listings_count, disponibilidade_365 e bairro_group, room_type. O modelo de DecisionTreeRegressor foi escolhido por se aproximar do conjunto de dados, por conseguir trabalhar com diversos tipos de dados e por ser um modelo onde possa se predizer um valor, não necessitando ser algo binário, os contras é que existem chances dele se tornar extremamente overfittado. E por fim a performance escolhida foi de acurácia avaliada pelo R2.
- Além dos testes gerados pelas próprias biibliotecas, também foi testado num suposto aluguel que supria todas as variáveis. Esses dados separados tinham como objetivo o teste da previsão do valor do preço e os resultados estão junto com os códigos no Jupyter Notebook.

## Autores

[@EduardoFonteneli](https://www.linkedin.com/in/carlos-eduardo-fontineli-goncalves/)
