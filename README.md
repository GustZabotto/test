
![159228906_3690079687713312_5035028843487831689_n](https://user-images.githubusercontent.com/91633230/138770250-597152ee-c3e7-4e9a-9a63-1d98c3eae343.png)

# Descritivo Técnico - Travelex. 


### Sumário:

1. Introdução
2. Ingestões da dados
3. Tratamentos de dados
4. Visualizações de dados
5. Complementos

## 1. Introdução

![GIF_SDP_NOTEBOOK_03](https://user-images.githubusercontent.com/91633230/138770478-23e9046d-be95-4aaf-95dd-f10aae6c184f.gif)

O objetivo desse descritivo técnico tem como finalidade demonstrar os passos utilizados para o desenvolvimento do projeto, sendo composto por três etapas. Sendo a primeira etapa a ingestão de dados, na qual foi utilizado o Apache NiFi para captura de dados para camada RAW. A segunda, o tratamento de dados constituído por uma serie de validações com scripts python, que foram feitos em uma funcionalidade da Semantix Data Plataform (SandBox) ingeridos na camada TRUSTED. Para a próxima etapa temos a visualização de dados que após as manipulações, tratamentos da base e com o entendimento do negócio, temos as criações de Charts (Gráficas) que foram adicionadas em um DashBoard (Painel resumo).

## 2. Ingestões da dados

Para a ingestão de dados na camada RAW foi utilizado a ferramenta Apache NiFi, software para automatizar o fluxo de dados entre sistemas de software. Na qual possui uma interface para criar, monitorar e controlar os fluxos de dados 

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
- Remoção das duplicatas
### BlackList e Depara
O termo BlackList tem como ideia a criação de uma tabela geral na qual há inserção de dados não validos. Já o termo “Depara”, tende revisar os dados não validos, podendo assim, recuperar algumas informações.

## 4. Visualizações de dados

Na camada de vizualicação temos para manipulação de dados via SQL usando DQL (Data Query Language) no SQL Lab e a criação de Dashboards e Charts,
onde é possível também a verificar e editação dos Datasets e Databases. Aqui está um exemplo de um Dashboard feito para controle de dados inválidos e
dados para possível revisão.

## 5. Complementos

### Catalogo
### Controle de acessos
### Ambientes separados
