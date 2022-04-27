# Comandos SQL - Referência

## Modelagem Física

### Criar banco de dados
```sql
CREATE DATABASE cinema CHARACTER SET utf8mb4;
```

### Criat tabelas filmes

```sql
CREATE TABLE filmes(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(45) NOT NULL,
    lancamento YEAR(4) NOT NULL,
    generos_id INT  NOT NULL
);
```
### Visualizar detalhes estruturais da tabela
```sql
DESC filmes;
```
### Criar tabelas genêros
```sql
CREATE TABLE generos(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45) NOT NULL,
    filmes_id INT NOT NULL
);
```
# Criação da chave estrangeira (relacionamento entre as tabelas)
```sql
ALTER TABLE filmes
 ADD CONSTRAINT fk_filmes_generos

 FOREIGN KEY(generos_id) REFERENCES generos(id);
 ```