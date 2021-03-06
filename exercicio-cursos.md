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
/* 1 */
SELECT nome, nascimento FROM alunos WHERE nascimento < '2009-01-01';
```
![c1](consulta/consulta-1.jpeg)

```sql
/* 2 */
SELECT nome, primeira_nota, segunda_nota, ROUND((primeira_nota + segunda_nota)/2, 2) AS 'Média' FROM alunos;
```
![c2](consulta/consulta-2.jpeg)

 ```sql
 /* 3 */
SELECT titulo, carga, (carga * 0.25) AS 'Faltas' FROM cursos ORDER BY titulo;
```
![c3](consulta/consulta-3.jpeg)

```sql
/* 4 */
SELECT nome, area FROM professor WHERE area = 'desenvolvimento';
```
![c4](consulta/consulta-4.jpeg)

```sql
/* 5 */
SELECT area, COUNT(nome) AS professor FROM professor GROUP BY area;
```
![c5](consulta/consulta-5.jpeg)

```sql
/* 6 */
SELECT alunos.nome AS alunos, titulo, cursos.carga FROM alunos
INNER JOIN cursos ON alunos.curso_id = cursos.id 
ORDER BY alunos.nome;
```
![c6](consulta/consulta-6.jpeg)

```sql
/* 7 */
SELECT professor.nome AS professor, titulo FROM professor
INNER JOIN cursos ON professor.cursos_id = cursos.id 
ORDER BY professor.nome;
```
![c7](consulta/consulta-7.jpeg)

```sql
/* 8 */
SELECT alunos.nome AS alunos, cursos.titulo, professor.nome FROM alunos
INNER JOIN cursos ON alunos.curso_id = cursos.id  
INNER JOIN professor ON cursos.professor_id = professor.id;
```
![c8](consulta/consulta-8.jpeg)

```sql
/* 9 */
SELECT (cursos.titulo) AS "Cursos",COUNT(alunos.curso_id) AS "Qtd. de alunos"  FROM alunos INNER JOIN cursos
ON alunos.curso_id = cursos.id 
GROUP BY curso_id ORDER BY curso_id DESC;
```
![c9](consulta/consulta-9.jpeg)

```sql
/* 10 */
SELECT alunos.nome, alunos.primeira_nota, alunos.segunda_nota, ROUND(AVG(alunos.primeira_nota + alunos.segunda_nota)/2, 2) AS "Médias", cursos.titulo FROM alunos INNER JOIN cursos ON alunos.curso_id = cursos.id WHERE cursos.titulo = "Front-End" OR cursos.titulo = "Back-End" GROUP BY alunos.nome ORDER BY alunos.nome;
```
![c10](consulta/consulta-10.jpeg)

```sql
/* 11 */
UPDATE cursos SET titulo = 'Adobe XD' WHERE id = 9;
UPDATE cursos SET carga = 15 WHERE id =9;
```
![c11](consulta/consulta-11.jpeg)

```sql
/* 12 */
DELETE FROM alunos WHERE id = 5 OR id = 10;
```
![c12](consulta/consulta-12.jpeg)

```sql
/* 13 */
SELECT alunos.nome, cursos.titulo FROM alunos INNER JOIN cursos ON alunos.curso_id = cursos.id ORDER BY alunos.nome;
```
![c13](consulta/consulta-13.jpeg)



### Desafios
```sql
/* desafio 1 */
SELECT nome AS Nome, TIMESTAMPDIFF(YEAR, nascimento, curdate()) AS Idade FROM alunos;
```
![d1](consulta/desafio-1.jpeg)


```sql
/* desafio 2 */
SELECT nome, primeira_nota, segunda_nota, ROUND((primeira_nota+segunda_nota)/2) AS Média FROM alunos WHERE (primeira_nota+segunda_nota)/2 >= 7;
```
![d2](consulta/desafio-2.jpeg)


```sql
/* desaio 3 */
SELECT nome, primeira_nota, segunda_nota, ROUND((primeira_nota+segunda_nota)/2) AS Média FROM alunos WHERE (primeira_nota+segunda_nota)/2 < 7;
```
![d3](consulta/desafio-3.jpeg)


```sql
/* desafio 4 */
SELECT COUNT((primeira_nota+segunda_nota)/2) AS 'Qtd de alunos com média acima ou igual à 7' FROM alunos WHERE (primeira_nota+segunda_nota)/2 >= 7;
```
![d4](consulta/desafio-4.jpeg)

