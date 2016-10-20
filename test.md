Consider the following schema:  

Suppliers(__*sid*__: integer, sname: string, address: string)   
Parts(__*pid*__: integer, pname: string, color: string)   
Catalog(__*sid: integer, pid: integer*__, cost: real)  

__*Find the names of suppliers who supply a red part.*__  

RA&nbsp;&nbsp;&nbsp;**π<sub>sname</sub>(π<sub>sid</sub>((π<sub>pid</sub>σ<sub>color='red'</sub>Parts)⋈Catalog)⋈Suppliers)**

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S.sname          
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Suppliers S, Parts P, Catalog C   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE P.color=’red’ AND C.pid=P.pid AND C.sid=S.sid  
      
__*Find the sids of suppliers who supply some red or green part.*__

RA&nbsp;&nbsp;&nbsp;&nbsp;**π<sub>sid</sub>(π<sub>pid</sub>(σ<sub>color='red' V color='green'</sub>Parts)⋈Catalog)** 
      
SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT C.sid   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Catalog C, Parts P   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE (P.color = ‘red’ OR P.color = ‘green’)   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AND P.pid = C.pid

__*Find the sids of suppliers who supply some red part or are at 221 Packer Street.*__  

RA&nbsp;&nbsp;&nbsp;&nbsp;**ρ(R1,π<sub>sid</sub>((π<sub>pid</sub>σ<sub>color='red'</sub>Parts)⋈Catalog))**   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**ρ(R2,π<sub>sid</sub>σ<sub>address='221PackerStreet'</sub>Suppliers)**  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**R1∪R2**  

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Suppliers S  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S.address = ‘221 Packer street’  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;OR S.sid IN ( SELECT C.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Parts P, Catalog C  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE P.color=’red’ AND P.pid = C.pid )  


__*Find the sids of suppliers who supply some red part and some green part.*__  

RA&nbsp;&nbsp;&nbsp;&nbsp;**ρ(R1,π<sub>sid</sub>((π<sub>pid</sub>σ<sub>color='red'</sub>Parts)⋈Catalog))**   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**ρ(R2,π<sub>sid</sub>((π<sub>pid</sub>σ<sub>color='green'</sub>Parts)⋈Catalog))**     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**R1∩R2**  


SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT C.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Parts P, Catalog C  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE P.color = ‘red’ AND P.pid = C.pid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AND EXISTS ( SELECT P2.pid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Parts P2, Catalog C2  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE P2.color = ‘green’ AND C2.sid = C.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AND P2.pid = C2.pid )   

__*Find the sids of suppliers who supply every part.*__  


RA&nbsp;&nbsp;&nbsp;&nbsp;**(π<sub>sid,pid</sub>Catalog)/(π<sub>pid</sub>Parts)**  

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT C.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Catalog C  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE NOT EXISTS (SELECT P.pid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Parts P  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE NOT EXISTS (SELECT C1.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Catalog C1  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE C1.sid = C.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AND C1.pid = P.pid))  

__*Find the sids of suppliers who supply every red part.*__  

RA&nbsp;&nbsp;&nbsp;&nbsp;**(π<sub>sid,pid</sub>Catalog)/(π<sub>pid</sub>σ<sub>color='red'</sub>Parts)**  

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT C.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Catalog C  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE NOT EXISTS (SELECT P.pid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Parts P    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE P.color = 'red'  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AND (NOT EXISTS (SELECT C1.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Catalog C1  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE C1.sid = C.sid AND  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C1.pid = P.pid)))  

