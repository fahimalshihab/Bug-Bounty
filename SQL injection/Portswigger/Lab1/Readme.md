Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.
 <pre> 
<b>Solution</b>
1.Use Burp Suite to intercept and modify the request that sets the product category filter.
2.Modify the category parameter, giving it the value '+OR+1=1--
3.Submit the request, and verify that the response now contains one or more unreleased products.</pre>

![l1](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/16a67fd5-fd98-4295-ac40-8a17be421caa)
