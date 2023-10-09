# Database University Part 1

## Consegna

Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
  Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

# Database University Part 2

## Consegna

1. Selezionare tutti gli studenti nati nel 1990 (160)

- SELECT \* FROM `students` WHERE `date_of_birth` LIKE '1990%'; (restituisce una stringa)
- SELECT \* FROM `students` WHERE YEAR(`date_of_birth`) = 1990; (restituisce un intero)

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

- SELECT \* FROM `courses` WHERE `cfu`> '10';
- SELECT `id`, `name`, `cfu` FROM `courses` WHERE `cfu` > 10 ;

3. Selezionare tutti gli studenti che hanno più di 30 anni

- SELECT \*, TIMESTAMPDIFF(year, `date_of_birth`, CURDATE()) AS `student_age` FROM `students` WHERE TIMESTAMPDIFF(year, `date_of_birth`, CURDATE()) > 30 ;

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
   laurea (286)

- SELECT \* FROM `courses` WHERE `period` LIKE 'I semestre' AND `year` = 1;
- SELECT \* FROM `courses` WHERE `period` = "I semestre" AND `year` = 1 ORDER BY `cfu` DESC;

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
   20/06/2020 (21)

- SELECT \* FROM `exams` WHERE `date` LIKE '2020-06-20' AND `hour` > '14:00:00';
- SELECT \* FROM `exams` WHERE `date` = '2020-06-20' AND HOUR (`hour`) >= 14;

6. Selezionare tutti i corsi di laurea magistrale (38)

- SELECT \* FROM `degrees` WHERE `level` = 'magistrale';

7. Da quanti dipartimenti è composta l'università? (12)

- SELECT COUNT(`id`) FROM `departments`;
- SELECT COUNT(\*) AS `departments_number` FROM `departments`;

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

- SELECT COUNT(`id`) FROM `teachers` WHERE `phone` is NULL;
- SELECT COUNT(\*) AS `teacher_without_phone` FROM `teachers` WHERE `phone` is NULL;
