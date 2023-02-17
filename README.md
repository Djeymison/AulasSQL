# AulasSQL
Todas as informações uteis a respeito de SQL

A linguagem SQL é dividida em 4 tipos de intruções de linguagem. DML(DATA MANIPULATION LANGUAGE), DDL(DATA DEFINITION LANGUAGE), DCL(DATA CONTROL LANGAGE) e TLC(TRANSATION CONTROL LANGUAGE).

COMANDOS DML: São utilizados para o gerenciamento de dados dentro de objetos do banco.
SELECT - Recupera dados do banco de dados.
INSERT - Inserir dados em uma tabela.
UPDATE - Atualiza dados existentes em uma tabela
DELETE - Exclui registros de uma tabela.

COMANDOS DDL: São usadas para definir a estrutura de banco de dados ou esquema.
CREATE - Para criar objetos no banco de dados, o proprio banco de dados, tabelas, indexes, procedures, views, functions e tiggers.
ALTER - Altera a estrutura de dados. O proprio banco de dados, tabelas, indexes, procedures, views, functions e tiggers.
DROP - Apaga o objeto no banco de dados. O proprio banco de dados, tabelas, indexes, procedures, views, functions e tiggers.
TRUNCATE - Remove todos os registros de uma tabela, incluindo todos os espaços alocados para registros são removidos.

COMANDOS DCL: São usados para definir acessos/controle de dados e objetos.
GRANT - Atribui privilégios de acesso do usuário a objetos do banco de dados. 
REVOKE - Remove os privilégios de acesso aos objetos obtidos com o comando GRANT
DENY - Nega a permissão a um usuário ou grupo para realizar a operação em um objeto ou recurso.

COMANDOS TLC: São usados para gerenciar as mudanças feitas por instruções DML. Ele permite que as declaraçõe a serem agrupadas em transações lógicas.
BEGIN TRANSACTION - Inicia uma transação.
COMMIT - Salva o trabalho feito.
SAVE TRANSACTION - Identifica um ponto em uma transação para que mais tarde você possa efetuar um ROLLBACK.
ROLLBACK - Restaura o banco de dados desde o último COMMIT.

?O que é uma subconsulta em SQL?
Uma subconsulta é uma consulta que está aninhada dentro de uma instrução SELECT , INSERT , UPDATE ou DELETE ou em outra subconsulta.


OBS: Boa parte das querys que serão criadas viram com os seguintes funções: FROM, WHERE, SELECT, INSERT, UPDATE ou DELETE. Para navegar entre as colunas será usado (0). Exemplo: (Azul, 84, ....)

DISTINCT: Apresenta resultados diferentes na planilha, eliminando objetos duplicados.



Alguns scripts para SQL: SELECT, FROM (Local), WHERE, AND, LIKE, GROUP BY, HAVING(Count).

Material de apoio. 

/* LINKS: Tipos de dados https://learn.microsoft.com/pt-br/sql/t-sql/data-types/data-types-transact-sql?view=sql-server-ver16

Operação de comparação https://learn.microsoft.com/pt-br/sql/t-sql/language-elements/comparison-operators-transact-sql?redirectedfrom=MSDN&view=sql-server-ver16

Operadores aritiméticos https://learn.microsoft.com/pt-br/sql/t-sql/language-elements/arithmetic-operators-transact-sql?redirectedfrom=MSDN&view=sql-server-ver16

Operadores Lógicos/Filtros https://learn.microsoft.com/pt-br/sql/t-sql/language-elements/logical-operators-transact-sql?redirectedfrom=MSDN&view=sql-server-ver16

DML https://learn.microsoft.com/pt-br/sql/t-sql/queries/queries?redirectedfrom=MSDN&view=sql-server-ver16

DDL https://learn.microsoft.com/pt-br/previous-versions/sql/sql-server-2012/ff848799(v=sql.110)?redirectedfrom=MSDN

TCL https://social.technet.microsoft.com/wiki/contents/articles/34477.sql-server-commands-dml-ddl-dcl-tcl.aspx#Transaction_Control_Language_TCL

SubConsultas https://learn.microsoft.com/pt-br/previous-versions/sql/sql-server-2008-r2/ms189575(v=sql.105)?redirectedfrom=MSDN

Funções de agregação https://learn.microsoft.com/pt-br/sql/t-sql/functions/aggregate-functions-transact-sql?redirectedfrom=MSDN&view=sql-server-ver16 https://learn.microsoft.com/pt-br/sql/t-sql/queries/select-group-by-transact-sql?view=sql-server-2017

Funções de classificação https://learn.microsoft.com/pt-br/sql/t-sql/functions/ranking-functions-transact-sql?redirectedfrom=MSDN&view=sql-server-ver16

Funções lógicas https://learn.microsoft.com/pt-br/previous-versions/sql/sql-server-2014/hh213226(v=sql.120)?redirectedfrom=MSDN

Funções Matemáticas https://learn.microsoft.com/pt-br/sql/t-sql/functions/mathematical-functions-transact-sql?redirectedfrom=MSDN&view=sql-server-ver16

Funções de Conversão https://learn.microsoft.com/pt-br/sql/t-sql/functions/conversion-functions-transact-sql?redirectedfrom=MSDN&view=sql-server-ver16

Funções de cadeia de caracteres https://learn.microsoft.com/pt-br/sql/t-sql/functions/string-functions-transact-sql?redirectedfrom=MSDN&view=sql-server-ver16

Expressão Case https://learn.microsoft.com/pt-br/sql/t-sql/language-elements/case-transact-sql?view=sql-server-ver16

Expessão NULLIF https://learn.microsoft.com/pt-br/sql/t-sql/language-elements/nullif-transact-sql?redirectedfrom=MSDN&view=sql-server-ver16 */


MATERIAL PARA CONSULTA:

-- LIMITE --

--TOP
--recuperando 3 registros da tabela
use NORTHWND
SELECT TOP 3 * FROM customers

SELECT TOP 10 a.CustomerID,a.CompanyName 
FROM customers a
 
--10 clientes com maior volume de pedido(compras)
use NORTHWND
select top 10
       rank() over(order by sum(c.Quantity*c.UnitPrice) desc)posicao,
	   a.CompanyName,
	   sum(c.Quantity*c.UnitPrice) Tot_compras
from Customers a
  inner join Orders b
  on a.CustomerID=b.CustomerID
  inner join [Order Details] c
  on b.OrderID=c.OrderID
  group by a.CompanyName
  --order by 3 desc

