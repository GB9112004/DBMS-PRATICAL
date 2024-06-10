# DBMS-PRATICAL

use only single quotes.

conditin-then and end if;
loop-loop and end loop;

Simplifying complex queries: Views can simplify complex queries by hiding the underlying complexity and making it easier for users to access the data they need.
Improving data security: Views can be used to restrict access to sensitive data by only exposing a limited set of columns or rows to users.
Providing a layer of abstraction: Views can provide a layer of abstraction between the physical database structure and the user interface, making it easier to change the underlying database structure without affecting the users.

explicit assignmnet use :=
comparision =(also inside select assignmnent)
u can only return a value in function;

DROP VIEW NAME
DELETE FROM TB_NAME

TO CALCULATE EMPLOYEE_ID

The error is because you are trying to use a SQL statement (SELECT) directly in a PL/SQL block. In PL/SQL, you need to use a SELECT INTO statement to assign the result of a query to a variable.

Here is the corrected

using first select stat.
both if and else with ; at end


DECLARE
  incentive   NUMBER(8,2);
BEGIN
  SELECT salary * 0.12 INTO incentive
  FROM employees
  WHERE employee_id = 110;
  DBMS_OUTPUT.PUT_LINE('Incentive  = ' || TO_CHAR(incentive));
END;
/

3.DECLARE
new_salary number(10,4);

BEGIN
select salary into new_salary
from employee
where employee_id=122;

new_salary:=new_salary*(1+0.12);

UPDATE employee
SET salary = new_salary
where employee_id=122;

END
/;


4.CREATE OR REPLACE PROCEDURE not_null(p_value in number)
AS
v_result boolean;
BEGIN
if p_value>0 AND p_value<100 then
v_result:=true;
else
v_result:=false;
END IF;
  IF v_result THEN
    DBMS_OUTPUT.PUT_LINE('The value is not NULL and is between 1 and 99');
  ELSE
    DBMS_OUTPUT.PUT_LINE('The value is NULL or not between 1 and 99');
END IF;
END NOT_NULL;
/;


5..DECLARE
v_count number;
BEGIN
Select count(*) into v_count
from employee
where last_name like '%s%';
DBMS_OUTPUT.PUT_LINE('the number of persons is' || TO_CHAR(v_count));
END
/;


6..DECLARE
small number(8,2);
large number(8,2);

BEGIN
small:=10;
large:=20;
if small>large THEN
small := small + large;
large := small - large;
small := small - large;
END IF;

DBMS_OUTPUT.PUT_LINE('The smaller number is'|| TO_CHAR(small));
DBMS_OUTPUT.PUT_LINE('The large number is'|| TO_CHAR(large));

END
/;


9)DECLARE
emp_no number(10,2);
BEGIN
Select count(*) into emp_no
from employee
WHERE employee_id=50;

IF emp_no>45 THEN
DBMS_OUTPUT.PUT_LINE('THERE ARE VACCANIES');
else
DBMS_OUTPUT.PUT_LINE('THERE ARE NO VACCANIES');

END IF;
END
/; 


17.1)CREATE OR REPLACE FUNCTION factorial(p_num in number)
return number
as result number;
BEGIN
result:=1;
FOR i in 1..p_num
loop
result:=result*1;
end loop;
return result;
end
/;



TRIGGER
1.CREATE OR REPLACE TRIGGER prevent_parent_deletion
BEFORE DELETE ON departments
FOR EACH ROW
DECLARE
  v_count NUMBER;
BEGIN
  SELECT COUNT(*) INTO v_count FROM employees WHERE department_id = :OLD.department_id;

  IF v_count > 0 THEN
    RAISE_APPLICATION_ERROR(-20001, 'Cannot delete department with associated employees.');
  END IF;
END;
/


2.CREATE OR REPLACE TRIGGER check_duplicate_values
BEFORE INSERT OR UPDATE ON my_table
FOR EACH ROW
DECLARE
  v_count NUMBER;
BEGIN
  SELECT COUNT(*) INTO v_count FROM my_table WHERE my_column = :NEW.my_column AND rowid!= :NEW.rowid;

  IF v_count > 0 THEN
    RAISE_APPLICATION_ERROR(-20001, 'Duplicate value found in column my_column.');
  END IF;
END;
/

3.CREATE OR REPLACE TRIGGER restrict_insertion
BEFORE INSERT ON my_table
FOR EACH ROW
DECLARE
  v_total NUMBER;
BEGIN
  SELECT SUM(my_column) INTO v_total FROM my_table;

  IF v_total + :NEW.my_column > 1000 THEN
    RAISE_APPLICATION_ERROR(-20001, 'Total value of my_column exceeds threshold.');
  END IF;
END;
/


4.CREATE TABLE audit_log (
  table_name VARCHAR2(30),
  column_name VARCHAR2(30),
  old_value VARCHAR2(100),
  new_value VARCHAR2(100),
  timestamp DATE
);

CREATE OR REPLACE TRIGGER log_changes
BEFORE UPDATE OF salary, department_id ON employees
FOR EACH ROW
BEGIN
  INSERT INTO audit_log (table_name, column_name, old_value, new_value, timestamp)
  VALUES ('employees', 'alary', :OLD.salary, :NEW.salary, SYSTIMESTAMP);

  IF :OLD.department_id!= :NEW.department_id THEN
    INSERT INTO audit_log (table_name, column_name, old_value, new_value, timestamp)
    VALUES ('employees', 'department_id', :OLD.department_id, :NEW.department_id, SYSTIMESTAMP);
  END IF;
