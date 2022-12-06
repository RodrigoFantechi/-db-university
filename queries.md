## Esercizio del 05-12-22

Query Todo:

- Selezionare tutti gli studenti nati nel 1990 (160)
```sql
SELECT `*` FROM `students` WHERE year(`date_of_birth`) = '1990';
```
- Selezionare tutti i corsi che valgono più di 10 crediti (479)
```sql
SELECT `*` FROM `courses` WHERE `cfu` > 10;
```
- Selezionare tutti gli studenti che hanno più di 30 anni
```sql
select `*` FROM `students` WHERE TIMESTAMPDIFF(Year, `date_of_birth`, curdate()) >30
```
- Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
```sql
SELECT `*` FROM `courses` WHERE `period` = 'I semestre' and `year` = 1;
```
- Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
```sql
SELECT `*` from `exams` WHERE `date` = '2020-06-20' and `hour` > '14:00:00';
```
- Selezionare tutti i corsi di laurea magistrale (38)
```sql
SELECT `*` FROM `degrees` WHERE `level` = 'magistrale';
```
- Da quanti dipartimenti è composta l'università? (12)
```sql
SELECT COUNT(`id`) as 'numero_dipartimenti' from `departments`;
```
- Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
```sql
SELECT COUNT(`id`) as 'numero_insegnanti_senza_telefono' from `teachers` where `phone` is NULL;
```
## Esercizio del 06-12-22

Group by:

- Contare quanti iscritti ci sono stati ogni anno
```sql
SELECT year(`enrolment_date`) as 'year' ,COUNT(`id`) as'number of subscriptions' FROM `students` GROUP BY year(`enrolment_date`);
```
- Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
SELECT office_address, COUNT(id) as 'number of teachers' FROM teachers GROUP BY office_address;
```
- Calcolare la media dei voti di ogni appello d'esame
```sql
SELECT `exam_id` as 'codice appello', AVG(`vote`) as 'media appello' FROM `exam_student` GROUP BY `exam_id`;
```
- Contare quanti corsi di laurea ci sono per ogni dipartimento
```sql
SELECT `department_id` as 'numero dipartimento', COUNT(id) as 'numero di corsi di laurea' FROM `degrees` GROUP BY `department_id`;
```

Join:

- Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```sql
SELECT `students`.`*`, `degrees`.`name` from `students` JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```
- Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
```sql
SELECT `degrees`.`*`, `departments`.`name` FROM `degrees` JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' and `degrees`.`level` = 'magistrale';
```
- Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
SELECT `courses`.`*` , `teachers`.`name`, `teachers`.`surname` FROM `course_teacher` JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id` JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` WHERE `teachers`.`id` = 44;
```
- Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
```sql
SELECT `students`.`name` as 'nome studente',`students`.`surname` as 'cognome studente', `degrees`.`*` , `departments`.`name` as 'nome dipartimento' FROM `degrees` JOIN `students` on `degrees`.`id` = `students`.`degree_id` JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` ORDER BY `students`.`surname` ASC, `students`.`name` ASC;
```
- Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```sql
select  `degrees`.`*`, `teachers`.`name` as 'nome insegnante', `teachers`.`surname` as 'cognome insegnante', `courses`.`name` as 'nome corso' FROM `course_teacher` JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`;
```
- Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
```sql
SELECT DISTINCT `teachers`.`*`, `departments`.`name` as 'nome dipartimento' FROM `course_teacher` JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id` JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` WHERE `departments`.`name` = 'Dipartimento di Matematica';
```
- BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami
```sql

```