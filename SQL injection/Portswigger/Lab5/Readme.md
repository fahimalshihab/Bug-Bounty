
<pre><h1>Lab: SQL injection attack, querying the database type and version on Oracle</h1>


This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

To solve the lab, display the database version string.
  
<h3>Hint</h3>

On Oracle databases, every SELECT statement must specify a table to select FROM. If your UNION SELECT attack does not query from a table, you will still need to include the FROM keyword followed by a valid table name.

There is a built-in table on Oracle called dual which you can use for this purpose. For example: UNION SELECT 'abc' FROM dual

For more information, see our SQL injection cheat sheet.
ACCESS THE LAB
  
<h2>Solution</h2>

    Use Burp Suite to intercept and modify the request that sets the product category filter.

    Determine the number of columns that are being returned by the query and which columns contain text data. Verify that the query is returning two columns, both of which contain text, using a payload like the following in the category parameter:
    '+UNION+SELECT+'abc','def'+FROM+dual--

    Use the following payload to display the database version:
    '+UNION+SELECT+BANNER,+NULL+FROM+v$version--
</pre>
