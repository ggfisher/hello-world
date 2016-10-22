__*Consider the following schema*__  

Student(__snum: integer__, sname: string, major: string, level: string, age: integer)  
Class(__name: string__, meets_at: time, room: string, fid: integer)  
Enrolled(snum: integer, __cname: string__)  
Faculty(__fid: integer__, fnarne: string, deptid: integer)  

** Find the names of all Juniors (level = JR) who are enrolled in a class taught by I. Teach. **  

SELECT DISTINCT S.Sname  
FROM Student S, Class C, Enrolled E, Faculty F  
WHERE S.snum = E.snum AND E.cname = C.name AND C.ﬁd = F.ﬁd AND F.fname = ‘I.Teach’ AND S.level = ‘JR’  



