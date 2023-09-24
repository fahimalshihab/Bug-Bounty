
<h2>Broken access control resulting from platform misconfiguration</h2>

Some applications enforce access controls at the platform layer. they do this by restricting access to specific URLs and HTTP methods based on the user's role. For example, an application might configure a rule as follows:
DENY: POST, /admin/deleteUser, managers

This rule denies access to the POST method on the URL /admin/deleteUser, for users in the managers group. Various things can go wrong in this situation, leading to access control bypasses.

Some application frameworks support various non-standard HTTP headers that can be used to override the URL in the original request, such as X-Original-URL and X-Rewrite-URL.
If a website uses rigorous front-end controls to restrict access based on the URL, but the application allows the URL to be overridden via a request header,
then it might be possible to bypass the access controls using a request like the following: 
<code>POST / HTTP/1.1
X-Original-URL: /admin/deleteUser
...</code>

<a href="https://portswigger.net/web-security/access-control/lab-url-based-access-control-can-be-circumvented">
Lab: URL-based access control can be circumvented</a>


  1.Try to load /admin and observe that you get blocked. Notice that the response is very plain, suggesting it may originate from a front-end system.
   
  2.Send the request to Burp Repeater. Change the URL in the request line to / and add the HTTP header X-Original-URL: /invalid. Observe that the application returns a "not found" response. 
    This indicates that the back-end system is processing the URL from the X-Original-URL header.
   
  3.Change the value of the X-Original-URL header to /admin. Observe that you can now access the admin page.
    
  4.To delete carlos, add ?username=carlos to the real query string, and change the X-Original-URL path to /admin/delete.


<i><b> An alternative attack relates to the HTTP method used in the request. The front-end controls described in the previous sections restrict access based on the URL and HTTP method. Some websites tolerate different HTTP request methods when performing an action. If an attacker can use the GET (or another) method to perform actions on a restricted URL, they can bypass the access control that is implemented at the platform layer.</b> </i> 
