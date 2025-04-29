Upload your SQL code files here.

CREATE TABLE course (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    teacher_id INT,
    FOREIGN KEY (teacher_id) REFERENCES teacher(id)
);

CREATE TABLE student (
    id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);

CREATE TABLE student_course (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id),
    FOREIGN KEY (student_id) REFERENCES student(id),
    FOREIGN KEY (course_id) REFERENCES course(id)
);

INSERT INTO teacher (id, first_name, last_name) VALUES
(1, 'Taylah', 'Booker'),
(2, 'Sarah-Louise', 'Blake');

INSERT INTO course (id, name, teacher_id) VALUES
(1, 'Database design', 1),
(2, 'English literature', 2),
(3, 'Python programming', 1);

INSERT INTO student (id, first_name, last_name) VALUES
(1, 'Shreya', 'Bain'),
(2, 'Rianna', 'Foster'),
(3, 'Yosef', 'Naylor');

INSERT INTO student_course (student_id, course_id) VALUES
(1, 2),
(1, 3),
(2, 1),
(2, 2),
(2, 3),
(3, 1);

SELECT 
    s.id AS student_id,
    s.first_name AS student_first_name,
    s.last_name AS student_last_name,
    c.name AS course_name,
    t.first_name AS teacher_first_name,
    t.last_name AS teacher_last_name
FROM student_course sc
JOIN student s ON sc.student_id = s.id
JOIN course c ON sc.course_id = c.id
JOIN teacher t ON c.teacher_id = t.id;
