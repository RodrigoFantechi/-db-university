Query Todo:

- Selezionare tutti gli studenti nati nel 1990 (160)
```sql
SELECT * FROM students WHERE year(date_of_birth) like (o =) '1990';
```
- Selezionare tutti i corsi che valgono più di 10 crediti (479)
```sql
SELECT * FROM courses WHERE cfu > 10;
```
- Selezionare tutti gli studenti che hanno più di 30 anni
```sql
select * FROM students WHERE TIMESTAMPDIFF(Year, date_of_birth, curdate()) >30
```
- Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
```sql
SELECT * FROM courses WHERE period = 'I semestre' and year = 1;
```
- Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
```sql
SELECT * from exams WHERE date = '2020-06-20' and hour > '14:00:00';
```
- Selezionare tutti i corsi di laurea magistrale (38)
```sql
SELECT * FROM degrees WHERE level = 'magistrale';
```
- Da quanti dipartimenti è composta l'università? (12)
```sql
SELECT COUNT(id) as numero_dipartimenti from departments;
```
- Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
```sql
SELECT COUNT(id) as numero_insegnanti_senza_telefono from teachers where phone is NULL;
```
