Lab: SQL injection UNION attack, finding a column containing text

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you first need to determine the number of columns returned by the query. You can do this using a technique you learned in a previous lab. The next step is to identify a column that is compatible with string data.

The lab will provide a random value that you need to make appear within the query results. To solve the lab, perform a SQL injection UNION attack that returns an additional row containing the value provided. This technique helps you determine which columns are compatible with string data.
ACCESS THE LAB
<pre>
  Solution

  GET /filter?category=Gifts'UNION+SELECT+NULL,'NT43fX',NULL-- HTTP/2
  
    Use Burp Suite to intercept and modify the request that sets the product category filter.

    Determine the number of columns that are being returned by the query. Verify that the query is returning three columns, using the following payload in the category parameter:
    '+UNION+SELECT+NULL,NULL,NULL--

    Try replacing each null with the random value provided by the lab, for example:
    '+UNION+SELECT+'NT43fX',NULL,NULL--
    If an error occurs, move on to the next null and try that instead.
</pre>

![lab4](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/8c4c5569-ecd4-4783-9562-6cb74bb631da)