--recuperando 10 cidades mais populosas Brasil
use curso
select top 10 * from cidades
order by populacao desc

use curso
select top 10 *,rank() over(order by populacao desc) as posicao 
from cidades
order by populacao desc


-- DATA E HORA ADD -- 

--Adicionando 90 dias
	SELECT getdate() agora,
		   Dateadd (day, 90, Getdate()) 
--Adicionando 2 meses
	SELECT getdate() agora,
	       Dateadd (month, 2, Getdate()) 
--Adicionando 3 anos
	SELECT getdate() agora,
		   Dateadd (year, 3, Getdate())

--Exemplo
USE NORTHWND
	SELECT a.OrderID,
		   a.OrderDate,
		   Dateadd (day,90,a.OrderDate) add_dia,
		   Dateadd (month,2,a.OrderDate) add_mes,
		   Dateadd (YEAR,3,a.OrderDate) add_anos
    FROM Orders A 
    
    
    
-- FORMATANDO DATAS --

	Select convert(varchar(10),getdate(),103)

	Select convert(varchar(5),getdate(),103)

	Select convert(varchar(10),getdate(),108)

	Select convert(varchar(5),getdate(),108)

	SELECT CONVERT(VARCHAR(20),GETDATE(), 100)

	SELECT CONVERT(VARCHAR(8),GETDATE(), 1) 

--Extensão
SELECT CAST(DAY(GETDATE()) AS VARCHAR(2)) + ' ' +
       DATENAME(MM, GETDATE()) AS [Dia e Mes]

--EXEMPLO EM TABELA
USE NORTHWND
	SELECT a.OrderDate,
		   CONVERT(varchar(10),a.OrderDate,120)padrao120,
	       CONVERT(varchar(10),a.OrderDate,103)padrao103,
		   CONVERT(VARCHAR(20),a.OrderDate,100)padrao100,
		   CONVERT(VARCHAR(11),a.OrderDate,100)padrao100,
		   CONVERT(VARCHAR(8),a.OrderDate,1)  padrao1
		   FROM Orders a
       
       
	--FUNCAO DE DATA E HORA PARTES --
	--RETORNA O DIA/Mes/Ano

	SELECT Getdate()data_hora,
	       Datename (day, Getdate()) DIA_N,
		   Datename (month, Getdate()) MES_N,
		   Datename (year, Getdate()) ANO_N
	--RETORNA O DIA/Mes/Ano
	
	SELECT Datepart (day, Getdate()) DIA_P,
		   Datepart (month, Getdate())MES_P,
		   Datepart (year, Getdate()) ANO_P
	
	--RETORNA O DIA/Mes/Ano
	SELECT Day(Getdate()) DIA,
	       Month (Getdate()) MES,
		   YEAR (Getdate()) ANO
	
	--RETONAR DATA HORA COM 7 ARGUMENTOS
	SELECT DATETIMEFROMPARTS (2017,11,30,3,45,59,1) HORA

--
use NORTHWND

--exemplo 1
select a.OrderID,
       a.OrderDate,
       month(OrderDate)mes,
	   year(OrderDate)ano  
	   from Orders a

--exemplo 2
select year(a.OrderDate)ano ,
       month(a.OrderDate)mes,
	   count(*) qtd
	   from Orders a
group by year(a.OrderDate),month(a.OrderDate)
order by year(a.OrderDate),month(a.OrderDate)
	    

--exemplo 3
select year(a.OrderDate)ano ,
	   count(*) qtd
	   from Orders a
group by year(a.OrderDate)
order by year(a.OrderDate)

--FUNCOES DATA E HORA DO SISTEMA --

SELECT Sysdatetime () exSysdatetime
SELECT Sysdatetimeoffset () exSysdatetimeoffset
SELECT Sysutcdatetime () exSysutcdatetime
SELECT CURRENT_TIMESTAMP exCURRENT_TIMESTAMP
SELECT Getdate () exGetdate
SELECT Getutcdate () exGetutcdate


-- AGREGAÇÕES --

--conhecendo as tabelas
use curso
select top 1 * from cidades
select top 1 * from senso_2013
select * from uf
select * from regiao_uf


--AVG Retorna a média dos valores em um grupo. Valores nulos são ignorados
select AVG(populacao) from cidades

--AVG MEDIA POR ESTADO

SELECT UF,AVG(POPULACAO) FROM CIDADES
GROUP BY UF
ORDER BY 2

--AVG POR REGIAO

SELECT B.regiao,AVG(a.POPULACAO) 
	FROM CIDADES A
INNER JOIN regiao_uf B
ON A.cod_uf=B.ID
GROUP BY B.regiao
ORDER BY 2 desc


--MIN Retorna o valor mínimo na expressão. Pode ser seguido pela cláusula OVER
select MIN(populacao) from cidades

--MIN  POR ESTADO

SELECT UF,MIN(POPULACAO) 
	FROM CIDADES
GROUP BY UF
ORDER BY 2

--MIN POR REGIAO

SELECT B.regiao,MIN(POPULACAO) FROM CIDADES A
INNER JOIN regiao_uf B
ON A.cod_uf=B.ID
GROUP BY B.regiao
ORDER BY 2

--MAX Retorna o valor máximo na expressão
select MAX(populacao) from cidades

--MAX  POR ESTADO

SELECT UF,MAX(POPULACAO) FROM CIDADES
GROUP BY UF
ORDER BY 2

--MAX POR REGIAO

SELECT B.regiao,MAX(a.POPULACAO)maximo FROM CIDADES a
INNER JOIN regiao_uf B
ON A.cod_uf=B.ID
GROUP BY B.regiao
ORDER BY 2



--SUM Retorna a soma de todos os valores ou somente os valores DISTINCT na expressão. 
--SUM pode ser usado exclusivamente com colunas numéricas.Valores nulos são ignorados.

select SUM(populacao) from cidades
--183989711
--183989711
--183989711

--SUM  POR ESTADO

SELECT UF,SUM(POPULACAO) FROM CIDADES
GROUP BY UF
ORDER BY 2

--SUM POR REGIAO

SELECT B.regiao,SUM(a.POPULACAO) FROM CIDADES a
INNER JOIN regiao_uf B
ON A.cod_uf=B.ID
GROUP BY B.regiao
ORDER BY 2

--COUNT Retorna o número de itens de um grupo

select COUNT(*) from cidades

--Descobrindo qtd estados
select count(distinct uf) from cidades

--exemplo
select count(uf) from cidades


--COUNT  POR ESTADO

