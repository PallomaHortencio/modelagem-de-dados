### Etapa 1

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
        segunda_nota DECIMAL(4,2) NOT NULL,
        cursos_id INT NOT NULL
);
```   

### Etapa 2

```sql
 INSERT INTO `professor`(`id`, `nome`, `area`, `cursos_id`) VALUES ('1','Palloma Hortencio','infra','6'), 
 ('2', 'Gabriel Genovez', 'Desenvolvimento', '9'), ('3', 'Tiago Ribeiro', 'Design', '8'), ('4', 'Antonio Vinicius', 'Desenvolvimento', '7'), ('5', 'Lucas Mendes', 'Design', '10');

```

```sql

INSERT INTO `cursos` (`id`, `titulo`, `carga`, `professor_id`) VALUES (NULL, 'Front-End', '40', NULL);

INSERT INTO `cursos` (`id`, `titulo`, `carga`, `professor_id`) VALUES (NULL, 'Back-End', '80', NULL);

INSERT INTO `cursos` (`id`, `titulo`, `carga`, `professor_id`) VALUES (NULL, 'UX/UI Design', '80', NULL);

INSERT INTO `cursos` (`id`, `titulo`, `carga`, `professor_id`) VALUES (NULL, 'Figma', '10', NULL);

INSERT INTO `cursos` (`id`, `titulo`, `carga`, `professor_id`) VALUES (NULL, 'Rede de Computadores', '100', NULL);
```

```sql
INSERT INTO `alunos`(`id`, `nome`, `nascimento`, `primeira_nota`, `segunda_nota`, `curso_id`) VALUES 
('1','João Silva','2001-03-10','5','6','6'), 
('2', 'Natalia Martins', '2001-11-25', '15-02-2001', '7', '8', '9'),
('3', 'Igor Siqueira', '2002-02-18', '8', '7', '8'),
('4', 'Leticia Hortencio', '2010-03-24', '5', '4', '7'),
('5', 'Maria Eduarda', '2012-08-14', '4', '3', '10'),
('6', 'Pedro Souza', '1999-09-30', '6', '4', '10'),
('7', 'Rafael Abdala', '2003-10-03', '8', '9', '6'),
('8', 'Mateus Ribeiro', '2009-06-07', '7', '5', '9'),
('9', 'Guilherme Mendes', '2011-11-29', '6', '4', '7'),
('10', 'Alice Lopes', '2015-04-11', '3', '5', '8');
```

### Etapa 3

```sql
SELECT nome, nascimento FROM alunos WHERE nascimento < '2009-01-01';
![image]()

SELECT nome, primeira_nota, segunda_nota, ROUND((primeira_nota + segunda_nota)/2, 2) AS 'Média' FROM alunos;
      
SELECT titulo, carga, (carga * 0.25) AS 'Faltas' FROM cursos ORDER BY titulo;

SELECT nome, area FROM professor WHERE area = 'desenvolvimento';

SELECT area, COUNT(nome) AS professor FROM professor GROUP BY area;

SELECT alunos.nome AS alunos, titulo, cursos.carga FROM alunos
INNER JOIN cursos ON alunos.curso_id = cursos.id 
ORDER BY alunos.nome;

SELECT professor.nome AS professor, titulo FROM professor
INNER JOIN cursos ON professor.cursos_id = cursos.id 
ORDER BY professor.nome;

SELECT alunos.nome AS alunos, cursos.titulo, professor.nome FROM alunos
INNER JOIN cursos ON alunos.curso_id = cursos.id  
INNER JOIN professor ON cursos.professor_id = professor.id;





```
