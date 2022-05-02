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
