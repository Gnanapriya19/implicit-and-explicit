SQL>Select * from customers;   
 
+----+----------+-----+-----------+----------+  
| ID | NAME     | AGE | ADDRESS   | SALARY   |  
+----+----------+-----+-----------+----------+  
|  1 | Ramesh   |  32 | Ahmedabad |  2000.00 |  
|  2 | Khilan   |  25 | Delhi     |  1500.00 |  
|  3 | kaushik  |  23 | Kota      |  2000.00 |  
|  4 | Chaitali |  25 | Mumbai    |  6500.00 |  
|  5 | Hardik   |  27 | Bhopal    |  8500.00 |  
|  6 | Komal    |  22 | MP        |  4500.00 |  
+----+----------+-----+-----------+----------+ 
 
SQL>DECLARE   
2	total_rows number(2);  
3	BEGIN  
4	UPDATE customers  
5	SET salary = salary + 500;  
6	IF sql%notfound THEN  
7	dbms_output.put_line('no customers selected');  
8	ELSIF sql%found THEN  
9	total_rows := sql%rowcount; 
10	dbms_output.put_line( total_rows || ' customers selected ');  
11	END IF;   
12	END;  Output: 
6 customers selected   
PL/SQL procedure successfully completed.  
SQL>Select * from customers;   
+----+----------+-----+-----------+----------+  
| ID | NAME     | AGE | ADDRESS   | SALARY   |  
+----+----------+-----+-----------+----------+  
|  1 | Ramesh   |  32 | Ahmedabad |  2500.00 |  
|  2 | Khilan   |  25 | Delhi     |  2000.00 |  
|  3 | kaushik  |  23 | Kota      |  2500.00 |  
|  4 | Chaitali |  25 | Mumbai    |  7000.00 |  
|  5 | Hardik   |  27 | Bhopal    |  9000.00 |  
|  6 | Komal    |  22 | MP        |  5000.00 |  
+----+----------+-----+-----------+----------+ 
2. Program to illustrate the concepts of explicit cursors &minua; 
SQL>DECLARE  
2	c_id customers.id%type;  
3	c_name customers.name%type;  
4	c_addr customers.address%type;  
5	CURSOR c_customers is  
6	SELECT id, name, address FROM customers;  
7	BEGIN  
8	OPEN c_customers;  
9	LOOP  
10	FETCH c_customers into c_id, c_name, c_addr;  
11	EXIT WHEN c_customers%notfound;  
   12cdbms_output.put_line(c_id || ' ' || c_name || ' ' || c_addr);  
13	END LOOP;  
14	CLOSE c_customers;  
15	END;  
/ 
