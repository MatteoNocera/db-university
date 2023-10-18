<!-- GROUP BY -->

<!-- 1. Contare quanti iscritti ci sono stati ogni anno -->

SELECT COUNT(*) AS 'students_count_by_year', `students`.`enrolment_date` 
FROM `students` 
GROUP BY `students`.`enrolment_date`;

<!-- 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio -->

SELECT `office_address`, COUNT(*) AS 'same_office_count' 
FROM `teachers` 
GROUP BY `office_address` 
ORDER BY COUNT(`office_address`) DESC;

<!-- 3. Calcolare la media dei voti di ogni appello d'esame -->

SELECT `exam_id`, AVG(`exam_student`.`vote`) AS 'avg_vote' 
FROM `exam_student` 
GROUP BY `exam_id` 
ORDER BY `exam_id` ASC;

<!-- 4. Contare quanti corsi di laurea ci sono per ogni dipartimento -->

SELECT `department_id`, COUNT(*) AS 'numberOfdegrees'
FROM `degrees`
GROUP BY `department_id`
ORDER BY COUNT('numberOfDegrees') ASC;



<!-- JOINS -->

<!-- 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia -->

SELECT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `degrees`.`name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia'
ORDER BY `students`.`surname` ASC;

<!-- 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienzeo -->

SELECT `degrees`.`name`, `degrees`.`id`, `degrees`.`address`, `degrees`.`email`, `departments`.`name`
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `level` = 'magistrale' 
AND `departments`.`name` = 'Dipartimento di Neuroscienze';

<!-- 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44) -->

SELECT `degrees`.*, `teachers`.`name`, `teachers`.`surname`
FROM `degrees`     
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `teacher_id` = `teachers`.`id`
WHERE `teachers`.`name` = 'Fulvio'
AND `teachers`.`surname` = 'Amato';

<!-- 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome -->

SELECT DISTINCT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `degrees`.`name`, `degrees`.`level`, `departments`.`name`, `departments`.`address`, `departments`.`website`
FROM `students` 
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`name` ASC, `students`.`surname` ASC;

<!-- 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti -->

SELECT `courses`.`id`, `courses`.`name`, `courses`.`period`, `teachers`.`name`, `teachers`.`surname`, `degrees`.`name`, `degrees`.`level`
FROM `courses`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
ORDER BY `teachers`.`surname` ASC;

<!-- 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)) -->

SELECT DISTINCT `teachers`.*, `departments`.`name`
FROM `teachers`
JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
ORDER BY `teachers`.`id` DESC;


<!-- 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18. -->


SELECT `students`.`id`, `students`.`name`, `students`.`surname`, MAX(`exam_student`.`vote`)
FROM `students`
JOIN `exam_student` ON `students`.`id` = `exam_student`.`student_id`
GROUP BY `exam_student`.`exam_id`;