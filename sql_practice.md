__*Consider the following schema*__  

Student(__snum: integer__, sname: string, major: string, level: string, age: integer)  
Class(__name: string__, meets_at: time, room: string, fid: integer)  
Enrolled(snum: integer, __cname: string__)  
Faculty(__fid: integer__, fname: string, deptid: integer)  

** Find the names of all Juniors (level = JR) who are enrolled in a class taught by I. Teach. **  

SELECT DISTINCT S.Sname  
FROM Student S, Class C, Enrolled E, Faculty F  
WHERE S.snum = E.snum AND E.cname = C.name AND C.ﬁd = F.ﬁd AND F.fname = ‘I.Teach’ AND S.level = ‘JR’  

__*Find the age of the oldest student who is either a History major or enrolled in a course taught by I.Teach*__  

SELECT max(S.age)  
FROM Student S  
WHERE (S.major = 'History')  
OR S.snum IN (SELECT E.snum   
FROM Class C, Enrolled E, Faculty F  
WHERE E.cname = C.name AND C.ﬁd = F.ﬁd AND F.fname = ‘I.Teach’)  

__*Find the names of all classes that either meet in room R128 or have ﬁve or more students enrolled*__  

SELECT C.name,    
FROM Class C  
WHERE C.room = 'R128'  
OR C.name IN (SELECT E.cname  
FROM Enrolled E  
GROUP BY E.cname  
HAVING COUNT(*) >=5)  

__*Find the names of all students who are enrolled in two classes that meet at the same time*__  

SELECT S.sname  
FROM Student S  
WHERE S.snum IN (SELECT E1.snum  
FROM Enrolled E1, Enrolled E2, Class C1, Class C2  
WHERE E1.snum = E2.snum AND E1.cname <> E2.cname  
AND E1.cname = C1.name  
AND E2.cname = C2.name  
AND C1.meets_at = C2.meets_at)  

__*Find the names of faculty members who teach in every room in which some class is taught*__  

SELECT DISTINCT F.fname  
FROM Faculty F  
WHERE NOT EXISTS (( SELECT *  
FROM Class C )  
EXCEPT (SELECT C1.room  
FROM Class C1  
WHERE C1.ﬁd = F.ﬁd))  

__*Find the names of faculty members for whom the combined enrollment of the courses that they teach is less than ﬁve*__  

SELECT DISTINCT F.fname  
FROM Faculty F  
WHERE 5 > (SELECT COUNT (E.snum)  
FROM Class C, Enrolled E  
WHERE C.name = E.cname AND C.ﬁd = F.ﬁd)  

__*For each level, print the level and the average age of students for that level*__  

SELECT S.level, AVG(S.age)  
FROM Student S GROUP BY S.level  
 
 __*For all levels except JR, print the level and the average age of students for that level*__  
 
SELECT S.level, AVG(S.age)  
FROM Student S  
WHERE S.level <> ‘JR’  
GROUP BY S.level 

__*For each faculty member that has taught classes only in room R128, print the faculty member’s name and the total number of classes she or he has taught*__

SELECT F.fname, COUNT(*) AS CourseCount  
FROM Faculty F, Class C  
WHERE F.ﬁd = C.ﬁd  
GROUP BY F.ﬁd, F.fname  
HAVING EVERY ( C.room = ‘R128’ )  

__*Find the names of students enrolled in the maximum number of classes*__  

SELECT DISTINCT S.sname  
FROM Student S  
WHERE S.snum IN (SELECT E.snum  
FROM Enrolled E  
GROUP BY E.snum  
HAVING COUNT (*) >= ALL (SELECT COUNT (*)  
FROM Enrolled E2  
GROUP BY E2.snum ))  





