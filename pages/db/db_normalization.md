---
layout: post
title: Database Normalization
subtitle: normalization
author: cloudjk
tags: [database, db, normalization]
---

[Normalization](https://beginnersbook.com/2015/05/normalization-in-dbms/)

> ### The purpose of Normalization

1. Eliminate unnecessary data redundancy
2. Prevent insertion, update, deletion anomalies

| Emp_id | Emp_name | Emp_address  | Emp_dept |
| :----- | :------- | :----------- | :------- |
| 101    | Rick     | Chatswood    | D001     |
| 101    | Rick     | Epping       | D002     |
| 123    | Maggie   | North Sydney | D890     |
| 166    | Glenn    | Melbourne    | D900     |
| 166    | Glenn    | Melbourne    | D004     |

1. **Insertion anomaly** : Suppose a new employee joins the company, who is under training and currently not assigned to any department then we would not be able to insert the data into the table if Emp_dept field doesn’t allow nulls.
2. **Update anomaly** : In the above table we have two rows for employee Rick as he belongs to two departments of the company. If we want to update the address of Rick then we have to update the same in two rows or the data will become inconsistent. If somehow, the correct address gets updated in one department but not in other then as per the database, Rick would be having two different addresses, which is not correct and would lead to inconsistent data.
3. **Delete anomaly** : Suppose, if at a point of time the company closes the department D890 then deleting the rows that are having Emp_dept as D890 would also delete the information of employee Maggie since she is assigned only to this department.

> ### Super key & Candidate key & prime/non-prime attribue

1. **super key** : a set of one or more attributes which can **uniquely identify** a row in a table
2. **candidate key** : selected from the set of super keys where redundant attribute does not exist. (candiate for primary key)
3. **prime attribute** : an attribute that is part of any candidate key
4. **non-prime attribute** : an attribute that is not part of any candidate key

**[example]**

| Emp_ssn   | Emp_number | Emp_name  |
| :-------- | :--------- | :-------- |
| 123456789 | 226        | Steve     |
| 999999321 | 227        | Ajeet     |
| 888997212 | 228        | Chaitanya |
| 777778888 | 229        | Robert    |

-   super keys
    {Emp_ssn}, {Emp_number}, {Emp_ssn, Emp_number}, {Emp_ssn, Emp_name}, {Emp_number, Emp_name}, {Emp_ssn, Emp_number, Emp_name}
-   candidate keys
    {Emp_ssn}, {Emp_number}

> ### Transitive Functional Dependency

-   when non-prime attribute is transitively dependent on super key

> ### 1NF (First Normal Form) Rules

-   Each attribute of a table must have atomic values

**[BEFORE 1NF]**

| Emp_id | Emp_name | Emp_address | Emp_mobile             |
| :----- | :------- | :---------- | :--------------------- |
| 101    | Herschel | New Delhi   | 8912312390             |
| 102    | Jon      | Kanpur      | 8812121212, 9900012222 |
| 103    | Ron      | Chennai     | 7778881212             |
| 104    | Lester   | Bangalore   | 9990000123, 8123450987 |

**[AFTER 1NF]**

| Emp_id | Emp_name | Emp_address | Emp_mobile |
| :----- | :------- | :---------- | :--------- |
| 101    | Herschel | New Delhi   | 8912312390 |
| 102    | Jon      | Kanpur      | 8812121212 |
| 102    | Jon      | Kanpur      | 9900012222 |
| 103    | Ron      | Chennai     | 7778881212 |
| 104    | Lester   | Bangalore   | 9990000123 |
| 104    | Lester   | Bangalore   | 8123450987 |

> ### 2NF (Second Normal Form) Rules

-   Table must be in 1NF
-   No non-prime attribute is dependent on proper subset of any **candidate key** of a table

**[BEFORE 2NF]**

| Teacher_id | Subject   | Teacher_age |
| :--------- | :-------- | :---------- |
| 111        | Maths     | 38          |
| 111        | Physics   | 38          |
| 222        | Biology   | 38          |
| 333        | Physics   | 40          |
| 333        | Chemistry | 40          |

**[AFTER 2NF]**
non-prime attribute Teacher_age is dependent on Teacher_id which is a proper subset of candidate key

| Teacher_id | Teacher_age |
| :--------- | :---------- |
| 111        | 38          |
| 222        | 38          |
| 333        | 40          |

| Teacher_id | Subject   |
| :--------- | :-------- |
| 111        | Maths     |
| 111        | Physics   |
| 222        | Biology   |
| 333        | Physics   |
| 333        | Chemistry |

> ### 3NF (Third Normal Form) Rules

-   Table must be in 2NF
-   Transitive functional dependency of non-prime attritube on any **super keys** should be removed

**[BEFORE 3NF]**

| Emp_id | Emp_name | Emp_zip | Emp_state | Emp_city | Emp_district |
| :----- | :------- | :------ | :-------- | :------- | :----------- |
| 1101   | John     | 282005  | UP        | Agra     | Dayal Bagh   |
| 1102   | Ajeet    | 222008  | TN        | Chennai  | M-City       |
| 1106   | Lora     | 282007  | TN        | Chennai  | Urrapakkam   |
| 1101   | Lilly    | 292008  | UK        | Pauri    | Bhagwan      |
| 1201   | Steve    | 222999  | MP        | Gwalior  | Ratan        |

-   Super keys: {emp_id}, {emp_id, emp_name}, {emp_id, emp_name, emp_zip}…so on
-   Candidate Keys: {emp_id}
-   Non-prime attributes: all attributes except emp_id are non-prime as they are not part of any candidate keys.
-   Here, emp_state, emp_city & emp_district dependent on emp_zip. And, emp_zip is dependent on emp_id that makes non-prime attributes (emp_state, emp_city & emp_district) transitively dependent on super key (emp_id). This violates the rule of 3NF.
-   To make this table complies with 3NF we have to break the table into two tables to remove the transitive dependency:

**[AFTER 3NF]**

| Emp_id | Emp_name | Emp_zip |
| :----- | :------- | :------ |
| 1101   | John     | 282005  |
| 1102   | Ajeet    | 222008  |
| 1106   | Lora     | 282007  |
| 1101   | Lilly    | 292008  |
| 1201   | Steve    | 222999  |

| Emp_zip | Emp_state | Emp_city | Emp_district |
| :------ | :-------- | :------- | :----------- |
| 282005  | UP        | Agra     | Dayal Bagh   |
| 222008  | TN        | Chennai  | M-City       |
| 282007  | TN        | Chennai  | Urrapakkam   |
| 292008  | UK        | Pauri    | Bhagwan      |
| 222999  | MP        | Gwalior  | Ratan        |

> ### Boyce Codd normal form (BCNF)

1. Advanced version of 3NF(3.5NF)
2. X -> Y X should be the **super key** of the table

**[BEFORE BCNF]**

| Emp_id | Emp_nationality | Emp_dept                     | Dept_type | Dept_no_of_emp |
| :----- | :-------------- | :--------------------------- | :-------- | :------------- |
| 1101   | Austrian        | Production and Planning      | D001      | 200            |
| 1101   | Austrian        | Stores                       | D001      | 250            |
| 1102   | American        | Design and Technical support | D134      | 100            |
| 1102   | American        | Purchasing department        | D134      | 600            |

-   Emp_id and Emp_dept are a key
-   Dependencies : {emp_nationality} dependent on emp_id, {dept_type, dept_no_of_emp} dependent on emp_dept
-   It does not fulfill "X should be **super key**"

**[AFTER BCNF]**

| Emp_id | Emp_nationality |
| :----- | :-------------- |
| 1101   | Austrian        |
| 1102   | American        |

| Emp_dept                     | Dept_type | Dept_no_of_emp |
| :--------------------------- | :-------- | :------------- |
| Production and Planning      | D001      | 200            |
| Stores                       | D001      | 250            |
| Design and Technical support | D134      | 100            |
| Purchasing department        | D134      | 600            |

| Emp_id | Emp_dept                     |
| :----- | :--------------------------- |
| 1101   | Production and Planning      |
| 1101   | Stores                       |
| 1102   | Design and Technical support |
| 1102   | Purchasing department        |
