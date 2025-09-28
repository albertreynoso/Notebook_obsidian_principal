Recursos:
Práctica:
https://www.sql-practice.com/
Teoría:
https://www.geeksforgeeks.org/sql/sql-select-database/


## COMANDOS SQL ESTRUCTURA
![[Pasted image 20250924121402.png]]
1. DDL - Data Definition Language: consiste en comandos SQL que permiten definir, modificar y eliminar estructuras de bases de datos como tablas, índices y esquemas.

| Command                                                               | Description                                                                                  | Syntax                                                               |
| --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| [CREATE](https://www.geeksforgeeks.org/sql/sql-create-table/)         | Create database or its objects (table, index, function, views, store procedure and triggers) | CREATE TABLE table_name (column1 data_type, column2 data_type, ...); |
| [DROP](https://www.geeksforgeeks.org/sql/sql-drop-truncate/)          | Delete objects from the database                                                             | DROP TABLE table_name;                                               |
| [ALTER](https://www.geeksforgeeks.org/sql/sql-alter-add-drop-modify/) | Alter the structure of the database                                                          | ALTER TABLE table_name ADD COLUMN column_name data_type;             |
| [TRUNCATE](https://www.geeksforgeeks.org/sql/sql-drop-truncate/)      | Remove all records from a table, including all spaces allocated for the records are removed  | TRUNCATE TABLE table_name;                                           |
| [COMMENT](https://www.geeksforgeeks.org/sql/sql-comments/)            | Add comments to the data dictionary                                                          | COMMENT ON TABLE table_name IS 'comment_text';                       |
| [RENAME](https://www.geeksforgeeks.org/sql/sql-rename-table/)         | Rename an object existing in the database                                                    | RENAME TABLE old_table_name TO new_table_name;                       |
2. DQL - Data Query Language: se utiliza para obtener datos de la base de datos. El comando principal es SELECT, que recupera registros según la consulta.

| Command                                                                      | Description                                                              | Syntax                                                                                                  |
| ---------------------------------------------------------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| [SELECT](https://www.geeksforgeeks.org/sql/sql-select-query/)                | It is used to retrieve data from the database                            | SELECT column1, column2, ...FROM table_name WHERE condition;                                            |
| FROM                                                                         | Indicates the ****table(s)**** from which to retrieve data.              | SELECT column1  <br>FROM table_name;                                                                    |
| [WHERE](https://www.geeksforgeeks.org/sql/sql-where-clause/)                 | Filters rows ****before**** any grouping or aggregation                  | SELECT column1  <br>FROM table_name  <br>WHERE condition;                                               |
| [GROUP BY](https://www.geeksforgeeks.org/sql/sql-group-by/)                  | Groups rows that have the same values in specified columns.              | SELECT column1, AVG_FUNCTION(column2)  <br>FROM table_name  <br>GROUP BY column1;                       |
| [HAVING](https://www.geeksforgeeks.org/sql/sql-having-clause-with-examples/) | Filters the results of GROUP BY                                          | SELECT column1, AVG_FUNCTION(column2)  <br>FROM table_name  <br>GROUP BY column1  <br>HAVING condition; |
| [DISTINCT](https://www.geeksforgeeks.org/sql/sql-distinct-clause/)           | Removes ****duplicate rows**** from the result set                       | SELECT DISTINCT column1, column2, ...  <br>FROM table_name;                                             |
| [ORDER BY](https://www.geeksforgeeks.org/sql/sql-order-by/)                  | Sorts the result set by one or more columns                              | SELECT column1  <br>FROM table_name  <br>ORDER BY column1 [ASC \| DESC];                                |
| [LIMIT](https://www.geeksforgeeks.org/mysql/mysql-limit-clause/)             | By default, it sorts in ****ascending order**** unless specified as DESC | SELECT * FROM table_name LIMI                                                                           |
3. DML - Data Manipulation Language: se utilizan para manipular los datos almacenados en las tablas de bases de datos.

|Command|Description|Syntax|
|---|---|---|
|[INSERT](https://www.geeksforgeeks.org/sql/sql-insert-statement/)|Insert data into a table|INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);|
|[UPDATE](https://www.geeksforgeeks.org/sql/sql-update-statement/)|Update existing data within a table|UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;|
|[DELETE](https://www.geeksforgeeks.org/sql/sql-delete-statement/)|Delete records from a database table|DELETE FROM table_name WHERE condition;|
4. DCL - Data Control Language: El lenguaje de control de datos (DCL) incluye comandos como GRANT y REVOKE, que gestionan principalmente los derechos, permisos y otros controles del sistema de base de datos

| Command | Description                                                                                                                 | Syntax                                                                                                     |
| ------- | --------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| GRANT   | Assigns new privileges to a user account, allowing access to specific database objects, actions or functions.               | GRANT privilege_type [(column_list)] ON [object_type] object_name TO user [WITH GRANT OPTION];             |
| REVOKE  | Removes previously granted privileges from a user account, taking away their access to certain database objects or actions. | REVOKE [GRANT OPTION FOR] privilege_type [(column_list)] ON [object_type] object_name FROM user [CASCADE]; |
5. TCL - Transaction Control Language: Las transacciones agrupan un conjunto de tareas en una única unidad de ejecución. Cada transacción comienza con una tarea específica y finaliza cuando todas las tareas del grupo se completan correctamente. Si alguna de las tareas falla, la transacción falla. Por lo tanto, una transacción solo tiene dos resultados: éxito o fracaso.

|Command|Description|Syntax|
|---|---|---|
|BEGIN TRANSACTION|Starts a new transaction|BEGIN TRANSACTION [transaction_name];|
|COMMIT|Saves all changes made during the transaction|COMMIT;|
|ROLLBACK|Undoes all changes made during the transaction|ROLLBACK;|
|SAVEPOINT|Creates a savepoint within the current transaction|SAVEPOINT savepoint_name;|
## SELECT
**Sintaxis básica:**
SELECT [Nombre de columnas]
FROM [Nombre de tablas]
WHERE [Criterios de selección]
ORDER BY [Criterios de ordenamiento]

**Operadores de comparación**
Igualdad -> "="
Mayor a -> ">"
Menor a -> "<"
Mayor o igual a -> ">="
Menor o igual a -> "<="

**Operadores generales**
- **CONCAT** -> Concatena los valores de dos columnas en una columna
  SELECT CONCAT(first_name, " ", last_name) AS full_name FROM patients
- **AND** -> Obliga el cumplimiento de dos condiciones o más
  SELECT * FROM customers WHERE city = 'Los Angeles' AND age < 30;
- **OR** -> Obliga el cumplimiento de una o más condiciones
  SELECT * FROM customers WHERE city = 'New York' OR age > 35;
- **LIKE** -> Es usado en la clausula WHERE para buscar un patron especifico en una columna

|Pattern|Meaning|
|---|---|
|'a%'|Match strings that start with 'a'|
|'%a'|Match strings with end with 'a'|
|'a%t'|Match strings that contain the start with 'a' and end with 't'.|
|'%wow%'|Match strings that contain the substring 'wow' in them at any position.|
|'_wow%'|Match strings that contain the substring 'wow' in them at the second position.|
|'_a%'|Match strings that contain 'a' at the second position.|
|'a_ _%'|Match strings that start with 'a and contain at least 2 more characters.|

- **IN** -> Es una forma de comparador pero con un conjunto de datos, muestra los datos que tengan un conjunto de valores.
  SELECT * FROM customers WHERE city IN ('New York', 'Chicago');
- **ORDER BY** -> Ordena el conjunto de resultados según una o más columnas
  SELECT name, age FROM employees ORDER BY age DESC;
	- **DESC**: Ordena en orden descendiente
	- **ASC**: Ordena en orden ascendiente (por defecto)
- **LIMIT** -> Restringe el numero de filas retornado
SELECT name, salary FROM employees ORDER BY salary DESC LIMIT 3;

- **BETWEEN AND** ->Se usa para especificar rangos de datos
  SELECT name, age FROM employees WHERE fechacontrato '1990-01-01' and '1990-12-31'
- **IS, NOT** -> Se asigna un valor por defecto
  SELECT name, age FROM employees WHERE email IS NULL
- **DISTINCT** -> Se usa para obtener solos los valores únicos de una columna.
  SELECT DISTINCT Country FROM Customer;
- **HAVING** -> Se usa para filtrar resultados después de aplicar la instrucción GROUP BY.
  SELECT Country, COUNT(*) AS customer_count FROM Customer GROUP BY Country  HAVING COUNT(*) >= 2;

**GROUP BY**
Query: Cuántoas compañias se tiene por pais?
SELECT country, COUNT(*) AS n_companies
FROM companies
GROUP BY country

Query: Precio promedio por unidad, el numero total de pedidos y la ganancia total para cada linea de producto
SELECT 
    product_line,
    AVG(unit_price) AS avg_price,
    SUM(quantity) AS tot_pieces,
    SUM(total) AS total_gain
FROM sales
GROUP BY product_line
ORDER BY total_gain DESC

Query: La misma query pero que muestre los que superen los 40000 de total
SELECT 
    product_line,
    AVG(unit_price) AS avg_price,
    SUM(quantity) AS tot_pieces,
    SUM(total) AS total_gain
FROM sales
GROUP BY product_line
HAVING SUM(total) > 40000
ORDER BY total_gain DESC

SELECT department, AVG(salary) AS average_salary FROM employees GROUP BY department;

Se usa para hacer agregación de un grupo de datos.
Usos:
- Dividir: el conjunto de datos se divide en fragmentos de filas segun los valores elegidos para la agregación
- Aplicar: Calcular una función agregada como promedio, mínimo y máximo. Devolviendo un único valor
- Combinar: Todos estos resultados se combinan en una única tabla. De esta forma, tendremos un único valor para cada modalidad de cariable
**Funciones de agregación**
Operan en grupos de filas y retornan un valor
Ignoran los valores NULL, excepto para COUNT()
Usualmente se usa con el statement GROUP BY
1. COUNT(): Cuenta el numero de filas en la tabla
   SELECT COUNT(Salary) AS NonNullSalaries FROM Employee;
2. SUM(): Calcula el valor numerico total de la columna
   SELECT SUM(DISTINCT Salary) AS DistinctSalarySum FROM Employee;
3. AVG(): Calcula el promedio de los valores numéricos de una columna
   SELECT AVG(Salary) AS AverageSalary FROM Employee;
4. MIN(), MAX(): Calculan el minimo o máximo de una columna y lo retornan
   SELECT MAX(Salary) AS HighestSalary FROM Employee;
## UPDATE
Sintaxis básica:
UPDATE [table_name]  
SET [column1 = value1, column2 = value2,...   ]
WHERE [condition];

Ejemplos:
**Query:** Actualizar una columna
UPDATE Customer  
SET CustomerName = 'Nitin'  
WHERE Age = 22;
**Explanation:** Only the rows where Age is 22 will be updated, and the CustomerName will be set to 'Nitin'.

**Query:** Actualizar multiples columnas
UPDATE Customer  
SET CustomerName = 'Satyam',  
Country = 'USA'  
WHERE CustomerID = 1;
**Explanation:** For the row where CustomerID is 1, both CustomerName and Country will be updated simultaneously.

## SQL JOINS
Las uniones SQL son herramientas fundamentales para combinar datos de múltiples tablas en bases de datos relacionales.
Tipos de uniones:
1. SQL INNER JOIN (JOIN is same as INNER JOIN): La palabra clave INNER JOIN selecciona ****todas**** las filas de ambas tablas siempre que se cumpla la condición. Esta palabra clave creará el conjunto de resultados combinando todas las filas de ambas tablas donde se cumpla la condición, es decir, el valor del campo común será el mismo.
	SELECT table1.column1,table1.column2,table2.column1,.... FROM table1  INNER JOIN table2 ON  table1.matching_column = table2.matching_column;
	SELECT
	  first_name,
	  last_name,
	  province_name
	FROM patients
	  JOIN province_names ON province_names.province_id = patients.province_id;
   ![[Pasted image 20250924123444.png|300]]
2. 
3. asdfsdf
4. asdfadsf
## Funciones de fecha
- YEAR(date): Estrae el año de una fecha, retorna el año como un numero entero.
- 
## OTROS

## Ejercicios
![[Pasted image 20250924130436.png|200]]
SELECT first_name, last_name, height
FROM patients
WHERE height = (SELECT MAX(height) FROM patients);
![[Pasted image 20250924131414.png|200]]
select distinct year(birth_date) as birth_year
from patients
order by birth_date asc
![[Pasted image 20250924131851.png|200]]
SELECT first_name
FROM patients
GROUP BY first_name
HAVING COUNT(first_name) = 1;
![[Pasted image 20250924132045.png|200]]
SELECT patient_id, first_name
FROM patients
where first_name like "s____%s"
