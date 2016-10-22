__*Consider the following schema*__  

Student(snum: integer, sname: string, major: string, level: string, age: integer)  
Class(name: string, meets_at: time, room: string, fid: integer)  
Enrolled(snum: integer, cname: string)  
Faculty(fid: integer, fnarne: string, deptid: integer)  

** Find the names of all Juniors (level = JR) who are enrolled in a class taught by I. Teach. **  

