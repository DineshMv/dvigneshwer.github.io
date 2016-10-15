---
layout: post
title: "MySql tutorials"
date: 2016-10-02
---

# Installing MySql server in ubuntu

~~~~
su -
apt-get install mysql-server
service mysql status
mysql_secure_installation 
mysql_install_db
mysqladmin -u root -p version

~~~~

# Basic commands
~~~~
create database db_name;

show databases;

use db_name;

shows tables;

show columns in db_name;
~~~~

# Creating a table
~~~~
create table dummy1 (
    -> c1 int not null auto_increment,
    -> c2 varchar(100) not null,
    -> primary key (c1)
    -> );
~~~~

# Inserting, updating and selecting
~~~~
insert into dummy1 (c2) values ('viki'),('viki2'),('viki3');

select * from dummy1;

select * from dummy1 where c2='viki';

update dummy1 set c2='ram' where c1=2;

delete from dummy1 where c1=3;
~~~~

# Joining tables 
~~~~
create table dummy2 (
	-> c1 int not null auto_increment,
	-> c3 varchar(100),
	-> primary key (c1),
	-> foreign key (c1) references dummy1(c1)
	-> );

 insert into dummy2 (c3) values ('cook'),('run');

select concat (dummy1.c2, '(',dummy2.c3,')') as activity, dummy1.c1 from dummy2 join dummy1 on dummy1.c1 = dummy2.c1;
~~~~

# Download a big dataset

~~~~
wget https://launchpad.net/test-db/employees-db-1/1.0.6/+download/employees_db-full-1.0.6.tar.bz2

tar xjf employees_db-full-1.0.6.tar.bz2

cd employees_db
~~~~

# Lets hack

~~~~
source employees.sql

create user viki@localhost identified by 'empadminpass';

grant all privileges on employees.* to viki@localhost;

msql -u viki -p

use employees;

SELECT * FROM salaries WHERE emp_no=10001 ORDER BY from_date;

SELECT * FROM salaries WHERE emp_no=10001 ORDER BY from_date DESC LIMIT 5;

SELECT CONCAT(last_name, ', ', first_name) AS Name, gender AS Gender,  hire_date AS "Hire date" FROM employees ORDER BY birth_date, last_name DESC LIMIT 10;

SELECT CONCAT(last_name, ', ', first_name) AS Name, MAX(B.salary) AS "Max. salary" FROM employees A JOIN salaries B ON A.emp_no = B.emp_no WHERE A.emp_no IN (10001, 10002, 10003) GROUP BY A.emp_no;

SELECT CONCAT(last_name, ', ', first_name) AS Name, MIN(B.salary) AS "Min. salary" FROM employees A JOIN salaries B ON A.emp_no = B.emp_no WHERE A.emp_no IN (10001, 10002, 10003) GROUP BY A.emp_no;

SELECT CONCAT(last_name, ', ', first_name) AS Name, ROUND(AVG(B.salary), 2) AS "Avg. salary" FROM employees A JOIN salaries B ON A.emp_no = B.emp_no WHERE A.emp_no IN (10001, 10002, 10003) GROUP BY A.emp_no;
~~~~

# Sources

[https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-14-04 Installation]
[http://www.tecmint.com/learn-mysql-mariadb-for-beginners/ Tutorials]
