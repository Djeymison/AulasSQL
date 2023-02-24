# AulasSQL
Todas as informações uteis a respeito de SQL

OBS1: Sobre SGBDs: Um Sistema de Gerenciamento de Banco de Dados (SGBD) – do inglês Data Base Management System (DBMS) – é o conjunto de programas de computador (softwares) responsáveis pelo gerenciamento de uma base de dados. Seu principal objetivo é retirar da aplicação cliente a responsabilidade de gerenciar o acesso, a manipulação e a organização dos dados. O SGBD disponibiliza uma interface para que seus clientes possam incluir, alterar ou consultar dados previamente armazenados. Em bancos de dados relacionais a interface é constituída pelas APIs (Application Programming Interface) ou drivers do SGBD, que executam comandos na linguagem SQL (Structured Query Language)

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

Material informativo conta GIT: https://github.com/brunocampos01/banco-de-dados