SELECT UF,COUNT(*) FROM CIDADES
GROUP BY UF
ORDER BY 2

--COUNT POR REGIAO

SELECT B.regiao,COUNT(*) FROM CIDADES a
INNER JOIN regiao_uf B
ON A.cod_uf=B.ID
GROUP BY B.regiao
ORDER BY 2

--usando varias funçoes de agregacao

select avg(populacao)media_pop,
	   min(populacao)minimo_pop,
	   max(populacao)maximo_pop,
	   sum(populacao)total_pop,
	   COUNT(*) qtd_cidades
from cidades

--POR ESTADO

SELECT UF,
	   avg(populacao)media_pop,
	   min(populacao)minimo_pop,
	   max(populacao)maximo_pop,
	   sum(populacao)total_pop,
	   COUNT(*) qtd_cidades
FROM CIDADES
GROUP BY UF
ORDER BY 2

--POR REGIAO

SELECT B.regiao,
	  avg(populacao)media_pop,
	   min(populacao)minimo_pop,
	   max(populacao)maximo_pop,
	   sum(populacao)total_pop,
	   COUNT(*) qtd_cidades
 FROM CIDADES a
INNER JOIN regiao_uf B
ON A.cod_uf=B.ID
GROUP BY B.regiao
ORDER BY 2

--STDEV Retorna o desvio padrão estatístico de todos os valores da expressão especificada

select STDEV(populacao)  from cidades

--STDEVP Retorna o desvio padrão estatístico para a população de todos os 
--valores na expressão especificada

select STDEVP(populacao)  from cidades

--GROUPING Indica se uma expressão de coluna especificada em uma lista 
--GROUP BY é agregada ou não. GROUPING retorna 1 para agregada ou 0 
--para não agregada no conjunto de resultados.

select uf,sum(populacao) as populacao,
GROUPING(uf) as grupo 
from cidades
group by uf with rollup

--COMPARANDO CRESCIMENTO DA CIDADES
SELECT TOP 1 *  FROM CIDADES
SELECT TOP 1 *  FROM senso_2013

--select cod_uf,cod_mun,cod_uf+cod_mun as concatenado from cidades
--usando exemplo
SELECT a.nome_mun,
       a.populacao as senso_2007,
	   b.populacao as senso_2013,
100/cast(a.populacao as float)*cast(b.populacao as float)-100 pct_cresc
from cidades a
inner join senso_2013 b
on a.cod_uf+a.cod_mun=b.cod_mun

--por estado
SELECT a.uf,
       sum(a.populacao) as senso_2007,
	   sum(b.populacao) as senso_2013,
100/cast(sum(a.populacao) as float)*cast(sum(b.populacao) as float)-100
from cidades a
inner join senso_2013 b
on a.cod_uf+a.cod_mun=b.cod_mun
group by a.uf



--GROUPING_ID
/*
É uma função que calcula o nível de agrupamento. 
GROUPING_ID pode ser usada apenas na lista SELECT <select>, 
na cláusula HAVING ou ORDER BY, quando GROUP BY for especificada.
*/
select b.regiao,a.uf,sum(a.populacao) populacao,
GROUPING_ID(b.regiao,a.uf) as grupo 
from cidades a
inner join regiao_uf b
on a.cod_uf=b.id
group by rollup(b.regiao,a.uf)



--VAR Retorna a variância estatística de todos os valores da expressão especificada
SELECT VAR(POPULACAO) FROM CIDADES

SELECT UF,VAR(POPULACAO) FROM CIDADES
GROUP BY UF


--VARP Retorna a variância estatística para o preenchimento 
--de todos os valores da expressão especificada.
SELECT VARP(POPULACAO) FROM CIDADES

SELECT UF,VARP(POPULACAO) FROM CIDADES
GROUP BY UF

SELECT UF,VAR(POPULACAO) var,VARP(POPULACAO)varp FROM CIDADES
GROUP BY UF



--exemplo com Grouping
use AdventureWorks2014
SELECT salesquota,        Sum(salesytd)        'TotalSalesYTD',        
Grouping(salesquota) AS 'Grouping' 
from sales.salesperson 
GROUP  BY salesquota WITH rollup;


-- CARACTERES --


--ASCII Exemplo
--
	select ASCII('SQL')
	select ASCII('S')
	select ASCII('Q')
	select ASCII('L')

/*O exemplo a seguir supõe um conjunto de caracteres ASCII e retorna o valor 
ASCII e o caractere CHAR para cada caractere na cadeia de 
caracteres da frase “Ola Mundo*/
	DECLARE @position INT,         
	@string   CHAR(5); 
	-- Initialize the variables. 
	SET @position = 1; 
	SET @string = 'TEste'; 
		WHILE @position <= Datalength(@string)   
			BEGIN       
				SELECT Ascii(Substring(@string, @position, 1))cod_ascii,              
				Char(Ascii(Substring(@string, @position, 1)))       
				SET @position = @position + 1   
			END;

--select Ascii(Substring('Ola Mundo', 1, 1))
			
--LTRIM
--Retorna uma expressão de caractere depois de remover espaços em branco à esquerda

	DECLARE @string_to_trim VARCHAR(60); 
	SET @string_to_trim ='     Cinco espaços no inicio.'; 
	SELECT  'Texto sem espaço:'+Ltrim(@string_to_trim); 
	SELECT  'Texto Com espaço:'+@string_to_trim; 

--STR

--Exemplo Retorna dados de caractere convertidos de dados numéricos.

SELECT  Str(123.45, 6, 1);
--Prova de conversao de numerico para caractere
SELECT 'Teste '+Str(123.45, 6, 1);


/*Quando a expressão excede o comprimento especificado, a cadeia de 
caracteres retorna ** para o comprimento especificado*/

SELECT Str(123.45, 2, 2); 

--CONCAT
/*Retorna uma cadeia de caracteres que é o resultado da concatenação de dois ou mais valores*/
 


SELECT  Concat(CURRENT_USER, 
               ' Seu Saldo é R$', 
			   11.00, 
			   ' em ',
               day(getdate()),'/',
			   month(getdate()),'/',
			   year(getdate())) AS Resultado

--Simulando erro com
SELECT CURRENT_USER+ 
               ' Seu Saldo é R$'+ 
			   11.00+
			   ' em '+
               day(getdate())+'/'+
			   month(getdate())+'/'+
			   year(getdate())AS Resultado	

