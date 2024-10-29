# Learn-SQL-by-Building-a-Student-Database-Part-2
Se inicia con echo en Bash, luego se conecta a la base de datos y usa psql para listar y consultar tablas.

# Resumen
Este es un resumen de los pasos principales para conectar, consultar y automatizar información en PostgreSQL usando Bash y SQL. Primero, se inicia con el comando echo en Bash, luego se conecta a la base de datos y se ejecutan comandos básicos en psql para listar, seleccionar y manipular tablas. En un segundo paso, se crea y configura un script de Bash (student_info.sh) para obtener información sobre los estudiantes, integrando consultas SQL condicionales y agregadas que imprimen datos específicos, como el GPA y los cursos. Finalmente, se usan JOINs y filtros avanzados en SQL para extraer y visualizar datos complejos según diversas condiciones.

# Pasos

1. Escribir `echo hello` en la terminal bash
2. Conectarse a la base de datos con --username=freecodecamp --dbname=postgres 
3. Listar con /l en el psql
4. Se divide la terminal y se conencta la base de datos estudiantes con el comando psql -U postgres < students.sql
Listamos students.sql con  /l em psql
5. Conectar a la base de datos students \c students
6. Mostrar la base de datos con \d en psql
7.Mostamos solo students \d students
8. Vemos toda la tabla con SELECT * FROM students;
9. hacer un script para imprimir información sobre tus estudiantes con touch student_info.sh en el bash
10. Le damos permisos de ejecucion chmod +x student_info.sh en el bash
11. agregamos el  shebang  #!/bin/bash
Nota: El shebang (#!) es una secuencia que se coloca al inicio de un script en sistemas Unix/Linux para indicar qué intérprete debe usarse para ejecutar el script.
12. Agregamos comentario # Info about my computer science students from students database en student_info.sh
13. Añadir echo -e "\n~~ My Computer Science Students ~~\n" en student_info.sh
14. Correr con ./student_info.sh en el bash
15. Agregamos la variable  PSQL para en el script usar la base de datosm escribimos en student_info.sh el texto PSQL="psql -X --username=freecodecamp --dbname=students --no-align --tuples-only -c"
16. Imprimimos un texto echo -e "\nFirst name, last name, and GPA of students with a 4.0 GPA:"
17. Consulta SELECT * FROM students;
18. Consulta SELECT first_name FROM students;
19. Consulta SELECT first_name, last_name, gpa FROM students;
20. Consulta condicionada con WHERE SELECT first_name, last_name, gpa FROM students WHERE gpa < 2.5;
21. Consulta condicionada con WHERE SELECT first_name, last_name, gpa FROM students WHERE gpa >= 3.8;
22. Consulta condicionada con WHERE  SELECT first_name, last_name, gpa FROM students WHERE gpa != 4.0;
23. Con esta linea imprimimos la consulta de sql echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE gpa = 4.0;")" y 
24. corremos en el bash
25. Agregamos otro texto echo -e "\nAll course names whose first letter is before 'D' in the alphabet:"
26. Consulta SELECT * FROM majors;
27. Consulta SELECT * FROM majors WHERE major = 'Game Design';
28. Consulta SELECT * FROM majors WHERE major != 'Game Design'; 
29. Consulta SELECT * FROM majors WHERE major > 'Game Design';
30. Consulta SELECT * FROM majors WHERE major >= 'Game Design';
31. Consulta SELECT * FROM majors WHERE major < 'G';
32. Agregar echo "$($PSQL "SELECT course FROM courses WHERE course < 'D'")" y 
33. Correr ./student_info.sh
34. Agregar echo -e "\nFirst name, last name, and GPA of students whose last name begins with an 'R' or after and have a GPA greater than 3.8 or less than 2.0:"
35. Consulta SELECT * FROM students; 
36. Consulta SELECT * FROM students WHERE last_name < 'M';
37. Consulta SELECT * FROM students WHERE last_name < 'M' OR gpa = 3.9;
38. Consulta SELECT * FROM students WHERE last_name < 'M' AND gpa = 3.9 OR gpa < 2.3;
39. Consulta SELECT * FROM students WHERE last_name < 'M' AND (gpa = 3.9 OR gpa < 2.3);
40. Consulta SELECT * FROM students WHERE last_name < 'M' AND (gpa = 3.9 OR gpa < 2.3);
41. Agregar echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE last_name >= 'R' AND (gpa > 3.8 OR gpa < 2.0)")"
42. Correr ./student_info.sh 
43. Agregar echo -e "\nLast name of students whose last name contains a case insensitive 'sa' or have an 'r' as the second to last letter:" 
44. Consulta SELECT * FROM courses;
45. Consulta SELECT * FROM courses WHERE course LIKE '_lgorithms';
46. Consulta SELECT * FROM courses WHERE course LIKE '%lgorithms';
47. Consulta SELECT * FROM courses WHERE course LIKE 'Web%'; 
48. Consulta SELECT * FROM courses WHERE course LIKE '_e%';
49. Consulta SELECT * FROM courses WHERE course LIKE '% %';
50. Consulta SELECT * FROM courses WHERE course NOT LIKE '% %';
51. Consulta SELECT * FROM courses WHERE course LIKE '%A%';
52. Consulta SELECT * FROM courses WHERE course ILIKE '%A%';
53. Consulta SELECT * FROM courses WHERE course NOT ILIKE '%A%';
54. Consulta SELECT * FROM courses WHERE course NOT ILIKE '%A%' AND course LIKE '% %';
55. Agregar echo "$($PSQL "SELECT * FROM courses WHERE last_name ILIKE '%sa%' OR last_name LIKE %r_")"
56. Correr ./student_info.sh
57. Agregar echo -e "\nFirst name, last name, and GPA of students who have not selected a major and either their first name begins with 'D' or they have a GPA greater than 3.0:"
58. Consulta SELECT * FROM students;
59. Consulta SELECT * FROM students WHERE gpa IS NULL;
60. Consulta SELECT * FROM students WHERE gpa IS NOT NULL;
61. Consulta SELECT * FROM students WHERE major_id IS NULL;
62. Consulta SELECT * FROM students WHERE major_id IS NULL AND gpa IS NOT NULL;
63. Consulta SELECT * FROM students WHERE major_id IS NULL AND gpa IS NULL; 
64. Agregar echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE major_id IS NULL AND (first_name LIKE 'D%' OR gpa > 3.0)")"
65. Agregar echo -e "\nCourse name of the first five courses, in reverse alphabetical order, that have an 'e' as the second letter or end with an 's':"
66. Consulta SELECT * FROM students ORDER BY gpa;
67. Consulta SELECT * FROM students ORDER BY gpa DESC;
68. Consulta SELECT * FROM students ORDER BY gpa DESC, first_name;
69. Consulta SELECT * FROM students ORDER BY gpa DESC, first_name LIMIT 10;
70. Consulta SELECT * FROM students WHERE gpa IS NOT NULL ORDER BY gpa DESC, first_name LIMIT 10;
71. Agregar echo "$($PSQL "SELECT course FROM courses WHERE course LIKE '_e%' OR course LIKE '%s' ORDER BY course DESC LIMIT 5")"
72. Correr ./student_info.sh
73. Agregar echo -e "\nAverage GPA of all students rounded to two decimal places:"
74. Consulta SELECT MIN(gpa) FROM students;
75. Consulta SELECT MAX(gpa) FROM students;
76. Consulta SELECT SUM(major_id) FROM students;
77. Consulta SELECT AVG(major_id) FROM students;
78. Consulta SELECT CEIL(AVG(major_id)) FROM students;
79. Consulta SELECT ROUND(AVG(major_id)) FROM students;
80. Consulta SELECT ROUND(AVG(major_id), 5) FROM students;
81. Agregar echo "$($PSQL "SELECT ROUND(AVG(gpa), 2) FROM students")"
82. Correr ./student_info.sh
83. Agregar echo -e "\nMajor ID, total number of students in a column named 'number_of_students', and average GPA rounded to two decimal places in a column name 'average_gpa', for each major ID in the students table having a student count greater than 1:"
84. Consulta SELECT COUNT(*) FROM majors;
85. Consulta SELECT COUNT(*) FROM students;
86. Consulta SELECT COUNT(major_id) FROM students;
87. Consulta SELECT DISTINCT(major_id) FROM students;
88. Consulta SELECT major_id FROM students GROUP BY major_id;
89. Consulta SELECT major_id, COUNT(*) FROM students GROUP BY major_id;
90. Consulta SELECT major_id, MIN(gpa) FROM students GROUP BY major_id;
91. Consulta SELECT major_id, MIN(gpa), MAX(gpa) FROM students GROUP BY major_id;
92. Consulta SELECT major_id, MIN(gpa), MAX(gpa) FROM students GROUP BY major_id HAVING MAX(gpa) = 4.0;
93. Consulta SELECT major_id, MIN(gpa) AS min_gpa, MAX(gpa) FROM students GROUP BY major_id HAVING MAX(gpa) = 4.0;
94. Consulta SELECT major_id, MIN(gpa) AS min_gpa, MAX(gpa) AS max_gpa FROM students GROUP BY major_id HAVING MAX(gpa) = 4.0;
95. Consulta SELECT major_id, COUNT(*) AS number_of_students FROM students GROUP BY major_id;
96. Consulta SELECT major_id, COUNT(*) AS number_of_students FROM students GROUP BY major_id HAVING COUNT(*) < 8;
97. Añadir echo "$($PSQL "SELECT major_id, COUNT(*) AS number_of_students, ROUND(AVG(gpa),2) AS average_gpa FROM students GROUP BY major_id HAVING COUNT(*) > 1")"
98. Correr ./student_info.sh
99. Agregar echo -e "\nList of majors, in alphabetical order, that either no student is taking or has a student whose first name contains a case insensitive 'ma':"
100. Consulta SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;
101. Consulta SELECT * FROM students RIGHT JOIN majors ON students.major_id = majors.major_id;
102. Consulta SELECT * FROM students INNER JOIN majors ON students.major_id = majors.major_id;
103. Consulta SELECT * FROM majors LEFT JOIN students ON majors.major_id = students.major_id;
104. Consulta SELECT * FROM majors INNER JOIN students ON majors.major_id = students.major_id;
105. Consulta SELECT * FROM majors RIGHT JOIN students ON majors.major_id = students.major_id;
106. Consulta SELECT * FROM majors FULL JOIN students ON majors.major_id = students.major_id;
107. Consulta SELECT * FROM students INNER JOIN majors ON students.major_id = majors.major_id;
108. Consulta SELECT major FROM students INNER JOIN majors ON students.major_id = majors.major_id;
109. Consulta SELECT DISTINCT(major) FROM students INNER JOIN majors ON students.major_id = majors.major_id;
110. Consulta SELECT * FROM students RIGHT JOIN majors ON students.major_id = majors.major_id;
111. Cosulta SELECT * FROM students RIGHT JOIN majors ON students.major_id = majors.major_id WHERE student_id IS NULL;
112. Consulta SELECT major FROM students RIGHT JOIN majors ON students.major_id = majors.major_id WHERE student_id IS NULL;
113. Consulta SELECT * FROM students LEFT JOIN majors ON students.major_id = majors.major_id;
114. Consulta SELECT * FROM students LEFT JOIN majors ON students.major_id = majors.major_id WHERE major='Data Science' OR gpa >= 3.8;
115. Consulta SELECT first_name, last_name, major, gpa FROM students LEFT JOIN majors ON students.major_id = majors.major_id WHERE major='Data Science' OR gpa >= 3.8;
116. Consulta SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;
117. Consulta SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE first_name LIKE '%ri%' OR major LIKE '%ri%';
118. Consulta SELECT first_name, major FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE first_name LIKE '%ri%' OR major LIKE '%ri%';
119. Agregar echo "$($PSQL "SELECT major FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE major IS NOT NULL AND (student_id IS NULL OR first_name ILIKE '%ma%') ORDER BY major")"
120. Correr ./student_info.sh
121. Agregar echo -e "\nList of unique courses, in reverse alphabetical order, that no student or 'Obie Hilpert' is taking:"
122. Consulta SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;
123. Consulta SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;
124. Consulta SELECT students.major_id FROM students FULL JOIN majors AS m ON students.major_id = m.major_id;
125. Consulta SELECT s.major_id FROM students AS s FULL JOIN majors AS m ON s.major_id = m.major_id;
126. Consulta SELECT * FROM students FULL JOIN majors USING(major_id);
127. Consulta SELECT * FROM students FULL JOIN majors USING(major_id) FULL JOIN majors_courses USING(major_id);
128. Consulta SELECT * FROM students FULL JOIN majors USING(major_id) FULL JOIN majors_courses USING(major_id) FULL JOIN courses USING(course_id);
130. Agregar echo "$($PSQL "SELECT DISTINCT(course) FROM students RIGHT JOIN majors USING(major_id) INNER JOIN majors_courses USING(major_id) INNER JOIN courses USING(course_id) WHERE (first_name = 'Obie' AND last_name = 'Hilpert') OR student_id IS NULL ORDER BY course DESC")"
131. Correr ./student_info.sh
132. Agregar echo -e "\nList of courses, in alphabetical order, with only one student enrolled:"
133. Agregar SELECT COUNT(course), COURSE FROM students INNER JOIN majors USING(major_id) INNER JOIN majors_courses USING(major_id) INNER JOIN courses USING(course_id) GROUP BY course;
134. Correr ./student_info.sh


