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

__*Find the sids of suppliers who supply some red part and some green part.*__  

RA&nbsp;&nbsp;&nbsp;&nbsp;**ρ(R1,π<sub>sid</sub>((π<sub>pid</sub>σ<sub>color='red'</sub>Parts)⋈Catalog))**   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**ρ(R2,π<sub>sid</sub>((π<sub>pid</sub>σ<sub>color='green'</sub>Parts)⋈Catalog))**     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**R1∩R2**  