--REPLACE
/*Substitui todas as ocorrências de um valor da cadeia de caracteres 
especificado por outro valor de cadeia de caracteres*/
--O exemplo a seguir substitui a cadeia de caracteres cde em abcdefghi por xxx.
	
	SELECT 'abcdefghicde' de,
		Replace('abcdefghicde', 'cde', 'xxx') para

--O exemplo a seguir substitui a cadeia de caracteres cde em teste por producao.
SELECT  'Isto é teste' de,
		Replace('Isto é teste', 'teste', 'producao')para;

--REPLACE NO SELECT
	use curso
	SELECT REGIAO,
		REPLACE(REGIAO,'Sul','South') 
		FROM regiao_uf

--Exemplo de Update usando replace.

CREATE TABLE pessoas   
	(nome VARCHAR(30) 
	) 
--inserindo registros
	INSERT INTO pessoas VALUES ('José') 
	INSERT INTO pessoas VALUES ('André') 
	INSERT INTO pessoas VALUES('Helem') 
--verificando registros

select * from pessoas
--
UPDATE pessoas SET nome=replace(nome, 'é', 'e')

--REPLICATE
--Repete um valor da cadeia de caracteres um número especificado de vezes
/*O exemplo a seguir replica um caractere 0 quatro vezes na frente de um código 
de linha de produção no banco de dados*/
     use AdventureWorks2014
	SELECT name,
	       productline,
		   Replicate('0', 4) + productline AS 'Line Code' 
	FROM   Production.product 
	WHERE  productline = 'T' 
	ORDER  BY name

/*Usando REPLICATE e DATALENGTH
O exemplo a seguir preenche números à esquerda até um comprimento especificado, 
à medida que são convertidos de um tipo de dados numérico em caractere ou Unicode.*/


use curso
--drop table t1
CREATE TABLE t1   
	(      c1 VARCHAR(3),      
			c2 CHAR(3)  
	 )

INSERT INTO t1 VALUES      ('2','2') 
INSERT INTO t1 VALUES      ('37','37') 
INSERT INTO t1 VALUES      ('597','597') 

--select * from t1

SELECT c1,
       c2,
	   Datalength(c1)dtlc1,
	   Datalength(c2)dtlc2,
	   Replicate('0', 3 - Datalength(c1)) + c1 AS 'Varchar Coluna',        
       Replicate('0', 3 - Datalength(c2)) + c2 AS 'Char Coluna' 
	   FROM   t1;

--LEFT
--Retorna a parte da esquerda de uma cadeia de caracteres com o número de caracteres especificado.

	use AdventureWorks2014
	SELECT  NAME,
			LEFT(NAME, 5) 
	FROM   production.product 
	ORDER  BY productid;

--UPPER
--Retorna uma expressão de caractere com dados de caractere em minúsculas convertidos em maiúsculas
	use curso
	SELECT estado, 
		   upper(estado) 
	from regiao_uf

--SUBSTRING
--Retorna uma substring de caractere com dados de caractere dento do parâmetro informado
use AdventureWorks2014
	SELECT lastname nome,        
		   Substring(lastname, 1, 3)  lastname1,        
		   Substring(lastname, 4, 10) lastname2 
	FROM   person.person 
	ORDER  BY lastname; 

--REVERSE
--Retorna a ordem inversa de um valor da cadeia de caracteres.

	SELECT firstname,        
		   Reverse(firstname) AS Reverse 
		   FROM   person.person 
   WHERE  businessentityid < 5 
   ORDER  BY firstname

--LEN
--Retorna o número de caracteres da expressão da cadeia de caracteres especificada, 
--excluindo espaços em branco à direita
	SELECT  firstname,
			Len(firstname) AS Tamanho        	             
   FROM   sales.vindividualcustomer 
   WHERE  countryregionname = 'Australia'; 
   
--DATALENGTH
--Retorna o número de bytes usado para representar qualquer expressão
	SELECT  NAME,
			Datalength(NAME)as data       	    
	FROM   production.product 
	ORDER  BY NAME;

--Comparando Datalength com Len
SELECT  NAME,
		Datalength(NAME)as Datalength,
       Len(NAME)as len		    
	FROM   production.product 
	ORDER  BY NAME

--RIGHT
--Retorna a parte da direita de uma cadeia de caracteres com o número de caracteres especificado
use curso
	SELECT a.estado,
		   RIGHT(estado, 5) AS 'Estado' 
	FROM   regiao_uf a
	
--LOWER
--Retorna uma expressão de caractere depois de converter 
--para minúsculas os dados de caracteres em maiúsculas
--O exemplo a seguir usa a função LOWER, a função UPPER, 
--e aninha a função UPPER dentro da função LOWER selecionando 
--nomes de produtos com preços entre US$ 11 e US$ 20. 
--Este exemplo usa o banco de dados AdventureWorks2014

use AdventureWorks2014
	SELECT Substring(NAME, 1, 20)name,
		   Lower(Substring(NAME, 1, 20)) AS Lower,        
		   Upper(Substring(NAME, 1, 20)) AS Upper,        
		   Lower(Upper(Substring(NAME, 1, 20))) AS LowerUpper 
   FROM   production.product 
   WHERE  listprice BETWEEN 11.00 AND 20.00; 

--RTRIM
--Retorna uma cadeia de caracteres depois de truncar todos os espaços em branco à direita
--EXEMPLO SIMPLES
SELECT Rtrim('Removendo espaços.   ');

--EXEMPLO 2
	DECLARE @string_to_trim VARCHAR(60); 
	SET @string_to_trim ='Deixamos 4 espacos apos final da sentença.    '; 
	SELECT @string_to_trim + ' proxima string.'; 
	SELECT Rtrim(@string_to_trim) + ' proxima string.'


-- CLASSIFICAÇÃO --

Função usada para classificar os objetos na planilha.

--RANK EXEMPLO 2 1
/*As funções de classificação retornam um valor de classificação 
para cada linha em uma partição. Dependendo da função usada, 
algumas linhas podem receber o mesmo valor que outras. 
As funções de classificação são não determinísticas
*/
select rank() OVER (ORDER BY estado ASC) AS rank_uf ,
       estado 
from uf

--RANK EXEMPLO 2
select rank() OVER (ORDER BY estado ASC) AS rank_uf ,
	   regiao,
	   estado  
from regiao_uf

--RANK EXEMPLO 3
select rank() OVER (ORDER BY regiao ASC) AS rank_uf ,
       regiao,
	   estado
from regiao_uf

