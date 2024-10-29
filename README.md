# Learn-SQL-by-Building-a-Student-Database-Part-2
Se inicia con echo en Bash, luego se conecta a la base de datos y usa psql para listar y consultar tablas.

# Resumen
Este es un resumen de los pasos principales para conectar, consultar y automatizar información en PostgreSQL usando Bash y SQL. Primero, se inicia con el comando echo en Bash, luego se conecta a la base de datos y se ejecutan comandos básicos en psql para listar, seleccionar y manipular tablas. En un segundo paso, se crea y configura un script de Bash (student_info.sh) para obtener información sobre los estudiantes, integrando consultas SQL condicionales y agregadas que imprimen datos específicos, como el GPA y los cursos. Finalmente, se usan JOINs y filtros avanzados en SQL para extraer y visualizar datos complejos según diversas condiciones.

# Pasos

1. Escribir `echo hello` en la terminal bash $${\color{red}Red}$$
2. Conectarse a la base de datos con `--username=freecodecamp --dbname=postgres`
3. Listar con `/l` en el psql
4. Se divide la terminal y se conencta la base de datos estudiantes con el comando `psql -U postgres < students.sql`
5. Listamos students.sql con  /l em psql
6. Conectar a la base de datos students `\c students`
7. Mostrar la base de datos con `\d` en psql
8. .Mostamos solo students `\d students`
9. Vemos toda la tabla con `SELECT * FROM students;`
10. hacer un script para imprimir información sobre tus estudiantes con `touch student_info.sh` en el bash
11. Le damos permisos de ejecucion `chmod +x student_info.sh` en el bash
12. Agregamos el  shebang  #!/bin/bash
Nota: El shebang (#!) es una secuencia que se coloca al inicio de un script en sistemas Unix/Linux para indicar qué intérprete debe usarse para ejecutar el script.
13. Agregamos comentario `# Info about my computer science students from students database en student_info.sh`
14. Añadir `echo -e "\n~~ My Computer Science Students ~~\n"`en student_info.sh
15. Correr con `./student_info.sh` en el bash
16. Agregamos la variable  PSQL para en el script usar la base de datosm escribimos en student_info.sh el texto `PSQL="psql -X --username=freecodecamp --dbname=students --no-align --tuples-only -c"`
17. Imprimimos un texto echo -e "\nFirst name, last name, and GPA of students with a 4.0 GPA:"
18. Consulta `SELECT * FROM students;`
19. Consulta `SELECT first_name FROM students;`
20. Consulta `SELECT first_name, last_name, gpa FROM students;`
21. Consulta condicionada con WHERE `SELECT first_name, last_name, gpa FROM students WHERE gpa < 2.5;`
22. Consulta condicionada con WHERE `SELECT first_name, last_name, gpa FROM students WHERE gpa >= 3.8;`
23. Consulta condicionada con WHERE `SELECT first_name, last_name, gpa FROM students WHERE gpa != 4.0;`
24. Con esta linea imprimimos la consulta de sql `echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE gpa = 4.0;")"`y 
25. corremos en el bash `./student_info.sh`
26. Agregamos otro texto `echo -e "\nAll course names whose first letter is before 'D' in the alphabet:"`
27. Consulta `SELECT * FROM majors;`
28. Consulta `SELECT * FROM majors WHERE major = 'Game Design';`
29. Consulta `SELECT * FROM majors WHERE major != 'Game Design';`
30. Consulta `SELECT * FROM majors WHERE major > 'Game Design';`
31. Consulta `SELECT * FROM majors WHERE major >= 'Game Design';`
32. Consulta `SELECT * FROM majors WHERE major < 'G';`
33. Agregar `echo "$($PSQL "SELECT course FROM courses WHERE course < 'D'")"` y 
34. Correr `./student_info.sh`
35. Agregar echo -e "\nFirst name, last name, and GPA of students whose last name begins with an 'R' or after and have a GPA greater than 3.8 or less than 2.0:"
36. Consulta `SELECT * FROM students;`
37. Consulta `SELECT * FROM students WHERE last_name < 'M';`
38. Consulta `SELECT * FROM students WHERE last_name < 'M' OR gpa = 3.9;`
39. Consulta `SELECT * FROM students WHERE last_name < 'M' AND gpa = 3.9 OR gpa < 2.3;`
40. Consulta `SELECT * FROM students WHERE last_name < 'M' AND (gpa = 3.9 OR gpa < 2.3);`
41. Consulta `SELECT * FROM students WHERE last_name < 'M' AND (gpa = 3.9 OR gpa < 2.3);`
42. Agregar `echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE last_name >= 'R' AND (gpa > 3.8 OR gpa < 2.0)")"`
43. Correr `./student_info.sh`
44. Agregar `echo -e "\nLast name of students whose last name contains a case insensitive 'sa' or have an 'r' as the second to last letter:"`
45. Consulta `SELECT * FROM courses;`
46. Consulta `SELECT * FROM courses WHERE course LIKE '_lgorithms';`
47. Consulta `SELECT * FROM courses WHERE course LIKE '%lgorithms';`
48. Consulta `SELECT * FROM courses WHERE course LIKE 'Web%'; `
49. Consulta `SELECT * FROM courses WHERE course LIKE '_e%';`
50. Consulta `SELECT * FROM courses WHERE course LIKE '% %';`
51. Consulta `SELECT * FROM courses WHERE course NOT LIKE '% %';`
52. Consulta `SELECT * FROM courses WHERE course LIKE '%A%';`
53. Consulta `SELECT * FROM courses WHERE course ILIKE '%A%';`
55. Consulta `SELECT * FROM courses WHERE course NOT ILIKE '%A%' AND course LIKE '% %';
56. Agregar `echo "$($PSQL "SELECT * FROM courses WHERE last_name ILIKE '%sa%' OR last_name LIKE %r_")"`
57. Correr `./student_info.sh`
58. Agregar `echo -e "\nFirst name, last name, and GPA of students who have not selected a major and either their first name begins with 'D' or they have a GPA greater than 3.0:"`
59. Consulta `SELECT * FROM students;`
60. Consulta `SELECT * FROM students WHERE gpa IS NULL;`
61. Consulta `SELECT * FROM students WHERE gpa IS NOT NULL;`
62. Consulta `SELECT * FROM students WHERE major_id IS NULL;`
63. Consulta `SELECT * FROM students WHERE major_id IS NULL AND gpa IS NOT NULL;`
64. Consulta `SELECT * FROM students WHERE major_id IS NULL AND gpa IS NULL;`
65. Agregar `echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE major_id IS NULL AND (first_name LIKE 'D%' OR gpa > 3.0)")"`
66. Agregar `echo -e "\nCourse name of the first five courses, in reverse alphabetical order, that have an 'e' as the second letter or end with an 's':"`
67. Consulta `SELECT * FROM students ORDER BY gpa;`
68. Consulta `SELECT * FROM students ORDER BY gpa DESC;`
69. Consulta `SELECT * FROM students ORDER BY gpa DESC, first_name;`
70. Consulta `SELECT * FROM students ORDER BY gpa DESC, first_name LIMIT 10;`
71. Consulta `SELECT * FROM students WHERE gpa IS NOT NULL ORDER BY gpa DESC, first_name LIMIT 10;`
72. Agregar `echo "$($PSQL "SELECT course FROM courses WHERE course LIKE '_e%' OR course LIKE '%s' ORDER BY course DESC LIMIT 5")"`
73. Correr `./student_info.sh`
74. Agregar `echo -e "\nAverage GPA of all students rounded to two decimal places:"`
75. Consulta `SELECT MIN(gpa) FROM students;`
76. Consulta `SELECT MAX(gpa) FROM students;`
77. Consulta `SELECT SUM(major_id) FROM students;`
78. Consulta `SELECT AVG(major_id) FROM students;`
79. Consulta `SELECT CEIL(AVG(major_id)) FROM students;`
80. Consulta `SELECT ROUND(AVG(major_id)) FROM students;`
81. Consulta `SELECT ROUND(AVG(major_id), 5) FROM students;`
82. Agregar `echo "$($PSQL "SELECT ROUND(AVG(gpa), 2) FROM students")"`
83. Correr `./student_info.sh`
84. Agregar `echo -e "\nMajor ID, total number of students in a column named 'number_of_students', and average GPA rounded to two decimal places in a column name 'average_gpa', for each major ID in the students table having a student count greater than 1:"`
85. Consulta `SELECT COUNT(*) FROM majors;`
86. Consulta `SELECT COUNT(*) FROM students;`
87. Consulta `SELECT COUNT(major_id) FROM students;`
88. Consulta `SELECT DISTINCT(major_id) FROM students;`
89. Consulta `SELECT major_id FROM students GROUP BY major_id;`
90. Consulta `SELECT major_id, COUNT(*) FROM students GROUP BY major_id;`
91. Consulta `SELECT major_id, MIN(gpa) FROM students GROUP BY major_id;
92. Consulta `SELECT major_id, MIN(gpa), MAX(gpa) FROM students GROUP BY major_id;`
93. Consulta `SELECT major_id, MIN(gpa), MAX(gpa) FROM students GROUP BY major_id HAVING MAX(gpa) = 4.0;`
94. Consulta `SELECT major_id, MIN(gpa) AS min_gpa, MAX(gpa) FROM students GROUP BY major_id HAVING MAX(gpa) = 4.0;`
95. Consulta `SELECT major_id, MIN(gpa) AS min_gpa, MAX(gpa) AS max_gpa FROM students GROUP BY major_id HAVING MAX(gpa) = 4.0;`
96. Consulta `SELECT major_id, COUNT(*) AS number_of_students FROM students GROUP BY major_id;`
97. Consulta `SELECT major_id, COUNT(*) AS number_of_students FROM students GROUP BY major_id HAVING COUNT(*) < 8;`
98. Añadir `echo "$($PSQL "SELECT major_id, COUNT(*) AS number_of_students, ROUND(AVG(gpa),2) AS average_gpa FROM students GROUP BY major_id HAVING COUNT(*) > 1")"`
99. Correr `./student_info.sh`
100. Agregar `echo -e "\nList of majors, in alphabetical order, that either no student is taking or has a student whose first name contains a case insensitive 'ma':"`
101. Consulta `SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;`
102. Consulta `SELECT * FROM students RIGHT JOIN majors ON students.major_id = majors.major_id;`
103. Consulta `SELECT * FROM students INNER JOIN majors ON students.major_id = majors.major_id;`
104. Consulta `SELECT * FROM majors LEFT JOIN students ON majors.major_id = students.major_id;`
105. Consulta `SELECT * FROM majors INNER JOIN students ON majors.major_id = students.major_id;`
106. Consulta `SELECT * FROM majors RIGHT JOIN students ON majors.major_id = students.major_id;`
107. Consulta `SELECT * FROM majors FULL JOIN students ON majors.major_id = students.major_id;`
108. Consulta `SELECT * FROM students INNER JOIN majors ON students.major_id = majors.major_id;`
109. Consulta `SELECT major FROM students INNER JOIN majors ON students.major_id = majors.major_id;`
110. Consulta `SELECT DISTINCT(major) FROM students INNER JOIN majors ON students.major_id = majors.major_id;`
111. Consulta `SELECT * FROM students RIGHT JOIN majors ON students.major_id = majors.major_id;`
112. Cosulta `SELECT * FROM students RIGHT JOIN majors ON students.major_id = majors.major_id WHERE student_id IS NULL;`
113. Consulta `SELECT major FROM students RIGHT JOIN majors ON students.major_id = majors.major_id WHERE student_id IS NULL;`
114. Consulta `SELECT * FROM students LEFT JOIN majors ON students.major_id = majors.major_id;`
115. Consulta `SELECT * FROM students LEFT JOIN majors ON students.major_id = majors.major_id WHERE major='Data Science' OR gpa >= 3.8;`
116. Consulta `SELECT first_name, last_name, major, gpa FROM students LEFT JOIN majors ON students.major_id = majors.major_id WHERE major='Data Science' OR gpa >= 3.8;`
117. Consulta `SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;`
118. Consulta `SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE first_name LIKE '%ri%' OR major LIKE '%ri%';`
119. Consulta `SELECT first_name, major FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE first_name LIKE '%ri%' OR major LIKE '%ri%';`
120. Agregar `echo "$($PSQL "SELECT major FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE major IS NOT NULL AND (student_id IS NULL OR first_name ILIKE '%ma%') ORDER BY major")"`
121. Correr `./student_info.sh`
122. Agregar `echo -e "\nList of unique courses, in reverse alphabetical order, that no student or 'Obie Hilpert' is taking:"`
123. `Consulta SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;`
124. `Consulta SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;`
125. `Consulta SELECT students.major_id FROM students FULL JOIN majors AS m ON students.major_id = m.major_id;`
126. `Consulta SELECT s.major_id FROM students AS s FULL JOIN majors AS m ON s.major_id = m.major_id;`
127. `Consulta SELECT * FROM students FULL JOIN majors USING(major_id);`
128. Consulta `SELECT * FROM students FULL JOIN majors USING(major_id) FULL JOIN majors_courses USING(major_id);`
129. Consulta `SELECT * FROM students FULL JOIN majors USING(major_id) FULL JOIN majors_courses USING(major_id) FULL JOIN courses USING(course_id);`
130. Agregar `echo `"$($PSQL "SELECT DISTINCT(course) FROM students RIGHT JOIN majors USING(major_id) INNER JOIN majors_courses USING(major_id) INNER JOIN courses USING(course_id) WHERE (first_name = 'Obie' AND last_name = 'Hilpert') OR student_id IS NULL ORDER BY course DESC")"`
131. Correr `./student_info.sh`
132. Agregar `echo -e "\nList of courses, in alphabetical order, with only one student enrolled:"`
133. Agregar `"$($PSQL "SELECT COUNT(course), COURSE FROM students INNER JOIN majors USING(major_id) INNER JOIN majors_courses USING(major_id) INNER JOIN courses USING(course_id) GROUP BY course;`
134. Correr `./student_info.sh`


