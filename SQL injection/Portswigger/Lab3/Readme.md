Lab: SQL injection UNION attack, determining the number of columns returned by the query


This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack.

To solve the lab, determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values. 
<pre>
   Solution
  
    <code>GET /filter?category=Corporate+gifts'+UNION+SELECT+null,null,null-- HTTP/2</code>

    Use Burp Suite to intercept and modify the request that sets the product category filter.
    Modify the category parameter, giving it the value '+UNION+SELECT+NULL--. Observe that an error occurs.

    Modify the category parameter to add an additional column containing a null value:
    '+UNION+SELECT+NULL,NULL--
    Continue adding null values until the error disappears and the response includes additional content containing the null values.


  
</pre>
  ![L3](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/cc197a77-40ea-41ad-b861-5b9c62cfbba1)
