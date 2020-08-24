# Provisões de Emergência
Trabalho desenvolvido durante a disciplina de BD1

# Sumário

### 1. COMPONENTES<br>
Integrantes do grupo<br>
Kelvin Lehrback Guilherme<br>

### 2.INTRODUÇÃO E MOTIVAÇÃO<br>
Este documento contém a especificação do projeto do banco de dados Provisões de Emergência 
<br>e motivação da escolha realizada. <br>

> A empresa "Devcom Projetos" visa colaborar com desenvolvimento de projetos para uma sociedade melhor. Sabendo-se dos desafios para gerenciar projetos dentro de uma empresa e visando unir as informações relativas a funcionários, departamentos e projetos em um mesmo local, ficamos motivados com o desenvolvimento deste sistema. O Sistema "Devcom" tem como objetivo gerenciar todas as informações ao desenvolvimento das atividades de projetos em diversas localidades do país. Para realizar suas operações adequadamente e empresa necessita que sistema que armazene informações relativas aos Projetos, Departamentos e Empregados, além de também armazenar dados sobre Dependentes e Históricos de Salário dos empregados. O sistema deverá gerar um conjunto de relatórios que por sua vez atenderá os anseios da empresa em questão.
 

### 3.MINI-MUNDO<br>

>O sistema “Provisões de emergência” tem como objetivo contribuir com o  planejamento financeiro de famílias e ONGS, gerando relatórios de preços e/ou dos produtos realmente essenciais para cada realidade num determinado intervalo de tempo. É necessário o cadastro da quantidade de pessoas. Pessoas são cadastradas por meio do nome, CPF, data de nascimento, grupo familiar a qual pertence e o informe se necessitam ou não de medicamentos, se necessário medicamentos, informar o(s) nome(s) do(s) medicamento(s), a dose diária de cada um e o preço médio (se conhecido o preço) ou um previsto. É necessário também informar a quantidade de comida que as pessoas consomem por dia, bem como quais alimentos essenciais para a preparação das respectivas refeições diárias (arroz, feijão, carne, verduras) e seus respectivos preços (médio ou previsto). Há ainda os gastos com produtos de limpeza, seja ele geral(desinfetantes, sabão para roupas etc) ou pessoal (sabonetes, pasta de dente, etc), informar também o preço médio ou previsto. Para a compra dos produtos, é necessário conhecer os fornecedores. Fornecedores possuem nome e quais produtos eles entregam, podendo ter o(s) produto(s) em estoque ou não. O objetivo inicial do sistema é gerar um relatório listando todos os bens de consumo para a sobrevivência num determinado intervalo de tempo, bem como os seus respectivos preços.

### 4.PROTOTIPAÇÃO, PERGUNTAS A SEREM RESPONDIDAS E TABELA DE DADOS<br>
#### 4.1 RASCUNHOS BÁSICOS DA INTERFACE (MOCKUPS)<br>
[Protótipo de telas feito para o sistema "Provisoes de Emergencia" (Arquivo .PDF)](https://github.com/GodKelvin/Provisoes_de_emergencia/blob/master/arquivos/Prototipo_telas.pdf "Provisões de Emergência")

#### 4.2 QUAIS PERGUNTAS PODEM SER RESPONDIDAS COM O SISTEMA PROPOSTO?
    a) O sistema proposto poderá fornecer quais tipos de relatórios e informaçes? 
    b) Crie uma lista com os 5 principais relatórios que poderão ser obtidos por meio do sistema proposto!
    
> A Empresa DevCom precisa inicialmente dos seguintes relatórios:
* Relatório que mostre o nome de cada supervisor(a) e a quantidade de empregados supervisionados.
* Relatório relativo aos os supervisores e supervisionados. O resultado deve conter o nome do supervisor e nome do supervisionado além da quantidade total de horas que cada supervisionado tem alocada aos projetos existentes na empresa.
* Relatorio que mostre para cada linha obtida o nome do departamento, o valor individual de cada salario existente no  departamento e a média geral de salarios dentre todos os empregados. Os resultados devem ser apresentados ordenados por departamento.
* Relatório que mostre as informações relacionadas a todos empregados de empresa (sem excluir ninguém). As linhas resultantes devem conter informações sobre: rg, nome, salario do empregado, data de início do salario atual, nomes dos projetos que participa, quantidade de horas e localização nos referidos projetos, numero e nome dos departamentos aos quais está alocado, informações do historico de salário como inicio, fim, e valores de salarios antigos que foram inclusos na referida tabela (caso possuam informações na mesma), além de todas informações relativas aos dependentes. 
>> ##### Observações: <br> a) perceba que este relatório pode conter linhas com alguns dados repetidos (mas não todos). <br>  b) para os empregados que não possuirem alguma destas informações o valor no registro deve aparecer sem informação/nulo. 
* Relatório que obtenha a frequencia absoluta e frequencia relativa da quantidade de cpfs únicos no relatório anterior. Apresente os resultados ordenados de forma decrescente pela frequencia relativa.

 
 
