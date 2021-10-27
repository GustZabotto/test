
![159228906_3690079687713312_5035028843487831689_n](https://user-images.githubusercontent.com/91633230/138770250-597152ee-c3e7-4e9a-9a63-1d98c3eae343.png)

# Descritivo Técnico - Travelex. 


### Sumário:

1. Introdução
2. Ingestões da dados
3. Tratamentos de dados
4. Visualizações de dados
5. Complementos

## 1. Introdução

O Semantix Data Plataform ou SDP, é uma plataforma que tem como oferecimento um produto para o trabalho e compreensão de dados. A partir de ferramentas implementadas, o SDP busca trabalhar com diversos conectores de bancos, com a possibilidade de ingestões, manuseamento, manipulações de dados e com visualizações para regra de negócio. Segue abaixo um gif apresentando o processo.  

![GIF_SDP_NOTEBOOK_03](https://user-images.githubusercontent.com/91633230/138770478-23e9046d-be95-4aaf-95dd-f10aae6c184f.gif)

O objetivo desse descritivo técnico tem como finalidade demonstrar os passos utilizados para o desenvolvimento do projeto, sendo composto por algumas etapas. Sendo a primeira etapa a ingestão de dados, na qual foi utilizado o Apache NiFi para captura de dados para camada RAW. A segunda, o tratamento de dados constituído por uma série de validações com scripts python, que foram feitos em uma funcionalidade da Semantix Data Plataform (SandBox) ingeridos na camada TRUSTED. Para a próxima etapa temos a visualização de dados que após as manipulações, tratamentos da base e com o entendimento do negócio, temos as criações de Charts (Gráficos) obtidos da camada SERVICE que foram adicionados em um DashBoard (Painel resumo).

## 2. Ingestões de dados

Para a ingestão full de dados na camada RAW foi utilizado a ferramenta Apache NiFi, software para automatizar o fluxo de dados entre sistemas de software. Essa ferramenta possui uma interface para criar, monitorar e controlar os fluxos de dados.

Seguimos com a criação de três blocos para a ingestão da carga full para RAW. Sendo o bloco “Arquivos Excel” criado para captura de arquivos do Excel, “Arquivos CSV” criado para a captura de arquivos em CSV e “Ingestoes_RAW_Travelex” bloco que permite a conexão direta ao banco de dados podendo ser inseridas automaticamente em nosso ambiente. 

![image](https://user-images.githubusercontent.com/91633230/138886377-143f1781-731c-4433-a71a-f190574565b2.png)

Dentro dos blocos há dois fluxos, sendo um deles para fazer a carga full da tabela tb_documento e a outro para fazer a carga full da tabela cubo clientes.

![image (1)](https://user-images.githubusercontent.com/91633230/138887385-46186d92-de8e-4dbe-9554-86128d1344b0.png)

## 3. Tratamentos de dados

Para os tratamentos de dados da camada RAW e a inserção para camada TRUSTED, temos as manipulações feitas com a utilização dos scripts python pela SandBox. Segue abaixo os blocos utilizados para execução desse tratamento. 

### Validações

São efetuados cálculos ou a implementação de uma lógica com a capacidade de verificar a veracidade dos dados.
- Validação do CPF;
- Validação do RG;
- Validação de CNPJ; 
- Validação de E-mail;
- Validação de Telefone;
- Validação de Nome;

### Higienização 

Padronização nos dados.
- Remoção de acentos;
- Remoção de caracteres especiais; 
- Transformação dos campos em branco para “NULL”;
- Remoção das duplicatas;

### BlackList e Depara

As Blacklists (a tradução literal é “Lista Negra”) trata-se de tabelas que agrupam dados não validados, evitando então a inserção de dados irreais na camada SERVICE. Segue abaixo alguns exemplos sobre e-mails da tabela “Blacklist”: 

![black](https://user-images.githubusercontent.com/91633230/138929703-b29d3827-df6c-4a67-b0a2-b47151a91b53.png)

Já o termo “Depara”, tem um algoritmo com a capacidade de identificar dados não validos, mas que exista a possibilidade de recuperação, devido ao um erro ortográfico, erro de digitação e entre outros. Segue abaixo alguns exemplos sobre e-mails da tabela Depara:  

![depara](https://user-images.githubusercontent.com/91633230/138929721-b9576718-56e8-495d-b01c-79707576c9cb.png)


## 4. Visualizações de dados

Na camada de visualização, temos que as manipulações de dados feitas via SQL usando DQL (Data Query Language) em outra funcionalidade da Semantix Data Plataform (SQL Lab). Sendo que ela permite a criação e edição de Charts (Gráficos), Datasets e Databases. 

![dash](https://user-images.githubusercontent.com/91633230/138911107-6ea146b5-f692-4528-9538-7e4362af9a6f.png)

Acima contém um dashboard da plataforma, apresentando de forma geral, informações pertinentes as tabelas de “BlackList” e “Depara”. São cartões de uma amostra que mostram a quantidade total de E-mails, celulares e telefones enviados para tabela BlackList ou Depara. Segue outro exemplo de Dashboard, que contém gráficos sobre tipo de cadastro, tipo de documento, tipo de parceria com a corretora e situação do cliente com a corretora.  

![dash2](https://user-images.githubusercontent.com/91633230/138946894-564a346d-f703-4b0a-a188-7dfb6a79dae3.png)



## 5. Complementos

### Catálogo
### Controle de acessos
### Ambientes separados