--NTILE
/*Distribui as linhas de uma partição ordenada em um número de grupos especificado. 
Os grupos são numerados, iniciando em um. Para cada linha, 
NTILE retorna o número do grupo ao qual a linha pertence.
*/
select NTILE(3) OVER (ORDER BY regiao ASC) AS NTILE_uf ,
regiao,estado
regiao_uf 
from regiao_uf

--DENSE_RANK
/*Retorna a classificação de linhas dentro da partição de um conjunto de resultados, 
sem qualquer lacuna na classificação. A classificação de uma linha é um mais 
o número de classificações distintas que vêm antes da linha em questão.
*/
select DENSE_RANK() OVER (ORDER BY regiao ASC) AS DENSE_RANK_uf ,
	  regiao,
	  estado
from regiao_uf

select DENSE_RANK() OVER (ORDER BY estado ASC) AS DENSE_RANK_uf ,
regiao,estado
regiao_uf 
from regiao_uf

--ROW_NUMBER
/*Retorna o número sequencial de uma linha em uma partição de um conjunto de resultados, 
iniciando em 1 para a primeira linha de cada partição.
*/
select ROW_NUMBER() OVER (ORDER BY estado ASC) AS ROW_NUMBER_uf ,
	  regiao,
	  estado
from regiao_uf

--combinando valores 1
select ROW_NUMBER() OVER (ORDER BY regiao ASC) AS ROW_NUMBER_uf ,
       DENSE_RANK() OVER (ORDER BY regiao ASC) AS DENSE_RANK_uf ,
	   NTILE(6) OVER (ORDER BY regiao ASC) AS NTILE_uf ,
	   rank() OVER (ORDER BY regiao ASC) AS rank_uf ,
       regiao,
	   estado
regiao_uf 
from regiao_uf
order by 5,6

--combinando valores 1
select ROW_NUMBER() OVER (ORDER BY estado ASC) AS ROW_NUMBER_uf ,
       DENSE_RANK() OVER (ORDER BY estado ASC) AS DENSE_RANK_uf ,
	   NTILE(5) OVER (ORDER BY estado ASC) AS NTILE_uf ,
	   rank() OVER (ORDER BY estado ASC) AS rank_uf ,
regiao,estado
regiao_uf 
from regiao_uf
order by 4,6

--simulando classificacao de campeonato
--drop table campeonato
create table campeonato
(
 nometime varchar(30)not null,
 pontos int not null
 )
 --populando tabela
insert into campeonato values ('Corinthians','53');
insert into campeonato values ('Grêmio','43');
insert into campeonato values ('Santos','41');
insert into campeonato values ('Palmeiras','40');
insert into campeonato values ('Flamengo','38');
insert into campeonato values ('Cruzeiro','37');
insert into campeonato values ('Botafogo','37');
insert into campeonato values ('Atlético-PR','34');
insert into campeonato values ('Vasco','31');
insert into campeonato values ('Atlético-MG','31');
insert into campeonato values ('Fluminense','31');
insert into campeonato values ('Sport','29');
insert into campeonato values ('Avaí','29');
insert into campeonato values ('Chapecoense','28');
insert into campeonato values ('Ponte Preta','28');
insert into campeonato values ('Bahia','27');
insert into campeonato values ('São Paulo','27');
insert into campeonato values ('Coritiba','27');
insert into campeonato values ('Vitória','26');
insert into campeonato values ('Atlético-GO','22');

--select * from campeonato

--Classificacao do campeonato
	select rank() OVER (ORDER BY pontos desc) AS classif ,
		    nometime,
			pontos 
	from campeonato

-- CONVERSSÃO -- 

FALTA ENCONTRAR

-- LOGICAS --

--CHOOSE
--Retorna o item ao índice especificado de uma lista de valores no SQL Server.
--Exemplo 1
SELECT Choose (3, 'Gerente', 'Diretor', 'Desenvolvedor', 'Tester') AS Escolhido 

--Exemplo 2
Use AdventureWorks2014
 SELECT productcategoryid,     
Choose (productcategoryid, 'A', 'B', 'C', 'D', 'E') AS Expressao 
FROM   production.productcategory; 

--exemplo 3

 SELECT jobtitle,        
        hiredate,
		Month(hiredate)mes,        
		Choose(Month(hiredate), 'Winter', 'Winter', 'Spring', 'Spring', 
		                        'Spring','Summer', 'Summer','Summer', 
								'Autumn', 'Autumn', 'Autumn','Winter') AS Quarter_Hired 
		FROM   humanresources.employee 
		WHERE  Year(hiredate) > 2005 
		ORDER  BY Year(hiredate);


--IIF
--Retorna um de dois valores, dependendo de a expressão booliana 
--ser avaliada como true ou false no SQL Server 
--Exemplo 1
 DECLARE @a INT = 45,          
		 @b INT = 40;   
		 SELECT IIF (@a > @b, 'TRUE', 'FALSE') AS Resultado;

DECLARE @a INT = 45,          
		 @b INT = 40;   
		 SELECT IIF (@a > @b, 'Maior', 'Menor') AS Resultado;

DECLARE @a INT = 45,          
		 @b INT = 40;   
		 SELECT IIF (@a < @b, 'Menor', 'Maior') AS Resultado;


--EXEMPLO 2
--IIF com constantes NULL
--O resultado dessa instrução é um erro
SELECT IIF (45 > 30, NULL, NULL) AS Result;

--EXEMPLO 3
/*IIF com parâmetros NULL
O retorno NULL.*/
	DECLARE @P INT = NULL,         
			@S INT = NULL; 
	SELECT  IIF (45 > 30, @p, @s) AS Result
  
  
 -- FUNÇÕES MATEMÁTICAS --
 
 --ABS
--Uma função matemática que retorna o valor absoluto (positivo) 
--da expressão numérica especificada.

SELECT Abs(-1.0),        
       Abs(0.0),        
	   Abs(1.0),
	   Abs(-9.0),
	   Abs(9.0),
	   abs(-5.4),
	   abs(5.4);

--RAND
--Retorna um valor float pseudoaleatório de 0 a 1, exclusivo.


SELECT Rand(), 
       Rand(), 
	   Rand()

--exenplo

DECLARE @cont smallint;
SET @cont = 1;
WHILE @cont < 5
   BEGIN
      SELECT RAND() Random_Number
      SET @cont = @cont + 1
   END;

--ROUND
--Retorna um valor numérico, arredondado, para o comprimento ou precisão especificados.

SELECT Round(123.9994, 3), --0,1,2,3,4<    
       Round(123.9995, 3); --5,6,7,8,9 >
--exemplo 2

