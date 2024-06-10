# DBMS-PRATICAL

use only single quotes.

explicit assignmnet use :=
comparision =(also inside select assignmnent)
u can only return a value in function;

TO CALCULATE EMPLOYEE_ID

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
