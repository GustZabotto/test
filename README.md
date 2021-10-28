
![159228906_3690079687713312_5035028843487831689_n](https://user-images.githubusercontent.com/91633230/138770250-597152ee-c3e7-4e9a-9a63-1d98c3eae343.png)

# Descritivo Técnico - Travelex. 


### Sumário:

1. Introdução
2. Nomenclatura
3. Ingestões da dados
4. Tratamentos de dados
5. Visualizações de dados
6. Complementos

## 1. Introdução

O Semantix Data Plataform ou SDP, é uma plataforma que tem como oferecimento um produto para o trabalho e compreensão de dados. A partir de ferramentas implementadas, o SDP busca trabalhar com diversos conectores de bancos, com a possibilidade de ingestões, manuseamento, manipulações de dados e com visualizações para regra de negócio. Além disso, tudo isso em uma plataforma com controle de acessos e segurança.

![GIF_SDP_NOTEBOOK_03](https://user-images.githubusercontent.com/91633230/138770478-23e9046d-be95-4aaf-95dd-f10aae6c184f.gif)

O objetivo desse descritivo técnico tem como finalidade demonstrar os passos utilizados para o desenvolvimento do projeto, sendo composto por algumas etapas. Sendo a primeira etapa a ingestão de dados, na qual foi utilizado o Apache NiFi para captura de dados para camada RAW. A segunda, o tratamento de dados constituído por uma série de validações com scripts python, que foram feitos em uma funcionalidade da Semantix Data Plataform (SandBox) ingeridos na camada TRUSTED. Para a próxima etapa temos a visualização de dados que após as manipulações, tratamentos da base e com o entendimento do negócio, temos as criações de Charts (Gráficos) obtidos da camada SERVICE que foram adicionados em um DashBoard (Painel resumo).

## 2. Nomenclatura

Como o processo se desenvolve em camadas, sendo elas RAW, TRUSTED, SERVICE e a VIEW. Foram adicionadas nomenclaturas padrões para a identificação de cada uma na plataforma.

Para tabelas no formato original (RAW):

- raw.{nome}_tabela_original 

Para tabelas no formato higienizadas (TRUSTED):

- trusted.{nome}_hig

Para tabelas no formato final refinada (SERVICE):

- service.{nome}_hig

Para tabelas no formato visualização (VIEW):

- service.{nome}_view

Para colunas em transformações personalizadas (VIEW):

- {nome}_new

** Observação: Jobs não disponíveis 


## 3. Ingestões de dados

### Ingestão pelo Apache NiFi

Para a ingestão full de dados na camada RAW foi utilizado a ferramenta Apache NiFi, software para automatizar o fluxo de dados entre sistemas de software. Essa ferramenta possui uma interface para criar, monitorar e controlar os fluxos de dados.

Seguimos com a criação de três blocos para a ingestão da carga full para RAW. Sendo o bloco “Arquivos Excel” criado para captura de arquivos do Excel, “Arquivos CSV” criado para a captura de arquivos em CSV e “Ingestoes_RAW_Travelex” bloco que permite a conexão direta ao banco de dados podendo ser inseridas automaticamente em nosso ambiente. 

![image](https://user-images.githubusercontent.com/91633230/138886377-143f1781-731c-4433-a71a-f190574565b2.png)

Dentro do bloco "Ingestoes_RAW_Travelex" há dois fluxos, sendo um deles para fazer a carga full da tabela tb_documento e a outro para fazer a carga full da tabela cubo clientes.

![image (1)](https://user-images.githubusercontent.com/91633230/138887385-46186d92-de8e-4dbe-9554-86128d1344b0.png)

### Ingestão pelo SDP

Contudo, apesar da utilização da ferramenta Apache NiFi para ingestão, existe a opção de ser feito pela própria plataforma. Entretanto, essa funcionalidade está temporariamente desabilitada.

## 4. Tratamentos de dados

Para os tratamentos de dados na camada RAW e a inserção para camada TRUSTED, temos as manipulações feitas com a utilização dos scripts Python na SandBox. Visto que na mesma, os scripts foram fragmentados em duas páginas no Jupyter, com cada página dedicada para determinada tabela. Nas bibliotecas, usamos validate_docbr e pycep-correios para validação de CEP, CPF e CNPJ, sqlalchemy para conexão no banco e manipulação dos dados juntamente com pandas sendo uma das mais utilizadas por sua completude baseando-se em data frame e manipulações, por fim, foram adicionadas algumas bibliotecas de datetime, para validações de datas de nascimento e idade. Segue abaixo os blocos utilizados para execução desse tratamento.   

### Validações

São efetuados cálculos ou a implementação de uma lógica com a capacidade de verificar a veracidade dos dados implementados pelas tabelas abaixo:
- A tabela documento faz as seguintes validações:
- Validação do CPF;

![CPF](https://user-images.githubusercontent.com/73028088/139148358-1850cf3c-3fcb-422a-9bed-8432a0c9ff40.png)

- Validação de CNPJ;

![CNPJ](https://user-images.githubusercontent.com/73028088/139148437-e2ea94d3-0a16-4bc7-bba1-96042a34f02e.png)

- Validação do RG;

![RG](https://user-images.githubusercontent.com/73028088/139148980-97f45621-f810-483c-b3c3-e89db86dcfa8.png)

- Alguns exemplos da tabela cubo_clientes:

- Validação de CEP;

![CEP](https://user-images.githubusercontent.com/73028088/139148623-9b33dc85-d0b6-445e-ae31-48465a9db490.png)

- Validação de E-mail;

![EMAIL](https://user-images.githubusercontent.com/73028088/139149088-baeecdc0-b73d-419a-8a9f-3017be385505.png)

- Validação de Telefones Brasileiros;

![TEL_BR](https://user-images.githubusercontent.com/73028088/139149222-fad8df8b-345a-4bc3-ba5b-397595613b39.png)

- Validação de Telefones Estrangeiros;

![TEL_EST](https://user-images.githubusercontent.com/73028088/139149300-b2651aad-893b-41e7-9ba8-7f6be20ea641.png)


### Higienização 

Padronização nos dados.
- Ambos fazem as seguintes higienizações, que consistem em remoção de acentuações, caracteres especiais e transforma as colunas em upper case, entre outras higienizações.
- Remoção de acentos;

![ACENTOS](https://user-images.githubusercontent.com/73028088/139149866-2efdccd2-0302-41cc-9363-b735c55504cd.png)

-  Remoção de caracteres especiais; 

![CARAC_ESP](https://user-images.githubusercontent.com/73028088/139150039-3a42e58a-88c1-4eb2-b552-028658e1b230.png)

- Transformação dos campos para upper case;

![UPPER_CASE](https://user-images.githubusercontent.com/73028088/139150141-d1fde7f8-dbce-4905-bdf9-9ee308cf6187.png)

- Há também algumas outras higienizações, que diferencia de tabela para tabela, aqui vai alguns exemplos da tabela documento:
- Função que faz o tratamento do CPF com a função lambda;

![CPF_HIG](https://user-images.githubusercontent.com/73028088/139150570-620c18aa-4c85-4bdc-8283-c993194c61a8.png)

- Função que faz o tratamento do CNPJ com a função lambda;

![CNPJ_HIG](https://user-images.githubusercontent.com/73028088/139150721-c23cf4fa-d1ec-4ceb-a119-d10c012ec49e.png)

- Função que faz o tratamento do RG com a função lambda;

![RG_HIG](https://user-images.githubusercontent.com/73028088/139150843-f00d7176-e45b-43fc-b9e8-56c58c8307f3.png)

- Alguns exemplos da tabela cubo_clientes:

- Função que faz o tratamento do CEP com a função lambda;

![CEP_HIG](https://user-images.githubusercontent.com/73028088/139151129-1cf6bbc9-f225-4f53-9d70-5052a18429b2.png)
- Função que faz o tratamento e do E-MAIL com a função lambda;

![EMAIL_HIG](https://user-images.githubusercontent.com/73028088/139152064-df9d97f5-7172-4823-bfcc-209d7ea98566.png)
- Função que faz o tratamento do TELEFONE e cria as colunas com os dados higienizados;

![TELEFONE_HIG](https://user-images.githubusercontent.com/73028088/139152404-9ee6eaa9-f09e-4ef4-a19a-c2d67ff3b8ee.png)


### BlackList e Depara

As Blacklists (a tradução literal é “Lista Negra”) trata-se de tabelas que agrupam dados não validados, evitando então a inserção de dados irreais na camada SERVICE. Segue abaixo alguns exemplos sobre e-mails da tabela “Blacklist”: 

![black](https://user-images.githubusercontent.com/91633230/138929703-b29d3827-df6c-4a67-b0a2-b47151a91b53.png)

Já o termo “Depara”, tem um algoritmo com a capacidade de identificar dados não validos, mas que exista a possibilidade de recuperação, devido ao um erro ortográfico, erro de digitação e entre outros. Segue abaixo alguns exemplos sobre e-mails da tabela Depara:  

![depara](https://user-images.githubusercontent.com/91633230/138929721-b9576718-56e8-495d-b01c-79707576c9cb.png)


## 5. Visualizações de dados

Na camada de visualização, temos que as manipulações de dados feitas via SQL usando DQL (Data Query Language) em outra funcionalidade da Semantix Data Plataform (SQL Lab). Sendo que ela permite a criação e edição de Charts (Gráficos), Datasets e Databases. 

![dash](https://user-images.githubusercontent.com/91633230/138911107-6ea146b5-f692-4528-9538-7e4362af9a6f.png)

Acima contém um dashboard da plataforma, apresentando de forma geral, informações pertinentes as tabelas de “BlackList” e “Depara”. São cartões de uma amostra que mostram a quantidade total de E-mails, celulares e telefones enviados para tabela BlackList ou Depara.

![dash2](https://user-images.githubusercontent.com/91633230/138946894-564a346d-f703-4b0a-a188-7dfb6a79dae3.png)

Segue outro exemplo de Dashboard, que contém gráficos ou tabelas que proporcionam a comparação da totalidade de cada item. Por exemplo, em tipo de documento, é possível verificar o total de RG, CPF e entre outros que foram cadastrados. Além do tipo de documento, a imagem apresenta tipo de cadastro, tipo de parceria com a corretora e situação do cliente com a corretora.

## 6. Complementos

### Catálogo

Foi escolhido o DataHub na parte de dicionário de dados, uma ferramenta open-source para dados estruturados em que terá diversos features na plataforma. Nela será possível as verificações das descrições das tabelas e dos gráficos para um maior entendimento. Visto que, é uma ferramenta intuitiva, viabilizando uma procura de grande facilidade que são feitas por tags até a modificação de alguma coluna caso necessário.

### Controle de acessos

Para o controle de acesso, foi utilizado a ferramenta Apache Ranger, uma ferramenta de código aberto na qual é possível habilitar, monitorar e gerenciar a segurança de dados.
Atualmente o nível de acesso é por nível de objeto, e futuramente será habilitado a nível de linha. 

### Ambientes separados

Foram desenvolvidos dois ambientes, um para homologação (Confidence - Travelex) e outro para produção (Travelex Prod). No nosso ambiente de homologação, estão contidos testes feitos em amostras ocorrendo higienizações, tratamentos das tabelas e geração de gráficos. Consequentemente, após as validações, foram transferidos para o ambiente de produção, na qual se passou utilizar a carga full.