SELECT Round(123.4545, 2); 
SELECT Round(123.45,-2);
SELECT Round(193.45,-2);

--exemplo 3
SELECT Round(150.75, 0);
SELECT Round(150.75, 0, 1); 


-- JOIN --

use curso
--drop table alunos
--CRIACAO DE TABELA ALUNOS
create table alunos
(id_aluno int identity(1,1),
 nome varchar(20) not null
 )
 --drop table disciplina
create table disciplina
(
 id_disciplina int identity(1,1),
 nome_disc varchar(20)
 )
 --drop table matricula
 create table matricula
 (id_aluno int,
  id_disciplina int,
  periodo varchar(10)
  )

  --ALTERANDO TABELA CAMPO ID_ALUNO PARA NAO PERMITIR NOT NULL
  ALTER TABLE MATRICULA ALTER COLUMN id_aluno INT NOT NULL
  --ALTERANDO TABELA 
  ALTER TABLE MATRICULA ALTER COLUMN id_disciplina INT NOT NULL

  --CRIANDO CHAVE PRIMARIA COMPOSTA
  ALTER TABLE MATRICULA ADD CONSTRAINT PK_1 PRIMARY KEY (ID_ALUNO,id_disciplina)
 --ADICIONANDO CHAVE PRIMARIA TABELA DISCIPLINA
  ALTER TABLE DISCIPLINA ADD CONSTRAINT PK2 PRIMARY KEY (id_disciplina)
  --ADICIONANDO CHAVE PRIMARIA TABELA ALUNOS
  ALTER TABLE ALUNOS ADD CONSTRAINT PK1 PRIMARY KEY (ID_ALUNO)
  
  --ADICIONANDO CHAVE ESTRANGEIRA NA TABELA MATRICULA CAMPO ID_ALUNO
  ALTER TABLE MATRICULA 
  ADD CONSTRAINT FK_MAT1 FOREIGN KEY  (ID_ALUNO) REFERENCES ALUNOS(ID_ALUNO)

  --ADICIONANDO CHAVE ESTRANGEIRA NA TABELA MATRICULA CAMPO ID_ALUNO
  ALTER TABLE MATRICULA 
  ADD CONSTRAINT FK_MAT2 FOREIGN KEY  (id_disciplina) REFERENCES DISCIPLINA(id_disciplina)


  

  
  --INSERINDO REGISTRO ALUNOS
  insert into alunos values ('Joao'),('Maria'),('Pedro'),('Tiago'),('Henrique')

  SELECT * FROM alunos

  --INSERINDO REGISTRO DISCIPLINAS
  insert into disciplina values 
  ('Fisica'),('Quimica'),('Matematica'),('Banco de Dados'),('Programacao')

  SELECT * FROM disciplina

  --INSERINDO MATRICULAS DE ALUNOS
  insert into matricula values ('1','1','Noturno')
  insert into matricula values ('1','2','Vespertino')
  insert into matricula values ('1','3','Matutino')

  insert into matricula values ('2','3','Noturno')
  insert into matricula values ('2','4','Noturno')

  insert into matricula values ('3','1','Noturno')
  insert into matricula values ('3','3','Noturno')
  insert into matricula values ('3','4','Noturno')

  insert into matricula values ('5','1','Matutino')
  insert into matricula values ('5','2','Vespertino')
  insert into matricula values ('5','4','Noturno')


  --ALUNO CODIG 4 NAO TEM MATRICULA
  --DISCIPLINA 5 NAO TEM ALUNOS

  --INNER JOIN

  select a.nome,c.nome_disc,b.periodo
  from alunos a
  inner join matricula b 
  on a.id_aluno=b.id_aluno
  inner join disciplina c
  on b.id_disciplina=c.id_disciplina

  --LEFT JOIN

  select a.nome,c.nome_disc,b.periodo
  from alunos a
  left join matricula b 
  on a.id_aluno=b.id_aluno
  left join disciplina c
  on b.id_disciplina=c.id_disciplina
  

 --RIGHT JOIN
  select a.nome,c.nome_disc,b.periodo
  from alunos a
  right join matricula b 
  on a.id_aluno=b.id_aluno
  right join disciplina c
  on b.id_disciplina=c.id_disciplina

  --FULL JOIN
  select a.nome,c.nome_disc,b.periodo
  from alunos a
  full join matricula b 
  on a.id_aluno=b.id_aluno
  full join disciplina c
  on b.id_disciplina=c.id_disciplina

--INNER JOIN

SELECT orders.orderid, 
       customers.CompanyName 
FROM   orders 
       INNER JOIN customers 
       ON orders.customerid = customers.customerid; 

--INNER JOIN
SELECT orders.orderid, 
       customers.CompanyName, 
       shippers.CompanyName 
FROM   orders 
         INNER JOIN customers 
                 ON orders.customerid = customers.customerid 
        INNER JOIN shippers 
                ON orders.shipvia = shippers.shipperid; 


--LEFT JOIN
SELECT customers.CompanyName, 
       orders.orderid 
FROM   customers 
       LEFT JOIN orders 
              ON customers.customerid = orders.customerid 
ORDER  BY customers.CompanyName; 

--Rigth Join
SELECT orders.orderid, 
       employees.lastname, 
       employees.firstname 
FROM   orders 
       RIGHT JOIN employees 
               ON orders.employeeid = employees.employeeid 
ORDER  BY orders.orderid; 

--FULL JOIN
SELECT customers.CompanyName, 
       orders.orderid 
FROM   customers 
       FULL OUTER JOIN orders 
                    ON customers.customerid = orders.customerid 
ORDER  BY customers.CompanyName; 

-- NULL --

--criando o problema 
SELECT 100 / 0 

--Tratando 
SELECT Isnull(100 / NULLIF(0, 0), 0) 
SELECT Isnull(1 / NULLIF(0, 0), 0) 
SELECT Isnull(100 / NULLIF(50, 0), 0)

use curso
create table teste2
(
  val1 int,
  val2 int
)
--Populando tabela teste2
insert into teste2 values (100,0),(100,25),(1,0),(5,2)

--verificando dados
select * from teste2
--Expressao com erro
select val1,val2,val1/val2 expressao
from teste2

--Expressao tratando erros
select 
		val1,
		val2,
		isnull(val1/nullif(val2,0),0) expressao,
		isnull(cast(val1 as decimal(5,2))/cast(nullif(val2,0) as decimal(5,2)),0) expressao
from teste2


--Comparando Case Nullif
--Retorna um valor nulo se as duas expressões especificadas forem iguais.