END;
/


5.CREATE TABLE audit_log (
  table_name VARCHAR2(30),
  operation VARCHAR2(10),
  username VARCHAR2(30),
  timestamp DATE
);

CREATE OR REPLACE TRIGGER log_user_activity
AFTER INSERT OR UPDATE OR DELETE ON employees, departments, jobs
DECLARE
  v_operation VARCHAR2(10);
BEGIN
  IF INSERTING THEN
    v_operation := 'INSERT';
  ELSIF UPDATING THEN
    v_operation := 'UPDATE';
  ELSIF DELETING THEN
    v_operation := 'DELETE';
  END IF;

  INSERT INTO audit_log (table_name, operation, username, timestamp)
  VALUES (SYS_CONTEXT('USERENV', 'CURRENT_SCHEMA'), v_operation, SYS_CONTEXT('USERENV', 'SESSION_USER'), SYSTIMESTAMP);
END;
/


VIEWS

CREATE OR REPLACE VIEW view_d_songs AS
SELECT ID AS "Song ID", title AS "Song Title", artist AS "Artist Name"
FROM DJs
WHERE id=1;


CREATE OR REPLACE VIEW EVENT AS
SELECT event_name as "EVENT_FOR",EVENT_DATE as "DYS"
from events
where event_date>=TRUNC(SYSDATE) AND event_date<=ADD_MONTHS(TRUNC(SYSDATE),3);

13.1.2)CREATE OR REPLACE VIEW copy_djs as
select * from DJS;

CREATE OR REPLACE VIEW read_copy_d_cds AS
SELECT * FROM copy_d_cds
WHERE release_year = 2000
WITH READ ONLY;


DELETE FROM read_copy_d_cds WHERE cd_number = 90;


CREATE OR REPLACE VIEW read_copy_d_cds WITH CHECK OPTION CONSTRAINT ck_read_copy_d_cds AS
SELECT * FROM copy_d_cds
WHERE release_year = 2000;

SELECT * FROM read_copy_d_cds;


SINGULARITY

The Singularity, in terms of computing, refers to a hypothetical future point in time at which artificial intelligence (AI) surpasses human intelligence, leading to exponential growth in technological advancements and potentially transforming human civilization beyond recognition.

MOORES LAW

Moore's Law, originally articulated by Intel co-founder Gordon Moore in 1965, predicts that the number of transistors on a microchip would double approximately every two years, leading to continuous improvements in computing power and efficiency. For several decades, this prediction held true and significantly drove advancements in technology.

CREATE VIEW view_copy_d_songs AS
SELECT title, artist
FROM copy_d_songs;

SELECT * FROM view_copy_d_songs;

DROP VIEW view_copy_d_songs;

SELECT * FROM view_copy_d_songs; -- This should raise an error because the view no longer exists.


MONGODB

db.restaurants.find().sort({
    "name": 1
})

db.restaurants.find({
    "grades.date": ISODate("2014-08-11T00:00:00Z"),
    "grades.grade": "A",
    "grades.score": 11
}, {
    "_id": 1,
    "name": 1,
    "grades": 1
})

db.restaurants.find({
    "grades.1.date": ISODate("2014-08-11T00:00:00Z"),
    "grades.1.grade": "A",
    "grades.1.score": 9
}, {
    "_id": 1,
    "name": 1,
    "grades": 1
})

db.restaurants.find({
    "address.coordinates.1": {
        $gte: 42,
        $lte: 52
    }
}, {
    "_id": 1,
    "name": 1,
    "address": 1,
    "location": 1
})


db.restaurants.find().sort({ "name": -1 })

db.restaurants.find().sort({ "cuisine": 1, "borough": -1 })

db.restaurants.find({ "address.street": { $exists: true } }).count()


db.restaurants.find({ "coord": { $type: 1 } })

db.restaurants.find({ "grades.score": { $mod: [7, 0] } }, { "_id": 1, "name": 1, "grades": 1 })

db.restaurants.find({ "name": { $regex: /mon/i } }, { "name": 1, "borough": 1, "coord": 1, "cuisine": 1 })

db.restaurants.find({ "name": { $regex: /^Mad/i } }, { "name": 1, "borough": 1, "coord": 1, "cuisine": 1 })

db.restaurants.find({ "grades.score": { $lt: 5 } })


db.restaurants.find({ "borough": "Manhattan", "grades.score": { $lt: 5 } })

db.restaurants.find({ $or: [ { "borough": "Manhattan" }, { "borough": "Brooklyn" } ], "grades.score": { $lt: 5 } })

db.restaurants.find({ $or: [ { "borough": "Manhattan" }, { "borough": "Brooklyn" } ], "grades.score": { $lt: 5 }, "cuisine": { $ne: "American" } })

db.restaurants.find({ $or: [ { "borough": "Manhattan" }, { "borough": "Brooklyn" } ], "grades.score": { $lt: 5 }, "cuisine": { $nin: ["American", "Chinese"] } })

db.restaurants.find({ $and: [ { "grades.score": 2 }, { "grades.score": 6 } ] })

db.restaurants.find({ $and: [ { "grades.score": 2 }, { "grades.score": 6 }, { "borough": "Manhattan" } ] })


create table emp_details(
    emp_no number(10),
    emp_name varchar(10),
    DOB DATE,
    address varchar(10)
);

insert into emp_details values(1,'AVV','10/12/23','chennai');
