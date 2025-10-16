# SQL - Fundamentals

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe

Objetivos De Aprendizagem

- Entenda o que são bancos de dados, bem como os principais termos e conceitos
- Entenda os diferentes tipos de bancos de dados 
- Entenda o que SQL é
- Compreender e ser capaz de usar SQL Operações CRUD
- Compreender e ser capaz de usar SQL Cláusulas Operações
- Compreender e ser capaz de usar SQL Operações
- Compreender e ser capaz de usar SQL Operadores
- Compreender e ser capaz de usar SQL Funções

---

## Relacionais vs. Não Relacionais

- **Bancos de dados relacionais:** armazenam dados estruturados em tabelas (linhas e colunas). Os dados seguem um formato fixo e podem se relacionar entre diferentes tabelas — por exemplo, usuarios e historico_pedidos.

- **Bancos de dados não relacionais:** armazenam dados não estruturados ou semiestruturados em formatos flexíveis (como documentos, chaves-valor ou grafos). São ideais quando os dados não seguem um padrão fixo, como documentos digitalizados com informações variadas.

---

## Configurando MySQL

Acessamos um banco de dados com:

`mysql -u root -p` 

`mysql -u usuario -p`

---

## Criando banco de dados

Para criar um banco de dados, utilizamos 

`CREATE DATABASE nome_do_banco;`

`SHOW DATABASES` mostra todos os banco de dados que temos.

---

Para interagir com determinado banco de dados, precisamos falar para o MySQL que vamos acessar o banco X, isso é feito com:

`USE banco_de_dados;`

`DROP database nome_do_banco;` - exclui o banco de dados.

---

Para criar tabelas, usamos o seguinte modelo:

```
mysql> CREATE TABLE example_table_name (
    example_column1 data_type,
    example_column2 data_type,
    example_column3 data_type
);
```

Que na prática ficaria como:

```
mysql> CREATE TABLE book_inventory (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    book_name VARCHAR(255) NOT NULL,
    publication_date DATE
);
```

Para descrever a estrutura de determinada tabela, podemos usar o 

`DESCRIBE nome_da_tabela`

---

Podemos usar `ALTER` para mudar a estrutura da tabela, o que ficaria mais ou menos assim:

```
mysql> ALTER TABLE book_inventory
    -> ADD page_count INT;

```

---

Para incluir uma row em uma tabela, podemos usar:

```
mysql> INSERT INTO books (id, name, published_date, description)
    VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");
```

---

Agora, para ler os dados dessa ou outra tabela, podemos usar 

`SELECT * FROM nome_da_tabela;`

---

Da pra filtrar, selecionando apenas as colunas que você quiser, como:

`SELECT name, description FROM books;`

---

Para atualizar um item:

```
mysql> UPDATE books
    SET description = "An In-Depth Guide to Android's Security Architecture."
    WHERE id = 1;SELEC
```

---

Para deletar um item da tabela, usamos 

`DELETE FROM books WHERE id = 1;`

---

## Clauses

`DISTINCT` evita duplicações quando executamos alguma query, como:

`SELECT DISTINCT name FROM books;`

---

`GROUP BY` agrupa por determinada condição.

```
mysql> SELECT name, COUNT(*)
    FROM books
    GROUP BY name;
```

---

`ORDER BY` 

Aqui o próprio nome ja diz, ele ordena o output com base no que você quer, o ASC é ascendente e DESC é descendente.

```
mysql> SELECT *
    FROM books
    ORDER BY published_date ASC;
```

---
`HAVING`

Nesse caso, é buscado pela reges onde temos o `LIKE`

```
mysql> SELECT name, COUNT(*)
    FROM books
    GROUP BY name
    HAVING name LIKE '%Hack%';
```

## Operadores

Temos o LIKE que sempre vem junto do WHERE e nos trás uma consulta sobre determinada alavra-chave, como:

```
mysql> SELECT *
    FROM books
    WHERE description LIKE "%guide%";
```

---

O AND seleciona dois valores distintos.

```
mysql> SELECT *
    FROM books
    WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp";
```

---

OR, nos traz um dos dois valores, se o primeiro for true ele para, se o primeiro for false ele tenta o segundo

```
mysql> SELECT *
    FROM books
    WHERE name LIKE "%Android%" OR name LIKE "%iOS%"; 
```

---

NOT exclui algo da consulta

```
mysql> SELECT *
    FROM books
    WHERE NOT description LIKE "%guide%";
```

Nesse caso ele selecionou tudo da tabela, menos na linha que tiver ocorrencias de guide na descrição.

---

BETWEEN pega valores entre números

```
mysql> SELECT *
    FROM books
    WHERE id BETWEEN 2 AND 4;
```