# sql
sql
learning sql


create database students_details;

use students_details;

CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(50),
    gender VARCHAR(10),
    department VARCHAR(50),
    subject VARCHAR(50),
    marks INT,
    exam_date DATe);
    
    select*from students;
    
INSERT INTO students (student_name, gender, department, subject, marks, exam_date) 
VALUES
('Aarav', 'Male', 'Computer Science', 'DBMS', 85, '2024-03-01'),
('Ananya', 'Female', 'Computer Science', 'DBMS', 92, '2024-03-01'),
('Rahul', 'Male', 'Electronics', 'Circuits', 78, '2024-03-02'),
('Priya', 'Female', 'Electronics', 'Circuits', 88, '2024-03-02'),
('Karthik', 'Male', 'Mechanical', 'Thermodynamics', 74, '2024-03-03'),
('Sneha', 'Female', 'Mechanical', 'Thermodynamics', 81, '2024-03-03'),
('Vikram', 'Male', 'Computer Science', 'Data Structures', 90, '2024-03-04'),
('Neha', 'Female', 'Computer Science', 'Data Structures', 95, '2024-03-04'),
('Rohit', 'Male', 'Mechanical', 'Manufacturing', 69, '2024-03-05'),
('Pooja', 'Female', 'Electronics', 'Signals', 84, '2024-03-05'),
('Suresh', 'Male', 'Computer Science', 'Operating Systems', 76, '2024-03-06'),
('Divya', 'Female', 'Computer Science', 'Operating Systems', 89, '2024-03-06'),
('Arjun', 'Male', 'Electronics', 'Microprocessors', 72, '2024-03-07'),
('Meena', 'Female', 'Electronics', 'Microprocessors', 91, '2024-03-07'),
('Nikhil', 'Male', 'Mechanical', 'Fluid Mechanics', 68, '2024-03-08'),
('Kavya', 'Female', 'Mechanical', 'Fluid Mechanics', 86, '2024-03-08'),
('Manoj', 'Male', 'Computer Science', 'Computer Networks', 80, '2024-03-09'),
('Ritika', 'Female', 'Computer Science', 'Computer Networks', 94, '2024-03-09'),
('Harsha', 'Male', 'Electronics', 'Digital Electronics', 77, '2024-03-10'),
('Swathi', 'Female', 'Electronics', 'Digital Electronics', 88, '2024-03-10'),
('Amit', 'Male', 'Mechanical', 'Machine Design', 73, '2024-03-11'),
('Bhavya', 'Female', 'Mechanical', 'Machine Design', 90, '2024-03-11'),
('Sahil', 'Male', 'Computer Science', 'Python Programming', 82, '2024-03-12'),
('Ishita', 'Female', 'Computer Science', 'Python Programming', 96, '2024-03-12'),
('Ramesh', 'Male', 'Electronics', 'Control Systems', 71, '2024-03-13'),
('Latha', 'Female', 'Electronics', 'Control Systems', 87, '2024-03-13'),
('Deepak', 'Male', 'Mechanical', 'Heat Transfer', 75, '2024-03-14'),
('Aishwarya', 'Female', 'Mechanical', 'Heat Transfer', 89, '2024-03-14'),
('Varun', 'Male', 'Computer Science', 'Software Engineering', 84, '2024-03-15'),
('Nandini', 'Female', 'Computer Science', 'Software Engineering', 93, '2024-03-15'),
('Ajay', 'Male', 'Electronics', 'VLSI', 70, '2024-03-16'),
('Keerthi', 'Female', 'Electronics', 'VLSI', 88, '2024-03-16'),
('Sandeep', 'Male', 'Mechanical', 'Metallurgy', 66, '2024-03-17'),
('Pallavi', 'Female', 'Mechanical', 'Metallurgy', 85, '2024-03-17'),
('Yash', 'Male', 'Computer Science', 'AI Basics', 91, '2024-03-18'),
('Shreya', 'Female', 'Computer Science', 'AI Basics', 97, '2024-03-18'),
('Kiran', 'Male', 'Electronics', 'Embedded Systems', 74, '2024-03-19'),
('Riya', 'Female', 'Electronics', 'Embedded Systems', 90, '2024-03-19'),
('Venu', 'Male', 'Mechanical', 'Robotics', 79, '2024-03-20'),
('Anu', 'Female', 'Mechanical', 'Robotics', 88, '2024-03-20'),
('Mohit', 'Male', 'Computer Science', 'SQL', 86, '2024-03-21'),
('Pavani', 'Female', 'Computer Science', 'SQL', 94, '2024-03-21'),
('Gopal', 'Male', 'Electronics', 'Power Systems', 72, '2024-03-22'),
('Lakshmi', 'Female', 'Electronics', 'Power Systems', 89, '2024-03-22'),
('Tejas', 'Male', 'Mechanical', 'Automobile Engineering', 76, '2024-03-23'),
('Renu', 'Female', 'Mechanical', 'Automobile Engineering', 91, '2024-03-23');

