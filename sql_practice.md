__*Consider the following schema*__  

Student(__snum: integer__, sname: string, major: string, level: string, age: integer)  
Class(__name: string__, meets_at: time, room: string, fid: integer)  
Enrolled(snum: integer, __cname: string__)  
Faculty(__fid: integer__, fnarne: string, deptid: integer)  

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
FROM Class C, Enrolled E  
WHERE C.room = 'R128'  
OR 

