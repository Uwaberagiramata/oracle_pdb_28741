#oracle_pdb_28741

#Oracle Pluggable Database Project
- **Name:** Sheilla Uwabera Giramata  
- **Student ID:** 28741

## Task 1: Create a New Pluggable Database (PDB)
- **Database Name:** sh_pdb_28741  
- **Admin User:** sheilla_plsqlauca_28741  
- **Password:** (hidden for security)
  
  **SQL Command Used:**
```sql
CREATE PLUGGABLE DATABASE sh_pdb_28741
ADMIN USER sheilla_plsqlauca_28741 IDENTIFIED BY "Sheilla@28741"
FILE_NAME_CONVERT=('D:\APPS\COMPRESSED\ORADATA\ORCL\PDBSEED\', 
                   'D:\APPS\COMPRESSED\ORADATA\ORCL\sh_pdb_28741\');
```

-- Open PDB
```
ALTER PLUGGABLE DATABASE sh_pdb_28741 OPEN;
ALTER PLUGGABLE DATABASE sh_pdb_28741 SAVE STATE;
```

-- Connect to PDB
```
CONNECT sheilla_plsqlauca_28741/"Sheilla@28741"@192.168.56.1:1521/sh_pdb_28741;
```

-- Create table
```
CREATE TABLE course (
    id NUMBER PRIMARY KEY,
    name VARCHAR2(50),
    score NUMBER
);
```
**Task 2:** Create and Delete Another PDB

**Database Name:** sh_to_delete_pdb_28741
**Admin User:** sheilla_delete

**SQL Commands Used:**

-- Create PDB to delete
```
CREATE PLUGGABLE DATABASE sh_to_delete_pdb_28741
ADMIN USER sheilla_delete IDENTIFIED BY "Sheilla@28741"
FILE_NAME_CONVERT=('D:\APPS\COMPRESSED\ORADATA\ORCL\PDBSEED\', 
                   'D:\APPS\COMPRESSED\ORADATA\ORCL\sh_to_delete_pdb_28741\');
```
-- Open PDB
```
ALTER PLUGGABLE DATABASE sh_to_delete_pdb_28741 OPEN;
```
-- Close and drop PDB
```
ALTER PLUGGABLE DATABASE sh_to_delete_pdb_28741 CLOSE IMMEDIATE;
DROP PLUGGABLE DATABASE sh_to_delete_pdb_28741 INCLUDING DATAFILES;
```
**Task 3**
Task 3: Oracle Enterprise Manager (OEM)  
Overview  

In this task, I set up and examined Oracle Enterprise Manager (OEM) to monitor and manage my Oracle 21c database after creating my pluggable database (SH_PDB_28741). The goal was to check the database status, performance, and resource usage using OEM and SQL Developer.

**Steps Performed**

Verified database connection in SQL Developer

Connected successfully as:
sheilla_plsqlauca_28741@sh_pdb_28741

**Used the command:**
```
SHOW CON_NAME;
```
to confirm I was inside my pluggable database (SH_PDB_28741).

**Opened Oracle Enterprise Manager.**

Accessed OEM through:  
https://localhost:5500/em  

Logged in as:  

Username: sys  

Role: SYSDBA  

Container name: orcl  

Confirmed access to the main dashboard.  

Explored key OEM sections.  

Status tab: Verified uptime, instance status, and connected sessions.  

Performance tab: Viewed CPU and I/O usage graphs.  

Resources tab: Checked tablespaces, memory, and storage.  

SQL Monitor: Observed active SQL operations.  

**Issues Encountered and Solutions**
Issue	
1. “Cannot connect
**Cause**:invalid container name”	The container name was entered incorrectly during OEM login.
**Solution**:Rechecked available PDBs using SHOW PDBS; and used orcl as the container.

3. OEM login kept looping back to the sign-in page
   
   **Cause**:OEM was not properly initialized with HTTPS.
   
   **Solution**:Checked port configuration using: SELECT dbms_xdb_config.gethttpsport FROM dual; → verified it was set to 5500. Then accessed https://localhost:5500/em.
   
5. Invalid username/password error in SQL Developer
   
   **cause**:Incorrect role or service name used in the connection.
   
   **solution**:Recreated the connection with username: sheilla_plsqlauca_28741 and service name: sh_pdb_28741.
   
7. No response after signing in to OEM
   
   **cause**:Browser cache issue or Oracle service not fully started.
   
   **solution**:Restarted the Oracle Listener and database services using lsnrctl start and startup commands in SQL*Plus.
   
**Conclusion**

Task 3 demonstrated how Oracle Enterprise Manager can be used alongside SQL Developer to manage and monitor database performance, storage, and user activities. Despite several connection and configuration issues, all problems were resolved, and the system is now fully functional.



