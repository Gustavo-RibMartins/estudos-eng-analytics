# Big Data

Peso de 25% na prova

---

## 1. O que é Big Data

> O que é Big Data, quais seus principais desafios (armazenamento, integração, análise e suporte "Fast Data").

É uma nova geração de tecnologias e arquiteturas, desenhadas de maneira econômica para extrair **valor** de grandes **volumes** de dados, provenientes de uma **variedade** de fontes, permitindo alta **velocidade** na captura, exploração e análise dos dados.

O contexto tradicional de bancos relacionais apresenta limitações em escalonamento, surgindo a oportunidade de realizar **computação paralela** usando hardware de baixo custo.

### 1.1) 5 Vs do Big Data

**Volume**: quantidades de dados na ordem de TB, PB;
**Variedade**: dados em diversos formatos diferentes (logs, DBs relacionais, JSON, IOT);
**Velocidade**: dados chegando de forma contínua;
**Veracidade**: é preciso extrair informações confiáveis dos dados para tomada de decisão;
**Valor**: só faz sentido ter uma infra de big data, se isso traz algum valor (financeiro, por ex.).

### 1.2) Fast Data

![](../Imagens/FastData.png)

[Fonte](https://blog.dsacademy.com.br/fast-data-a-evolucao-do-big-data/)

Por muito tempo, o volume foi o foco no Big Data, mas cada vez mais o mundo muda de uma forma mais rápida, e para garantir competitividade, as empresas precisam extrair valor dos dados em formatos variados com maior velocidade.

Fast Data é coletar os dados em tempo real para tomada de decisão.

Em arquiteturas fast data, diferente do processamento batch tradicional feito durante a noite, os eventos individuais são processados à medida que chegam, na ordem de milissegundos (processamento de streaming).

---

## 2. Tipos de Processamento

> Quais os tipos de processamento de dados, ETL vs ELT e análise de complexidade e aplicabilidade em cenários reais.

**ETL**: Extract-Transform-Load - primeiro você extrai os dados de um sistema origem, transforma esses dados que estão em formato raw (muitas vezes sem estrutura) e os deixa mais legíveis para serem trabalhados pelo analista de dados ou ferramenta de dataviz. Por fim, você carrega esses dados em algum repositório para serem consumidos.

**ELT**: Extract-Load-Transform - primeiro extraímos e depois carregamos os dados no repositório de destino, fazendo a transformação apenas no final. Com o contexto da nuvem (armazenamento escalável e barato), então é mais fácil armazenar a informação para somente transforma o que for necessário.

---

## 3. Camadas de Dados

> Camadas de dados e sua relevância (Source of Record, Source of Truth, Specialized).

Um Data Lake é uma estrutura que visa armazenar um volume imenso de dados provenientes de diversas fontes.

Porém, se mal gerenciado, pode gerar um cenário de falta de controle sobre quais informações estão disponíveis, onde elas se encontram, por quanto tempo são válidas, quem deveria ter acesso e etc.

Para evitar isso, é eseencial aplicar a **governança de dados**, tanto em rotinas operacionais quanto nos frameworks usados na arquitetura.

A prática da divisão em zonas ajuda na organização e a governança dos data lakes, evitando que a estrutura acabe descontrolada e desorganizada (virando um Data Swamp).

O padrão é a divisão do Data Lake em 4 zonas:

![DataLake](../Imagens/DataLake.png)

**Transient Zone**

Zona transitória onde os dados são ingeridos pelo Data Lake. Aqui pode-se iniciar o processo de governança com catalogação das origens e tipos de dados que estão entrando.

Depois que os dados ingeridos forem alocados na Raw Data Zone, os arquivos aqui são excluídos, tornando essa uma zona de arquivos temporários.

**Raw Data Zone**

Zona de dados brutos armazenados de todas as fontes relevantes, independente de quanto será consumido de imediato. Dados brutos que ainda não receberam tratamentos para serem consumidos em análises tradicionais.

**Trusted Zone**

Dados já tratados. Sofreram as transformações necessários para serem consumidos e já possuem garantias de Data Quality, podendo ser considerados exatos e confiáveis.

**Refined Zone**

Dados tratados e enriquecidos, estando prontos para serem consumidos por aplicações externas.

Justamente por esse uso, essa camada costuma ser construída com infraestrutura de bancos de dados relacionais (SQL Server, Oracle, etc.), facilitando a conexão com APIs e sistemas transacionais.

### 3.1) Camadas no Data Mesh



---

## 4. Tipos de dados

> Tipos de dados (estruturados, semiestruturados, não estruturado) e formatos comuns utilizados (izo, parquet, orc, avro, xml, json).

### 4.1) Dados Estruturados

* Esquema fixo;
* Formato bem definido;
* Conhecimento prévio da estrutura de dados;
* Simplicidade para relacionar informações;
* Dificuldade para alterar o modelo.

Exemplos: Tabelas de um banco de dado relacional.

### 4.2) Dados Semi-estruturados

 Categoria entre dados estruturados e não estruturados. Não se limitam a uma estrutura rígida como em bancos de dados relacionais, mas possuem metadados ou tags semânticas para serem gerenciados.

 Por exemplo, uma foto que você tira possui atributos estruturados como geotag, ID do dispositivo, carimbo de data/hora. Depois de salvá-la podemos atribuir outras tags a imagem como "animal de estimação" ou "cachorro".

 ### 4.3) Dados não estruturados

 Não possuem formato pré-definido. Pode ser um parágrafo de um livro, postagens de mídia social, imagens de satélite, etc.

### 4.4) Formatos de arquivos para Big Data

- Formatos menos utilizados em Data Lakes: XML, LOG e CSV;
- Formatos mais usados em Data Lakes: Parquet, Avro, ORC,

#### 4.4.1. XML

Muito comum em ferramentas de ERP que trabalham com dados de notas fiscais. Usa o conceito de chave-valor mas, diferente do JSON, as chaves são TAGs e os valores vão dentro das TAGs, bem parecido com HTML.

![](../Imagens/arquivo-xml.png)

#### 4.4.2. LOGs

Possuem formato de linha do tempo, sempre possuem um timestamp com data e hora.

![](../Imagens/arquivo-log.png)

#### 4.4.3. JSON

JavaScript Object Notation: funciona no modelo de chave-valor. O grande benefício do JSON é poder armazenar todas as informações de um objeto de forma agrupada e não impor schema rígido as estruturas.

![](../Imagens/arquivo-json.png)

#### 4.4.4. Parquet

O Parquet é um formato Open Source construído para o ecossistema Hadoop destinado ao armazenamento de dados estruturados. Assim como o HDF5, ele surge com a ambição de trabalhar com conjuntos de dados massivos, tendo em seu funcionamento uma abordagem diferente da tradicional orientada por linhas, onde cada linha armazena uma observação distinta. No Parquet, em cada linha é registrado todos os valores da coluna, o que permite uma **compressão mais eficiente**, sendo portanto, pouco custoso no disco.

Em um CSV quando você faz uma consulta, você lê o arquivo todo. Por exemplo, em um arquivo com 20 bilhões de linhas e 300 colunas, você teria que ler o arquivo todo mesmo que precisasse apenas de uma coluna com 100 mil linhas.

Exemplo:

Dado no CSV
![](../Imagens/parquet-dadoCSV.png)

Dado no Parquet
![](../Imagens/parquet-dadoParquet.png)

Como desvantagem, sobressai o fato do formato restringir-se a dados estruturados, sendo menos felxível que o HDF5, o arquivo ser binário e a não existência de suporte em editores de planilhas.

Comparação entre Parquet x CSV:
![](../Imagens/parquet-vs-csv.png)
[Fonte](https://www.databricks.com/br/glossary/what-is-parquet#:~:text=Caracter%C3%ADsticas%20do%20Parquet&text=Formato%20baseado%20em%20colunas%3A%20os,bancos%20de%20dados%20OLTP%20tradicionais.)

#### 4.4.5. Avro

O Avro funciona com uma estrutura de sub itens de um item assim como o JSON, até existe no Parquet como família de colunas (estilo Cassandra) mas não funciona muito bem, o Avro é melhor para isso assim como o JSON (Estrutura de dados "Nested").

![](../Imagens/avro-file.png)

Um ponto negativo do Avro em relação ao Parquet, é que quando uma informação é requerida, ele lÊ todo o arquivo e não só a parte que precisa como no Parquet. O Avro é mais indicado para gravação do que para leitura.

#### 4.4.6. ORC

É uma evolução do Parquet que trabalha de forma mais rápida e com menor armazenamento. Também utiliza o modelo colunar do Parquet e os mesmos princípios de trazer só o que realmente é necessário.

![](../Imagens/orc-file.png)

#### 4.4.7. Comparação

![](../Imagens/comparacao-arquivos.png)

#### 4.4.8. Compressão x Compactação

Existem duas formas de se reduzir o tamanho de armazenamento dos arquivos, pela compressão e pela compactação, os quais são processos distintos.

**Compressão**: a quantidade de bits usados para representar os dados são refuzidos;

**Compactação**: é realizada a união de dados que estavam separados, como na desfragmentação de disco de um computador.

A compressão é realizada por meio de diversos algoritmos de compressão, os quais irão reduzir a quantidade de bytes que representam um dado. A compressão também ajuda na remoção de redundância, onde por exemplo, "BBBBBB" que ocupa 6 bytes pode ser representado por "6B", que ocupa 2 bytes. Com isso, há uma redução do tamanho do arquivo e no armazenamento.

A compressão depende do tipo de armanzenamento:

* Formato baseado em linha: CSV, Avro e JSON;
* Formato baseado em coluna: Parquet e ORC.

Os arquivos baseados em linha são muito rápidos na escrita e lentos na leitura. Os baseados em coluna são o contrário.

Além disso, dados com armazenamento colunar possuem uma grande vantagem em relação ao armazenamento em linha, pois o algoritmo aplica a compressão em dados que possuem o mesmo tipo (str, int, float, etc), já o em linha isso tende a ser o oposto, caso atabela possua colunas com tipos de dados distintos, gerando uma taxa de compressão menor.

![](../Imagens/nivel-compressao.png)

**Algoritmos de Compressão**

* Gzip;
* Bzip2;
* Snappy;
* LZO.

![](../Imagens/comparacao-comparacao.png)

---

## 5. Métricas de qualidade

> Qual a importância e quais métricas de qualidade de dados devem ser utilizadas em pipelines de dados.

---

## 6. Infraestrutura de Sistemas Distribuídos

> O que é o ambiente Hadoop, quais ferramentas o compõe, vantagens e desvantagens do paradigma de programação MapReduce.

### 6.1) Ecossistema Hadoop

Componentes do Hadoop Core:

* HDFS: sistema de armazenamento distribuído
* MapReduce: modelo de programação para processamento paralelo
* YARN: gerenciador de recursos do cluster Hadoop

#### 6.1.1. HDFS

Hadoop Distributed FileSystem é um componente do Hadoop Core para armazenar volumes massivos de dados de forma distribuída em um cluster de computadores.

O HDFS trabalha com um conceito de **write once/ read many** que, por sua vez, indica um padrão de utilização onde os usuários realizam a escrita de grandes quantidades de dados uma única vez e realizam a leitura múltiplas vezes. Neste cenário, o tempo para leitura de todo o conjunto de dados é mais importante do que a latência em ler o primeiro registro.

O HDFS também possui o conceito de **hardware commodity**, pois não precisa de máquina poderas, equipamentos comuns e de baixo custo podem ser usados no cluster.

> **Cenários em que o HDFS não é adequado**
>
> * Padrões de acesso com baixa latência
> * ExistÊncia de small files
> * Grande quantidade de modificações em arquivos

O HDFS trabalha com "Blocos de Armazenamento" de 128MB (ou 256MN em alguns cenários) canalizando o posicionamento de um grande volume de dados em chunks.

![](../Imagens/HDFS.png)

Um arquivo de grande volume é **particionado** e tem suas partes armazenadas separadamente em cada bloco (que é um nó no cluster).

**Replicação de Dados no Cluster**

Por padrão, sempre que um grande volume de dados é armazenado no cluster de computadores, existe um fator de replicação que automaticamente realiza cópias dos blocos em múltiplos nós do sistema.

![](../Imagens/HDFS-replication.png)

**Arquitetura do HDFS**

* Namenodes (master): gerencia toda a árvore do sistema de armazenamento e os metadados para todos os arquivos e diretórios presentes. Os namenodes mantém um arquivo conhecido como **edit log** responsável por registrar informações sobre o que é criado, mantido ou alterado no cluster. Além disso, possuem informações de todos os datanodes do sistema.

* Datanodes (workers): atuam como os verdadeiros trabalhadores do cluster. São eles que armazenam os dados em blocos e retornam, sempre que solicitados, informações para o namenode para que este saiba exatamente a localização dos arquivos.

![](../Imagens/HDFS-architecture.png)

**Recuperação à Falhas**

Considerando a arquitetura acima, é possível notar que o namenode é um ponto crítico de falha do sistema. Sua inexistência impede por completo a utilização do HDFS, visto a impossibilidade de obter informações de metadados e localidade dos dados nos blocos presentes nos datanodes do cluster.

Para contornar isso, é possível:

* **Realizar o backup dos metadados**: realizar backups periódicos locais ou em um outro sistema de arquivos para retomar a operação em caso de falhas. Nesta abordagem, eventualmente alguns dados serão perdidos, dado que a retomada do sistema pode ter algum delay;

* **Manter um secondary namenode**: apenas do nome intuitivo, não há um namenode secundário executando ao mesmo tempo que o primário. Basicamente, cópias dos arquivos importantes do namenode são mantidas em uma máquina separada no cluster para que, em eventuais falhas, o sistema possa ser recuperado.

#### 6.1.2. MapReduce

Motor de processamento distribuído que funciona com funções de mapeamento (map) e redução (reduce) que utilizam entradas e saídas baseadas em conjuntos de chave e valor. Cada uma dessas etapas possuem responsabilidades específicas na dinâmica de processamento dos dados:

* **Map**: funções de mapeamento são normalmente usadas para filtrar, transforma ou converter dados;
* **Reduce**: já as funções de redução, atuam na sumarização e agregação dos dados.

![](../Imagens/MapReduce-Process.png)

1. Os jobs (programas) submetidos no cluster Hadoop são divididos em tasks (tarefas);
2. As tasks são então distribuídas para os nós do cluster (datanodes);
3. Processos em Java são iniciados para o processamento dos dados;
4. Neste ponto, dados do sistema distribuído (HDFS) são lidos conforme a requisição;
5. Inicia-se a fase de mapeamento de acordo com a solicitação realizada;
6. A saída da fase de mapeamente é então submetida a uma fase de redução, conforme a solicitação realizada;
7. O resultado final é escrito novamente no HDFS.

NA fase de **map**, cada task individual recebe uma porção dos dados. Assim, o número de tasks estabelecidas pelo sistema para atuar no job depende da quantidade de dados.

Exemplo de uma etapa de mapeamente para obter a quantidade de vendas por vendedor:

![](../Imagens/MapReduce-Map.png)

> **Observação**: no exemplo acima foi aplicado um filtro (amout > 1.000) e selecionadas apenas as colunas relevantes para o resultado desejado. Ambas as operações são tasks de mapeamento, assim como transformações e qualquer outra operação em cenário de um pra um.

Na sequência, a solicitação passa por um processo de "shuffle and sort" antes de chegar à fase de redução.

**Shuffle and Sort** é um processo intermediário que as vezes é necessário e que faz a unificação dos dados de todas as tarefas de map executadas em cada datanode de modo a criar um input facilitado para a subsequente tarefa de reduce.

![](../Imagens/MapReduce-ShuffleSort.png)

Por fim, a etapa de reduce é onde ocorrem as agregações:

![](../Imagens/MapReduce-Reduce.png)

#### 6.1.3. YARN

O YARN é o gerenciador de recursos de um cluster Hadoop.

> YARN = Yet Another Resource Negotiator.

O funcionamento do YARN está baseado na disponibilização de APIs responsáveis por entregar informações dos recursos presentes em um cluster de computadores. Em geral, estas APIs são transparentes aos usuários do Hadoop, sendo papel das aplicações de alto nível (como o MapReduce, por exemplo) realizar este contato de modo a tomar ações com base nas informações obtidas. Assim, é correto pontuar que o YARN atua em uma camada separada entre o armazenamento e aplicações de alto nível, sendo um grande intermediador entre as partes.

![](../Imagens/YARN.png)

Ele é basicamente o sistema que gerencia os recursos no cluster de computadores, decidindo quem executa as tarefas, quando as mesmas serão executadas, quais nós estão disponíveis para receber demandas e quais estão totalmente ocupados. O YARN é como o coração que permite o funcionamento do cluster.

O YARN funciona da seguinte forma:

![](../Imagens/YARN-esboco.png)

**Application client**: programa solicitado pelo usuário. Pode ser um job de MapReduce, por exemplo.

**Resource Manager**: gerencia e aloca recursos do cluster. Possui dois principais elementos: o `scheduler` e o `application manager`. Atua como um agendador global de recursos.

**Node Manager**: presente em todos os nós do cluster. Executa e monitora os containers.

**Container**: referência ao pacote de recursos incluindo RAM, CPU, Rede, HD, entre outros. Responsável por executar a aplicação com um conjunto restrito de recursos disponibilizados. Dependendo de como o YARN é configurado, um container é basicamente um processo Unix ou um cgroup Linux.

**Application Process**: basicamente é o job submetido ao framework utilizado (ex: MapReduce).

---

## 7. Framework Spark

> Suas características, conceitos, sintaxe, vantagens e desvantagens.

Apache Spark é um framework de processamento de dados em larga escala que foi desenvolvido para ser rápido, fácil de usar e escalável. Ele é projetado para trabalhar com grandes conjuntos de dados distribuídos em clusters de computadores.

Ele utiliza cache na memória e execução de consulta otimizada para consultas analíticas rápidas em dados de qualquer tamanho.

Ele fornece APIs de desenvolvimento em **Java, Scala, Python e R** e suporta a reutilização de código em várias cargas de trabalho - processamento em lote, consultas interativas, análise em tempo real, aprendizado de máquina e processamento de grafos.

Com relação ao Hadoop MapReduce o Spark fornece os seguintes benefícios:

* Mais rápido;
* Amigável ao desenvolvedor;
* Múltiplas cargas de trabalho;
* Podemos utilizar diferentes linguagens de programação com Spark.

![](../Imagens/Spark-Core.png)

* O módulo **Spark SQL** contém sintaxe que os usuários de Pandas e SQL acharão familiar;
* O módulo **Spark MLlib** pode ser usado para implementar muitos modelos populares de aprendizado de máquina;
* O módulo **GraphX** para processamento de grafos;
* O módulo **Spark Streaming** que é um mecanismo de processamento de stream escalável e tolerante a falhas desenvolvido sobre o mecanismo Spark SQL.

**Spark Core** é a base da plataforma. É responsável pelo gerenciamento de memória, recuperação de falhas, agendamento, distribuição e monitoramento de jobs e interação com os sistemas de armazenamento. O Spark Core é exposto por meio de uma interface de APIs construídas em Java, Scala, Python e R. Essas APIs escondem a complexidade do processamento distribuído por trás de operadores simples de alto nível.

## 7.1. PySpark

PySpark é uma API em Python para executar o Spark e foi lançado para oferecer suporte à colaboração entre Apache Spark e Python. O PySpark também oferece suporta à interface do Apache Spark com conjuntos de dados distribuídos resilientes (RDDs) na linguagem de programação Python. Isso é obtido aproveitando a biblioteca Py4J.

Os **RDDs** são a principal abstração de dados do Spark. Eles são coleções distribuídas de objetos e podem ser armazenados em memória ou no disco. O RDD é imutável, ou seja, uma vez criado, você não pode alterá-lo (mas pode criar uma cópia com as transformações necessárias).

Imagine o RDD como uma tabela do banco de dados que pode guardar qualquer tipo de dado. O Spark armazena os dados do RDD em diferentes partições. Isso ajuda a reorganização computacional e otimização no processamento dos dados.