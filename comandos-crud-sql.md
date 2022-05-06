# Comandos SQL para CRUD - Referência

### Resumo
- C -> Create (inserir dados)
- R -> Read (ler dados)
- U -> Update (atualizar dados)
- D -> Delete (excluir dados)

## Insert
```sql
INSERT INTO fabricantes (nome) VALUES('Asus');
INSERT INTO fabricantes (nome) VALUES('Dell');

INSERT INTO fabricantes (nome) 
VALUES('Apple'), ('LG'), ('Samsung'), ('Brastemp');
```

### Produtos
```sql
INSERT INTO produtos(nome, descricao, preco, quantidade, fabricantes_id) VALUES(
    'Ultrabook',
    'Ultrabook Asus com processador Intel Core i12, memória RAM de 16GB e Windows 11',
    6500.99, 
    7,
    1
);

INSERT INTO produtos(nome, descricao, preco, quantidade, fabricantes_id) VALUES(
    'Tablet Android',
    'Tablet com a versão 12 do sistema operacional da Google, possui tela de 10 polegadas e armazenamento de 64GB.',
    4999, 
    3,
    5 # Samsung
);

INSERT INTO produtos(nome, descricao, preco, quantidade, fabricantes_id) VALUES
   (
       'Xbox',
       'Console de ultima geração com acesso aos melhores jogos e bla bla bla',
       2500,
       6,
       7 # Microsoft
   ),
   (
       'Ultrabook',
       'equipamentos com processador AMD ryzen5, 12gb de ram, placa de video rtx',
       4500.68,
       12,
       8 # Positivo
    );


```

```sql
INSERT INTO fabricantes (nome) 
VALUES('Positivo'), ('Microsoft');
```

```sql
INSERT INTO produtos(nome, descricao, preco, quantidade, fabricantes_id) VALUES
   (
       'Geladeira',
       'Refrigerador Frost-Free com acesso á Internet das Coisas e bla bla bla',
       1500,
       10,
       6 # Brastemp
   ),
   (
       'Iphone 13 Pro Max',
       'Alta durabilidade, processador Bionic 14, 128GB de armazenamento',
       6999.99,
       3,
       3 # Apple
   ),
   (
       'Ipad Mini',
       'Tablet Apple com tela retina display de 4k, memória interna de 64GB, acesso ao icloud.',
       5000,
       8,
       3 -- Apple
    );
```

## SELECT

### Ler dados da tabela produtos
```sql
SELECT * FROM produtos;
SELECT nome, preco FROM produtos;
SELECT nome FROM produtos WHERE preco < 5000;

SELECT nome, descricao FROM produtos
WHERE fabricantes_id = 3; 
```

### Operadores Lógicos: E OU NÃO
```sql
SELECT * FROM produtos WHERE preco >= 5000 AND preco < 8000;

SELECT nome, preco FROM produtos
-- dos fabricantes apple ou microsoft
```

### Filtros
```sql
SELECT nome, preco FROM produtos ORDER BY nome; -- ASC
-- ASC -> ordenação em modo crescente (padrão)
-- DSC -> ordenação em modo decrescente (não é padrão, quando quiser usar tem que colocar)
SELECT nome, preco FROM produtos ORDER BY nome DESC;
SELECT nome, descricao FROM produtos
WHERE descricao LIKE '%processador%'; -- LIKE (COMO)
-- % OPERADOR CORINGA (SIGNIFICA QUALQUER TEXTO)
```

### Operações e funções de agregação
```sql
SELECT SUM(preco) FROM produtos; -- SOMA
SELECT SUM(preco) AS TOTAL FROM produtos; -- AS É ALIAS (APELIDO)

SELECT SUM(quantidade) AS "Quantidade em estoque" FROM produtos WHERE fabricantes_id = 3; -- Apple
SELECT AVG(preco) AS  "Média dos preços" FROM produtos;-- AVG (AVERAGE) MÉDIA
SELECT ROUND (AVG(preco), 2) AS  "Média dos preços" FROM produtos; -- ROUND é arredondamento dos valores

-- COUNT (Contagem)
SELECT COUNT(id) AS "Quantidades de produtos" FROM produtos;

SELECT COUNT(DISTINCT fabricantes_id) AS "Quantidades de produtos" FROM produtos; 
-- DISTINCT é um comando para evitar a duplicidade na contagem em campos que não são chave-primária 

SELECT nome, preco, quantidade, (preco * quantidade) AS Total FROM produtos;
```

### Agrupamentos
```sql
SELECT fabricantes_id, SUM(preco) AS Total FROM produtos
GROUP BY fabricantes_id;
-- GROUP BY permite segmentar resultados da consulta. Neste caso, somamos todos os preços e segmentos/agrupamos por cada fabricante.
```


## Update (sempre com WHERE)

### Atualizar dados de uma tabela
```sql
UPDATE fabricantes SET nome = 'Microsoft Brasil' WHERE id = 8;

-- Mudar o preço do Ultrabook da Positivo para 5200.
UPDATE produtos SET preco = 5200 WHERE id = 7;

-- Mudar a quantidade dos produtos da Asus e da Apple para 15.
UPDATE produtos SET quantidade = 15 WHERE fabricantes_id = 1 OR fabricantes_id = 3;
```

## Excluir dados de uma tabela
```sql
DELETE FROM fabricantes WHERE id = 4; -- LG

DELETE FROM produtos WHERE preco <= 2000 AND preco > 500;
```


<!-- CTRL + SHIFT + ENTER = executa direto no mysql -->


### Consultas em duas ou mais tabelas (JUNÇÂO)
```sql  
-- nomeDaTabela.nomeDaColuna
SELECT produtos.nome, fabricantes.nome 

-- INNER JOIN é o comando que permite JUNTAR tabelas
FROM produtos INNER JOIN fabricantes

-- ON comando para indicar o criterio da junção
 ON produtos.fabricantes_id = fabricantes.id;

 SELECT
 produtos.nome AS Produto, 
 fabricantes.nome AS Fabricantes
 FROM produtos INNER JOIN fabricantes
 ON produtos.fabricantes_id = fabricantes.id
 ORDER BY produtos.nome, fabricante.nome;


 -- Fabricante, soma dos preços e quantidade dos produtos
 SELECT 
 fabricantes.nome AS Fabricante,
 SUM(produtos.preco) AS Total,
 COUNT(produtos.fabricantes_id) AS "Qtd de Produtos",
 FROM produtos INNER JOIN fabricantes
 ON produtos.fabricantes_id = fabricantes.id
 GROUP BY Fabricante
 ORDER BY Total;
 
 -- Trazer a quantidade de produtos de cada fabricante

 SELECT 
 fabricantes.nome AS fabricantes,
 COUNT(produtos.id) AS "Quantidade de Produtos"
 FROM produtos INNER JOIN fabricantes
 ON produtos.fabricantes_id = fabricantes.id
 GROUP BY Fabricantes;


-- RIGHT exibe fabricantes que não tem produtos
 SELECT 
 fabricantes.nome AS fabricantes,
 COUNT(produtos.id) AS "Quantidade de Produtos"
 FROM produtos RIGHT JOIN fabricantes
 ON produtos.fabricantes_id = fabricantes.id
 GROUP BY Fabricantes;


```