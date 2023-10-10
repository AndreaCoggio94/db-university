# DB University

## Consegna

Utilizzando lo stesso database di ieri, eseguite le query in allegato. Caricate un secondo file nella stessa repo di ieri (db-university) con le query di oggi.

### Query GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno

```SQL
   SELECT COUNT(*) `students_enrolled`, YEAR(`enrolment_date`) `enrolment_year` FROM `students` GROUP BY YEAR(`enrolment_date`);
```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```SQL
    SELECT `office_address`, COUNT(*) `number_of_teachers` FROM `teachers` GROUP BY `office_address`;
```

3. Calcolare la media dei voti di ogni appello d'esame

```SQL
    SELECT AVG(`vote`) `vote_average`, `exam_id` `exam_round` FROM `exam_student` GROUP BY `exam_id`;
```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```SQL
    SELECT COUNT(*) `degrees`, `department_id` `department` FROM `degrees` GROUP BY `department_id`;
```

### Query JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```SQL
    SELECT `students`.`name` , `students`.`surname` , `degrees`.`name` FROM `students` JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` WHERE `degrees`.`name` = "Corso di Laurea in Economia";
```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
   Neuroscienze

```SQL
    SELECT `departments`.`name` `department_name`, `degrees`.`level` `degree_level` , `courses`.`name` `course_name` FROM `departments` JOIN `degrees` ON `department_id` = `departments`.`id` JOIN `courses` ON `degree_id` = `degrees`.`id` WHERE `departments`.`name` = "Dipartimento di Neuroscienze" AND `degrees`.`level` = "magistrale";
```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```SQL
    SELECT `teachers`.`name`, `teachers`.`surname`, `courses`.`name` FROM `teachers` JOIN `course_teacher` ON `teacher_id` = `teachers`.`id` JOIN `courses` ON `course_id` = `courses`.`id` WHERE `teachers`.`id` = 44;
```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
   sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
   nome

```SQL
    SELECT `students`.`surname`, `students`.`name`, `degrees`._, `departments`._ FROM `departments` JOIN `degrees` ON `department_id` = `departments`.`id` JOIN `students` ON `degree_id` = `degrees`.`id` ORDER BY `students`.`surname`, `students`.`name`;
```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```SQL
    SELECT `degrees`._, `courses`._ , `teachers`.`surname`, `teachers`.`name` FROM `degrees` JOIN `courses` ON `degree_id`= `degrees`.`id` JOIN `course_teacher` ON `course_id` = `courses`.`id` JOIN `teachers` ON `teacher_id` = `teachers`.`id` ORDER BY `degrees`.`name`;
```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)

```SQL
    SELECT DISTINCT `departments`.`name`, `teachers`.`surname`, `teachers`.`name` FROM `departments` JOIN `degrees` ON `department_id` = `departments`.`id` JOIN `courses` ON `degree_id`= `degrees`.`id` JOIN `course_teacher` ON `course_id` = `courses`.`id` JOIN `teachers` ON `teacher_id` = `teachers`.`id` WHERE `departments`.`name` = "Dipartimento di Matematica" ORDER BY `teachers`.`surname` , `teachers`.`name`;
```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.

```SQL
    SELECT COUNT(*) `amount_of_tries` , `students`.`id` `id_student`, `students`.`name` `student_name`, `students`.`surname` `student_surname`, MAX(`exam_student`.`vote`) `max_vote`, `courses`.`id` `id_course`, `courses`.`name` `course_name` FROM `students` JOIN `exam_student` ON `student_id` = `students`.`id` JOIN `exams` ON `exam_id` = `exams`.`id` JOIN `courses` ON `course_id` = `courses`.`id` GROUP BY `students`.`id` , `courses`.`id` HAVING MAX(`exam_student`.`vote`) >= 18;
```
