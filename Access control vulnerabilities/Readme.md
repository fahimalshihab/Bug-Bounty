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


3. Parameter-based access control methods
   Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location. This could 
   be:

  A hidden field.
  A cookie.
  A preset query string parameter.
  The application makes access control decisions based on the submitted value.

4. https://insecure-website.com/login/home.jsp?admin=true
   https://insecure-website.com/login/home.jsp?role=1
   This approach is insecure because a user can modify the value and access functionality they're not authorized to, such as administrative functions.

5. Horizontal privilege escalation occurs if a user is able to gain access to resources belonging to another user, instead of their own resources of 
   that type. For example, if an employee can access the records of other employees as well as their own, then this is horizontal privilege escalation.
   Horizontal privilege escalation attacks may use similar types of exploit methods to vertical privilege escalation. For example, a user might access 
   their own account page using the following URL:
   https://insecure-website.com/myaccount?id=123
   If an attacker modifies the id parameter value to that of another user, they might gain access to another user's account page, and the associated 
   data and functions.<h5>Note This is an example of an insecure direct object reference (IDOR) vulnerability. This type of vulnerability arises where user-controller parameter values are used to access resources or functions directly.</h5>
In some applications, the exploitable parameter does not have a predictable value. For example, instead of an incrementing number, an application might use globally unique identifiers (GUIDs) to identify users. This may prevent an attacker from guessing or predicting another user's identifier. However, the GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced, such as user messages or reviews.
such as for carlos GIUD = 615e4372-9f69-4878-a133-ac5cf46ff84f & for wiener GUID = 0938d105-690f-4aac-9f94-1b554cddf910
  
</pre>
