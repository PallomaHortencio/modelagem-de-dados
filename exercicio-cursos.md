```sql
CREATE TABLE professor(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(50) NOT NULL,
    area ENUM('design', 'desenvolvimento', 'infra') NOT NULL,
    cursos_id INT NOT NULL
);
```

```sql
CREATE TABLE cursos (
        id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        titulo VARCHAR(30) NOT NULL,
        carga SMALLINT NOT NULL,
        professor_id INT NOT NULL
);
```

```sql
CREATE TABLE alunos (
        id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        nome VARCHAR (50) NOT NULL,
        nascimento DATE NOT NULL,
        primeira_nota DECIMAL(4,2) NOT NULL,
        segunda_nota DECIMAL(4,2) NOT NULL
);
```