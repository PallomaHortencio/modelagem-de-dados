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


```sql
INSERT INTO professor (nome, area, curso_id) VALUES
('Palloma'
'infra'),
('Gabriel'
'design'),
('Antonio'
'design'),
('Tiago'
'desenvolvimento'),
('Klaibert'
'desenvolvimento');
```
Jon Oliva, área infra
Lemmy Kilmister, área design
Neil Peart, área design
Ozzy Osbourne, área desenvolvimento
David Gilmour, área desenvolvimento


```sql
INSERT INTO `cursos` (`id`, `titulo`, `carga`, `professor_id`) VALUES (NULL, 'Front-End', '40', NULL);

INSERT INTO `cursos` (`id`, `titulo`, `carga`, `professor_id`) VALUES (NULL, 'Back-End', '80', NULL);

INSERT INTO `cursos` (`id`, `titulo`, `carga`, `professor_id`) VALUES (NULL, 'UX/UI Design', '80', NULL);

INSERT INTO `cursos` (`id`, `titulo`, `carga`, `professor_id`) VALUES (NULL, 'Figma', '10', NULL);

INSERT INTO `cursos` (`id`, `titulo`, `carga`, `professor_id`) VALUES (NULL, 'Rede de Computadores', '100', NULL);
```