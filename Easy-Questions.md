Link to ERM: https://sqlzoo.net/wiki/File:Helpdesk.png

###1. There are three issues that include the words "index" and "Oracle". Find the call_date for each of them


```SQL
SELECT call_date, call_ref FROM Issue
WHERE Detail LIKE '%Oracle%' AND Detail Like '%index%'
```
###2. Samantha Hall made three calls on 2017-08-14. Show the date and time for each

```SQL
SELECT call_date, first_name, last_name FROM Issue
NATURAL JOIN Caller
WHERE First_name = 'Samantha' AND Last_name = 'Hall' AND Date(call_date) = '2017-08-14'
```
###3.There are 500 calls in the system (roughly). Write a query that shows the number that have each status.

```SQL
SELECT Status, COUNT(*) As Volume FROM Issue
GROUP BY Status
```
###4. Calls are not normally assigned to a manager but it does happen. How many calls have been assigned to staff who are at Manager Level?
```SQL
SELECT COUNT(*) as mlcc FROM Issue
JOIN
(SELECT Staff_code FROM Staff
WHERE Level_Code >3) AS t1
ON t1.Staff_code = Issue.Assigned_to
```

###5.Show the manager for each shift. Your output should include the shift date and type; also the first and last name of the manager.
```SQL
SELECT Shift_date, Shift_type, first_name, last_name FROM Shift
JOIN Staff ON Manager = Staff_code
```
