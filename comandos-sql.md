# Comandos SQL - Referência

## Modelagem Física

### Criar banco de dados
```sql
CREATE DATABASE vendas CHARACTER SET utf8mb4;
```

### Criar tabela fabricantes

```sql
CREATE TABLE fabricantes(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45) NOT NULL
);
```

### Visualizar detalhes estruturais da tabela
```sql
DESC fabricantes;
```

### Criar tabelas produtos
```sql
CREATE TABLE produtos(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45) NOT NULL,
    descricao TEXT(1000) NOT NULL,
    preco DECIMAL(6,2) NOT NULL,
    fabricantes_id INT NOT NULL
);
```

### Criação da chave estrangira (relacionamento entre as tabelas)
```sql
ALTER TABLE produtos
# CONSTRAINT é uma restrição definida no relaciomaneto
    ADD CONSTRAINT fk_produtos_fabricantes

# A chave estrangera deve fazer referência á chave primária
    FOREIGN KEY(fabricantes_id) REFERENCES fabricantes(id);
```

### Adicionar campo/coluna em uma tabela
```sql
ALTER TABLE `produtos` ADD `fabricante_id` INT NOT NULL AFTER `preco`;
```