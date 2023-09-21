<pre>
1. User might be able to access the administrative functions by browsing to the relevant admin URL.
  
    /robots.txt
    /administrator-panel
    /admin
    
 2. In some cases, sensitive functionality is concealed by giving it a less predictable URL.
   This might not be directly guessable by an attacker. However, the application might still leak the URL to users.
   The URL might be disclosed in JavaScript that constructs the user interface based on the user's role:
  <h5>
  <script>
	var isAdmin = false;
	if (isAdmin) {
		...
		var adminPanelTag = document.createElement('a');
		adminPanelTag.setAttribute('https://insecure-website.com/administrator-panel-yb556');
		adminPanelTag.innerText = 'Admin panel';
		...
	}
</script></h5>


3.By Observeing that the response sets the cookie Admin=false. Change it to Admin=true. 
 
</pre>
