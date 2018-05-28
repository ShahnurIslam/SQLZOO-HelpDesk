
Link to ERM: https://sqlzoo.net/wiki/File:Helpdesk.png

### 6. List the Company name and the number of calls for those companies with more than 18 calls.


```SQL
SELECT Company_Name, Count(*) as cc FROM Issue
NATURAL JOIN Caller
NATURAL JOIN Customer
GROUP BY 1
HAVING Count(*)>18
```
### 7. Find the callers who have never made a call. Show first name and last name

```SQL
SELECT First_name, Last_name FROM Caller C
LEFT JOIN Issue I ON C.Caller_id = I.Caller_ID
WHERE I.Caller_ID IS Null
```
### 8. For each customer show: Company name, contact name, number of calls where the number of calls is fewer than 5

```SQL
SELECT Status, COUNT(*) As Volume FROM Issue
GROUP BY Status
```
### 9. For each shift show the number of staff assigned. Beware that some roles may be NULL and that the same person might have been assigned to multiple roles (The roles are 'Manager', 'Operator', 'Engineer1', 'Engineer2').
```SQL
SELECT COUNT(*) as mlcc FROM Issue
JOIN
(SELECT Staff_code FROM Staff
WHERE Level_Code >3) AS t1
ON t1.Staff_code = Issue.Assigned_to
```

### 10.Caller 'Harry' claims that the operator who took his most recent call was abusive and insulting. Find out who took the call (full name) and when.
```SQL
SELECT First_name, Last_name FROM Staff
WHERE Staff_CODE =
(SELECT Taken_by FROM Caller
NATURAL JOIN Issue
WHERE First_name = 'Harry'
ORDER BY Call_date DESC
```