use AdventureWorks2014
	SELECT productid,        
		   makeflag,        
		   finishedgoodsflag,        
		   NULLIF(makeflag, finishedgoodsflag)AS 'Null se igual' 
		   FROM   production.product 
		   WHERE  productid < 10; 
		   go 
   
   SELECT productid,        
          makeflag,        
		  finishedgoodsflag,        
		  CASE                            
		  WHEN makeflag = finishedgoodsflag THEN NULL 
		   ELSE makeflag  end 'Null se igual'                        
		  FROM   production.product 
		  WHERE  productid < 10; 

--COMPARAÇÃO--

--Usando operador = 
	SELECT * FROM   cidades 
	WHERE  uf ='SP'

--Outro exemplo operador =
	SELECT * FROM   cidades 
	WHERE nome_mun = 'Dourado'      
	AND uf = 'SP' 

--Usando operador > 
	SELECT * FROM   cidades 
	WHERE  populacao > 100000 

--Usando operador > 
	SELECT * FROM   cidades 
	WHERE  populacao > 1000000

--Usando operador < 
	SELECT * FROM   cidades 
	WHERE  populacao < 10000 
--Usando operador < 
	SELECT * FROM   cidades 
	WHERE  populacao < 50000

--Usando operador <= 
	SELECT * FROM   cidades 
	WHERE  populacao <= 10000 
--Usando operador <= 
	SELECT * FROM   cidades 
	WHERE  populacao <= 50000

--Usando operador <> 
	SELECT * FROM   cidades 
	WHERE  uf <> 'SP'        
	AND uf <> 'SC'

--Combinando operadores 
	SELECT * FROM   cidades 
	WHERE  populacao <= 100000        
		AND populacao >= 50000        
		AND uf = 'SP'        
		AND nome_mun <> 'Vinhedo'

--UNION--
USE NORTHWND
--SIMULANDO ERRO UNION

SELECT '1',1
UNION 
SELECT 'A',2

--EXEMPLO USANDO UNION
	
	SELECT city 
	FROM   customers 

	UNION 

	SELECT city 
	FROM   suppliers 
	ORDER  BY city
----EXEMPLO USANDO UNION ALL

	SELECT 'CLI',city 
	FROM   customers 

	UNION ALL

	SELECT 'FORNEC', city 
	FROM   suppliers 
	ORDER  BY city

--EXEMPLO COM UNION
	SELECT city,        
		   country 
	FROM   customers 
		WHERE  country = 'Germany' 
		
	UNION
	 
	SELECT city,        
		   country 
	FROM   suppliers 
		WHERE  country = 'Germany' 
	ORDER  BY city

--EXEMPLO COM UNION ALL
	SELECT city,        
		   country 
	FROM   customers 
		WHERE  country = 'Germany' 
		
	UNION ALL
	 
	SELECT city,        
		   country 
	FROM   suppliers 
		WHERE  country = 'Germany' 
	ORDER  BY city
  
-- OPERADORES ARITIMETRICOS --

--Operador + 
SELECT 1 + 3 

--Operador * 
SELECT 3 * 2

--Operador - 
SELECT 5 - 2
 
--Operador / 
SELECT 15 / 3
 

--Operador % 
SELECT 12%5

--
select ((1+4)*(3*3))/5

/*
Usando o operador de adição para calcular o número total de 
horas de ausência do trabalho para cada funcionário.
*/
use AdventureWorks2014

SELECT  p.firstname,             
		p.lastname,             
		e.vacationhours,             
		e.sickleavehours,             
		e.vacationhours + e.sickleavehours AS 'Horas Ausente' 
FROM   humanresources.employee AS e        
	JOIN person.person AS p          
	ON e.businessentityid = p.businessentityid 
	ORDER  BY 'Horas Ausente' ASC; 




--Usando subtração em uma instrução SELECT
SELECT Max(taxrate) maximo,Min(taxrate) minimo,
	   Max(taxrate) - Min(taxrate) AS 'Tax Rate Difference' 
FROM   sales.salestaxrate 
WHERE  stateprovinceid IS NOT NULL; 

/*
O exemplo a seguir recupera o número de identificação do produto, 
o nome, o preço de tabela e o novo preço de tabela de 
todas as bicicletas mountain bike na tabela Product. 
O novo preço de tabela é calculado usando o operador aritmético * 
para multiplicar ListPrice por 1.15.
*/

	SELECT  productid,        
			NAME,        
			listprice,        
			listprice * 1.15 AS Novo_preco 
			FROM   production.product 
				WHERE  NAME LIKE 'Mountain-%' 
	ORDER  BY productid ASC; 


/*
O exemplo a seguir usa o operador aritmético de divisão para 
calcular a meta de vendas mensal da equipe de vendas em Ciclos de 12 meses
*/

	SELECT  s.businessentityid AS SalesPersonID,        
			firstname,        
			lastname,        
			salesquota,        
			salesquota / 12    AS 'Meta Mensal' 
			FROM   sales.salesperson AS s        
				JOIN humanresources.employee AS e          
				ON s.businessentityid = e.businessentityid        
				JOIN person.person AS p          
				ON e.businessentityid = p.businessentityid;


/*
O exemplo a seguir divide o número 38 por 5. 
Isto resulta em 7 como a parte inteira do resultado 
e demonstra como o módulo retorna o resto de 3.
*/

	SELECT 38 / 5 AS Inteiro,        
	       38 % 5 AS Restante
         
         
         
--OPERADORES LOGICOS --

--Operador + 
SELECT 1 + 3 

--Operador * 
SELECT 3 * 2

--Operador - 
SELECT 5 - 2
 
--Operador / 
SELECT 15 / 3
 

--Operador % 
SELECT 12%5

--
select ((1+4)*(3*3))/5

/*
Usando o operador de adição para calcular o número total de 
horas de ausência do trabalho para cada funcionário.
*/
use AdventureWorks2014

SELECT  p.firstname,             
		p.lastname,             
		e.vacationhours,             
		e.sickleavehours,             
		e.vacationhours + e.sickleavehours AS 'Horas Ausente' 
FROM   humanresources.employee AS e        
	JOIN person.person AS p          
	ON e.businessentityid = p.businessentityid 
	ORDER  BY 'Horas Ausente' ASC; 




--Usando subtração em uma instrução SELECT
SELECT Max(taxrate) maximo,Min(taxrate) minimo,
	   Max(taxrate) - Min(taxrate) AS 'Tax Rate Difference' 