#### 4.3 TABELA DE DADOS DO SISTEMA:
[Tabela contendo exemplos de dados do sistema "Provisões de Emergência" (Arquivos .xlsx)](https://github.com/GodKelvin/Provisoes_de_emergencia/blob/master/arquivos/Exemplo_de_tabelas_Provisoes_de_Emergencia.xlsx "Tabela - Provisões de Emergência")
    
    
### 5.MODELO CONCEITUAL<br>    
![Alt text](https://github.com/GodKelvin/Provisoes_de_emergencia/blob/master/images/Conceitual_v3.png?raw=true "Modelo Conceitual")
    
    
        
    
#### 5.1 Validação do Modelo Conceitual
    [Grupo01]: [Nomes dos que participaram na avaliação]
    [Grupo02]: [Nomes dos que participaram na avaliação]

#### 5.2 Descrição dos dados 
    [objeto]: [descrição do objeto]
    
    EXEMPLO:
    CLIENTE: Tabela que armazena as informações relativas ao cliente<br>
    CPF: campo que armazena o número de Cadastro de Pessoa Física para cada cliente da empresa.<br>


### 6	MODELO LÓGICO<br>
![Alt text](https://github.com/GodKelvin/Provisoes_de_emergencia/blob/master/images/modelo_logico.png?raw=true "Modelo Conceitual")

### 7	MODELO FÍSICO<br>
```
create table GRUPO_FAMILIAR(
	cod_grupo_familiar SERIAL primary key not null,
	nome_grupo_familiar varchar(30) not null
);


create table PESSOA(
	cod_pessoa SERIAL primary key not null,
	fk_cod_grupo_familiar integer not null,
	nome_pessoa varchar(50) not null,
	cpf varchar(11) not null,
	data_nascimento date not null
);

create table PESSOA_CONSOME(
	cod_pessoa_consome SERIAL primary key not null,
	fk_cod_produto integer not null,
	fk_cod_pessoa integer not null,
	quantidade_produto float not null
);

create table FORNECEDOR(
	cod_fornecedor SERIAL primary key not null,
	nome_fornecedor varchar(30) not null
);

create table FORNECEDOR_PRODUTO(
	cod_fornecedor_produto SERIAL primary key not null,
	fk_cod_fornecedor integer not null,
	fk_cod_produto integer not null
);

create table PRODUTO(
	cod_produto SERIAL primary key not null,
	fk_cod_tipo_produto integer not null,
	preco_produto float not null,
	nome_produto varchar(40) not null
);

create table TIPO_PRODUTO(
	cod_tipo_produto SERIAL primary key not null,
	nome_tipo_produto varchar(30) not null
);

alter table PESSOA
add foreign key(fk_cod_grupo_familiar) references GRUPO_FAMILIAR(cod_grupo_familiar);

alter table PESSOA_CONSOME
add foreign key(fk_cod_produto) references PRODUTO(cod_produto),
add foreign key(fk_cod_pessoa) references PESSOA(cod_pessoa);

alter table FORNECEDOR_PRODUTO
add foreign key(fk_cod_fornecedor) references FORNECEDOR(cod_fornecedor),
add foreign key(fk_cod_produto) references PRODUTO(cod_produto);

alter table PRODUTO
add foreign key(fk_cod_tipo_produto) references TIPO_PRODUTO(cod_tipo_produto);
```
        
       
### 8	INSERT APLICADO NAS TABELAS DO BANCO DE DADOS<br>
[Script de exclusão, criação da estrutura e inserção dos dados (arquivo SQL)](https://github.com/GodKelvin/Provisoes_de_emergencia/blob/master/arquivos/Insert_aplicado_nas_tabelas_bd.sql)


### 9	TABELAS E PRINCIPAIS CONSULTAS<br>
    OBS: Incluir para cada tópico as instruções SQL + imagens (print da tela) mostrando os resultados.<br>
#### 9.1	CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas) <br>

># Marco de Entrega 01: Do item 1 até o item 9.1<br>

#### 9.2	CONSULTAS DAS TABELAS COM FILTROS WHERE (Mínimo 4)<br>
#### 9.3	CONSULTAS QUE USAM OPERADORES LÓGICOS, ARITMÉTICOS E TABELAS OU CAMPOS RENOMEADOS (Mínimo 11)
    a) Criar 5 consultas que envolvam os operadores lógicos AND, OR e Not
    b) Criar no mínimo 3 consultas com operadores aritméticos 
    c) Criar no mínimo 3 consultas com operação de renomear nomes de campos ou tabelas

#### 9.4	CONSULTAS QUE USAM OPERADORES LIKE E DATAS (Mínimo 12) <br>
    a) Criar outras 5 consultas que envolvam like ou ilike
    b) Criar uma consulta para cada tipo de função data apresentada.