select*from students;


select * from students
where marks<=35;

select 
subject, 
avg(marks) as avarage_marks
from students
group by subject
order by subject desc;

-- Average marks per department

select department, avg(marks)
from students
group by department;


-- Top-performing students (marks > 85)

select student_id,
student_name,
department,
subject,marks
from students 
where marks>=85
order by marks desc;

-- Top-performing student

select * from 
students 
where marks>=90
order by marks desc
limit 1;


select subject, AVG(marks) AS average_marks
FROM students
GROUP BY subject
HAVING AVG(marks) >= 75;

select department, 
count(*) as total_students
from students
group by department;


select department,
count(*) as merit_students 
from students
where marks>=97
group by department;

select department,
count(*) as numberof_students
from students
group by department
having count(*)>5;


select
department,
count(CASE WHEN marks >= 35 THEN 1 END) * 100.0 / count(*) as pass_percentage
from students
group by department
having count(*) > 5;

use students_details;

delimiter $$

create procedure department_wise_marks()
begin
     select*from students
     order by student_name;
  end $$
  
  call department_wise_marks;
  
  DROP PROCEDURE IF EXISTS department_wise_marks;

delimiter $$
create procedure department_wise_marks( 
in p_student_id int,
in p_studen_name varchar(99))
begin
select *from students
where student_id=student_id and student_name=student_name;
end $$
delimiter;

DELIMITER $$

CREATE PROCEDURE department_wise_marks(
    IN p_student_id INT,
    IN p_student_name VARCHAR(99)
)
BEGIN
    SELECT *
    FROM students
    WHERE student_id = p_student_id
      AND student_name = p_student_name;
END $$

DELIMITER ;
 
call department_wise_marks;

CALL department_wise_marks(1, 'Amit');


DELIMITER $$

DROP PROCEDURE IF EXISTS student_summary;

CREATE PROCEDURE student_summary(
    IN p_student_id INT,
    IN p_student_name VARCHAR(99)
)
BEGIN
    SELECT 
        student_id,
        student_name,
        department,
        COUNT(subject) AS total_subjects,
        AVG(marks) AS average_marks,
        MAX(marks) AS highest_mark,
        MIN(marks) AS lowest_mark
    FROM students
    WHERE student_id = p_student_id
      AND student_name = p_student_name
    GROUP BY student_id, student_name, department;
END $$

DELIMITER ;


select*from students;

insert into students(student_name
,gender,
department,
subject,
marks,exam_date)
value 
('sathya','male','mechanical','materials',99,'2024-03-23');


delimiter $$

create procedure insert_into_students(
in p_department varchar(77),
in p_student_name varchar(99) )
begin
     insert into students(department,student_name)
     values(p_department,p_student_name);
    end $$
    
    delimiter $$
    
call insert_into_students('computer science','jessi');


call insert_into_students;

22:23:00	execute insert_into_students('mechanichal','yash')	Error Code: 1064. You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '('mechanichal','yash')' at line 1	0.0041 sec



22:36:37	alter procedure students_details() begin select department,student_name ,marks from students	Error Code: 1064. You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '() begin select department,student_name ,marks from students' at line 1	0.00035 sec



-- Source - https://stackoverflow.com/a
-- Posted by Suresh Kamrushi, modified by community. See post 'Timeline' for change history
-- Retrieved 2026-01-13, License - CC BY-SA 4.0

CREATE PROCEDURE simpleproc (IN name varchar(50),IN user_name varchar(50),IN branch varchar(50))
BEGIN
    insert into student (name,user_name,branch) values (name ,user_name,branch);
END


drop procedure if exists students_details;

delimiter $$
create procedure students_details(s_department varchar(99),
s_student_name varchar(88)
,marks int)
begin
insert into students(department,student_name,marks)
values(department,student_name,marks);
end $$


22:42:01	delimiter$$ create procedure students_details() begin select department,student_name,marks from students	Error Code: 1064. You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'delimiter$$ create procedure students_details() begin select department,student_' at line 1	0.00016 sec


call students_details('mechanical','latha',85);









22:57:34	call students_details('mechanical','latha',85), ('computer sceince','yish',66), ('mechanical','jessica',98)	Error Code: 1064. You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ', ('computer sceince','yish',66), ('mechanical','jessica',98)' at line 1	0.00022 sec