FROM   sales.salestaxrate 
WHERE  stateprovinceid IS NOT NULL; 

/*
O exemplo a seguir recupera o número de identificação do produto, 
o nome, o preço de tabela e o novo preço de tabela de 
todas as bicicletas mountain bike na tabela Product. 
O novo preço de tabela é calculado usando o operador aritmético * 
para multiplicar ListPrice por 1.15.
*/

	SELECT  productid,        
			NAME,        
			listprice,        
			listprice * 1.15 AS Novo_preco 
			FROM   production.product 
				WHERE  NAME LIKE 'Mountain-%' 
	ORDER  BY productid ASC; 


/*
O exemplo a seguir usa o operador aritmético de divisão para 
calcular a meta de vendas mensal da equipe de vendas em Ciclos de 12 meses
*/

	SELECT  s.businessentityid AS SalesPersonID,        
			firstname,        
			lastname,        
			salesquota,        
			salesquota / 12    AS 'Meta Mensal' 
			FROM   sales.salesperson AS s        
				JOIN humanresources.employee AS e          
				ON s.businessentityid = e.businessentityid        
				JOIN person.person AS p          
				ON e.businessentityid = p.businessentityid;


/*
O exemplo a seguir divide o número 38 por 5. 
Isto resulta em 7 como a parte inteira do resultado 
e demonstra como o módulo retorna o resto de 3.
*/

	SELECT 38 / 5 AS Inteiro,        
	       38 % 5 AS Restante


--SUB QUERYS--

--criando ta tabelas cliente

use curso
create table  clientes
(cod_cli nchar(5) primary key,
 cli_nome nvarchar(40) not null
 ) 

--inserindo dados da tabelas cliente apartir da tabela customers do db Northwnd
insert into clientes 
select customerid,companyname from NORTHWND.dbo.Customers

--criando tabelas pedidos

 create table pedidos
	(
	 num_ped int primary key,
	 cod_cliente nchar(5)not null,
     data datetime not null,
	 total decimal(10,2)
	 )

--inserindo dados na tabela pedido com dados da tabela orders do bd Northwnd
insert into pedidos (num_ped,cod_cliente,data)
select OrderID,customerid,OrderDate from NORTHWND.dbo.Orders 

--atualizando campo total da tabela pedido com update em subselect

select * from pedidos

  update pedidos set total=(select sum(b.unitprice*b.quantity) 
  from NORTHWND.dbo.[Order Details] b
  where num_ped=b.orderid)



--Aqui somente apresentamos os clientes que fizeram compras antes da data atual 
SELECT cod_cli , 
       cli_nome 
FROM   clientes 
WHERE  cod_cli NOT IN (SELECT cod_cliente
              FROM   pedidos 
              WHERE  data < Getdate() )

--Aqui apresentamos todos os clientes  que cliente já fizeram algum pedido.
--trocando "in" por "Not in" apresenta o cliente que nao fizeram pedidos

SELECT cli_cod, 
       cli_nome 
FROM   cliente 
WHERE  cli_cod IN(SELECT cli_cod 
                  FROM   pedidos) 



/*
Nesta query estamos retornando o campo NOM_CLI da tabela CLIENTES.
Porém, não estamos filtrando a tabela PEDIDO de modo que se houver 
algum COD_CLI na tabela PEDIDOS que não se encontre na tabela CLIENTE o 
valor NULL será retornado para o campo
NOME_CLI calculado através da subquery

*/
  SELECT P.num_ped, 
       P.data, 
       P.cod_cliente, 
       (SELECT C.cli_nome 
        FROM   clientes C 
        WHERE  P.cod_cliente = C.cod_cli) AS NOME_CLI 
FROM   pedidos AS P 

/*
Nesta Query com Subquery vamos trazer  o total de cada cliente partindo da tabela pedidos 
*/
SELECT P.cod_cliente, 
       (SELECT C.cli_nome 
        FROM   clientes C 
        WHERE  P.cod_cliente = C.cod_cli) AS NOME_CLI, 
       Sum(p.total) total 
FROM   pedidos AS P 
GROUP  BY P.cod_cliente 

/*
Nesta Query vamos trazer todos clientes e através de subconsulta o valor de suas compras.
*/

SELECT c.cod_cli, 
      (SELECT isnull(Sum(p.total),0)
        FROM   pedidos p
        WHERE  c.cod_cli = p.cod_cliente) AS total 
FROM   clientes c 
GROUP  BY c.cod_cli 

--eliminando clientes da tabela cliente que nao fizeram pedidos
delete from clientes
where cod_cli not in (select cod_cliente from pedidos)

--TCL 1--
--criando de teste
create table cadastro
(
 nome varchar(50) not null,
 docto varchar(20) not null
 )

--INICIA TRANSAÇÃO
BEGIN TRANSACTION 

--INSERE REGISTROS
INSERT INTO cadastro VALUES      ('Andre', '12341244') 
INSERT INTO cadastro VALUES      ('Joao',  '12341248') 
INSERT INTO cadastro VALUES      ('Pedro', '12341246') 

--SELECT DOS REGISTRO INSERIDOS
SELECT * FROM   cadastro 

--RETORNA O TABELA NAO ESTADO ANTERIOR DO BEGIN TRANSACTION
ROLLBACK 

--EFETIVA AS INFORMACOES NA TABELAS DO BANCO DE DADOS
COMMIT TRANSACTION


--TCL 2--

--limpando a tabela
delete from cadastro
--INICIA TRANSACAO

BEGIN TRANSACTION 
--INSERE REGISTRO
INSERT INTO cadastro  VALUES ('Andre', '12341244') 
--CRIA UM PONTO DE RECUPERACAO
SAVE TRANSACTION a1 
--INSERE REGISTRO
INSERT INTO cadastro  VALUES ('Joao','12341244') 
--CRIA UM PONTO DE RECUPERACAO
SAVE TRANSACTION a2 
--INSERE REGISTRO
INSERT INTO cadastro VALUES ('Pedro', '12341244') 
--CRIA UM PONTO DE RECUPERACAO
SAVE TRANSACTION a3 

--VERIFICA REGISTROS
SELECT * FROM   cadastro

--RESTAURA A TABELA ATE O PONTO A2 
ROLLBACK TRANSACTION a2 

--VERIFICA REGISTROS
SELECT * FROM   cadastro

--RETORNA A TABELA NO ESTADO ANTERIOR AO BEGIN TRANSACTION
ROLLBACK 

--EFETIVA AS INFORMAÇOES NA TABELA
COMMIT TRANSACTION


