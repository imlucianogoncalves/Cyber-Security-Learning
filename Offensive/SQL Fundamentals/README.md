# SQL - Guia Completo de Fundamentos

Notas sobre SQL e bancos de dados do caminho Pentester do TryHackMe.

---

## 📚 Objetivos de Aprendizagem

- Entender o que são bancos de dados e seus conceitos principais
- Conhecer os diferentes tipos de bancos de dados
- Compreender o que é SQL
- Dominar operações CRUD
- Aprender cláusulas e operadores SQL
- Utilizar funções SQL

---

## 🔄 Bancos de Dados: Relacionais vs. Não Relacionais

### Bancos Relacionais
Armazenam dados estruturados em tabelas (linhas e colunas) com formato fixo. Os dados podem se relacionar entre diferentes tabelas.

**Exemplo:** Uma tabela de `usuarios` conectada a uma tabela de `historico_pedidos`.

### Bancos Não-Relacionais
Armazenam dados não estruturados ou semiestruturados em formatos flexíveis como documentos, chaves-valor ou grafos. Ideais quando os dados não seguem um padrão fixo.

**Exemplo:** Documentos digitalizados com informações variadas.

---

## 🔐 Conectando ao MySQL

```sql
mysql -u root -p
mysql -u usuario -p
```

---

## 💾 Operações com Bancos de Dados

### Criar um banco de dados
```sql
CREATE DATABASE nome_do_banco;
```

### Listar todos os bancos
```sql
SHOW DATABASES;
```

### Selecionar um banco para usar
```sql
USE banco_de_dados;
```

### Deletar um banco de dados
```sql
DROP DATABASE nome_do_banco;
```

---

## 📋 Trabalhando com Tabelas

### Criar uma tabela
```sql
CREATE TABLE nome_tabela (
    coluna1 tipo_dado,
    coluna2 tipo_dado,
    coluna3 tipo_dado
);
```

**Exemplo prático:**
```sql
CREATE TABLE book_inventory (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    book_name VARCHAR(255) NOT NULL,
    publication_date DATE
);
```

### Visualizar estrutura da tabela
```sql
DESCRIBE nome_da_tabela;
```

### Modificar uma tabela (adicionar coluna)
```sql
ALTER TABLE book_inventory
ADD page_count INT;
```

---

## ✏️ Operações CRUD

### CREATE - Inserir dados
```sql
INSERT INTO books (id, name, published_date, description)
VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");
```

### READ - Ler dados
**Selecionar tudo:**
```sql
SELECT * FROM nome_da_tabela;
```

**Selecionar colunas específicas:**
```sql
SELECT name, description FROM books;
```

### UPDATE - Atualizar dados
```sql
UPDATE books
SET description = "An In-Depth Guide to Android's Security Architecture."
WHERE id = 1;
```

### DELETE - Deletar dados
```sql
DELETE FROM books WHERE id = 1;
```

---

## 🎯 Cláusulas SQL

### DISTINCT
Remove duplicatas dos resultados.

```sql
SELECT DISTINCT name FROM books;
```

### ORDER BY
Ordena os resultados em ordem ascendente (ASC) ou descendente (DESC).

```sql
SELECT * FROM books ORDER BY published_date ASC;
SELECT * FROM books ORDER BY published_date DESC;
```

### GROUP BY
Agrupa os resultados por uma ou mais colunas.

```sql
SELECT name, COUNT(*) FROM books GROUP BY name;
```

### HAVING
Filtra grupos resultantes de GROUP BY (similar ao WHERE, mas para grupos).

```sql
SELECT name, COUNT(*)
FROM books
GROUP BY name
HAVING name LIKE '%Hack%';
```

---

## 🔍 Operadores SQL

### LIKE
Busca por padrões de texto. Use `%` como curinga para representar qualquer caractere.

```sql
SELECT * FROM books WHERE description LIKE "%guide%";
```

### AND
Retorna resultados que atendem TODAS as condições.

```sql
SELECT * FROM books
WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp";
```

### OR
Retorna resultados que atendem PELO MENOS UMA das condições.

```sql
SELECT * FROM books
WHERE name LIKE "%Android%" OR name LIKE "%iOS%";
```

### NOT
Exclui resultados que atendem a condição.

```sql
SELECT * FROM books WHERE NOT description LIKE "%guide%";
```

### BETWEEN
Seleciona valores dentro de um intervalo (inclusivo).

```sql
SELECT * FROM books WHERE id BETWEEN 2 AND 4;
```

---

## 📝 Dicas Práticas

- Use `WHERE` para filtrar linhas individuais
- Use `HAVING` para filtrar grupos (depois de GROUP BY)
- Combine operadores com `AND`, `OR`, `NOT` para filtros mais complexos
- O `LIKE` é sensível ao contexto; use `%` nos locais apropriados
- Sempre use `WHERE` para ser específico ao deletar ou atualizar dados