#### 9.5	INSTRUÇÕES APLICANDO ATUALIZAÇÃO E EXCLUSÃO DE DADOS (Mínimo 6)<br>
    a) Criar minimo 3 de exclusão
    b) Criar minimo 3 de atualização

#### 9.6	CONSULTAS COM INNER JOIN E ORDER BY (Mínimo 6)<br>
    a) Uma junção que envolva todas as tabelas possuindo no mínimo 2 registros no resultado
    b) Outras junções que o grupo considere como sendo as de principal importância para o trabalho

#### 9.7	CONSULTAS COM GROUP BY E FUNÇÕES DE AGRUPAMENTO (Mínimo 6)<br>
    a) Criar minimo 2 envolvendo algum tipo de junção

#### 9.8	CONSULTAS COM LEFT, RIGHT E FULL JOIN (Mínimo 4)<br>
    a) Criar minimo 1 de cada tipo

#### 9.9	CONSULTAS COM SELF JOIN E VIEW (Mínimo 6)<br>
        a) Uma junção que envolva Self Join (caso não ocorra na base justificar e substituir por uma view)
        b) Outras junções com views que o grupo considere como sendo de relevante importância para o trabalho

#### 9.10	SUBCONSULTAS (Mínimo 4)<br>
     a) Criar minimo 1 envolvendo GROUP BY
     b) Criar minimo 1 envolvendo algum tipo de junção

># Marco de Entrega 02: Do item 9.2 até o ítem 9.10<br>

### 10 RELATÓRIOS E GRÁFICOS

#### a) análises e resultados provenientes do banco de dados desenvolvido (usar modelo disponível)
#### b) link com exemplo de relatórios será disponiblizado pelo professor no AVA
#### OBS: Esta é uma atividade de grande relevância no contexto do trabalho. Mantenha o foco nos 5 principais relatórios/resultados visando obter o melhor resultado possível.

    

### 11	AJUSTES DA DOCUMENTAÇÃO, CRIAÇÃO DOS SLIDES E VÍDEO PARA APRESENTAÇAO FINAL <br>

#### a) Modelo (pecha kucha)<br>
#### b) Tempo de apresentação 6:40 

># Marco de Entrega 03: Itens 10 e 11<br>
<br>
<br>
<br> 



### 12 FORMATACAO NO GIT:<br> 
https://help.github.com/articles/basic-writing-and-formatting-syntax/
<comentario no git>
    
##### About Formatting
    https://help.github.com/articles/about-writing-and-formatting-on-github/
    
##### Basic Formatting in Git
    
    https://help.github.com/articles/basic-writing-and-formatting-syntax/#referencing-issues-and-pull-requests
    
    
##### Working with advanced formatting
    https://help.github.com/articles/working-with-advanced-formatting/
#### Mastering Markdown
    https://guides.github.com/features/mastering-markdown/

    
### OBSERVAÇÕES IMPORTANTES

#### Todos os arquivos que fazem parte do projeto (Imagens, pdfs, arquivos fonte, etc..), devem estar presentes no GIT. Os arquivos do projeto vigente não devem ser armazenados em quaisquer outras plataformas.
1. <strong>Caso existam arquivos com conteúdos sigilosos<strong>, comunicar o professor que definirá em conjunto com o grupo a melhor forma de armazenamento do arquivo.

#### Todos os grupos deverão fazer Fork deste repositório e dar permissões administrativas ao usuário do git "profmoisesomena", para acompanhamento do trabalho.

#### Os usuários criados no GIT devem possuir o nome de identificação do aluno (não serão aceitos nomes como Eu123, meuprojeto, pro456, etc). Em caso de dúvida comunicar o professor.


Link para BrModelo:<br>
http://www.sis4.com/brModelo/download.html
<br>


Link para curso de GIT<br>
![https://www.youtube.com/curso_git](https://www.youtube.com/playlist?list=PLo7sFyCeiGUdIyEmHdfbuD2eR4XPDqnN2?raw=true "Title")


