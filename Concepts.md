## **XSS**

##### What is XSS
- XSS is a type of injection attack where malicious scripts are added to otherwise benign assets.
- This is widespread and even some of the largest tech companies have had XSS in their main products.
- Occurs where a web application takes user input without validation or encoding.
- Provides access to cookies, tokens, sensitive information, and can rewrite contents of pages (replace links)
##### How does this happen?
- Input data is not sanitized and is included in dynamic content sent to a user (Example: Little Bobby Tables XKCD Comic, Google's XSS Bug, MySpace's Samy Worm)
- Data is entered through an untrusted source, like a raw web request that is manipulated by the adversary
- JavaScript, HTML, Flash, any other browser executable code
##### Reflected XSS
- When injected scripts are REFLECTED on the target web server, sent in a response to the users, this is reflected XSS.
- This could be done in an error message, search results, or anything sent back to the user when a request is made.
- When a user clicks  a link in an email or on another website it can lead to a reflected XSS on the target user's box. 
- Anything reflected is now "trusted" by user browsers ad it has come from the legitimate server.
- Reflected XSS is also referred to as Non-Persistent or Type-I XSS (carried out through a single request/response cycle.)
##### Stored XSS
- Injections are permanently stored on a target server
- This could be in a database, a message on a forum, visitor log, comments, etc. - User input data 
- Referred to as Persistent or Type-II XSS
##### Blind Cross-site Scripting
- A form of stored/persistent XSS
- The payload is saved on the server and reflected back from the backend. 
- Ex: a attacker adds a malicious payload to a feedback form. The admin opens the form via the backend application. The payload is executed.
	- Usually requires deep knowledge and understanding of the tech stack to be successful or spray and pray with common popular payloads.
- Could use tools like XSS Hunter Express, XSStrike


##### Other Types
- DOM Based XSS
	- Called Type-0 XSS
	- Payloads execute by manipulating the DOM in the victim's browser via original client side scripts vs server side code
### Summary
- Reflected XSS uses malicious scripts from the current HTTP request
	- EX: `https://insecure-website.com/search?term=<script>/*+Bad+stuff+here...+*/</script>`
- Stored XSS uses malicious scripts stored in the server's assets
	- EX: https://portswigger.net/web-security/cross-site-scripting/stored
- DOM-based XSS uses client-side code after assets are loaded, manipulating the browser environment 
	- EX: 
	- https://portswigger.net/web-security/cross-site-scripting/dom-based


### Remediation 
- https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html

## SQL Injections

- When input data is not sanitized (and certain characters are not escaped) and a request accesses a database, a malicious actor can manipulate data and execute commands on the host.
#### Impact
	- Information that should not be displayed can be returned (cross tenant access)
	- data can be deleted
	- Integrity, Availability, and Confidentiality are all affected.
	- Compromises the underlying servers, backend, and can result in DoS.
	- Can result in a backdoor and long-term compromise
	- Regulatory fines and reputational damage
#### Detection & Prevention
	- Burp Suite
	- Manual testing
	- Agent based logging
	- Prepared Statements / Parameterized Queries
		- Ensure attackers cannot change what a query does w/ injection
	- https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html
	- https://www.kitploit.com/p/sql-injection-tools.html



## Private Keying/Key Management
### Rules/Practices for Effective Key Management
1. Key life cycle management (generation, distribution, destruction)
2. Key compromise, recovery, and zeroization
3. Key storage
4. Key agreement
- achieve consensus on cryptographic strategy for an organization, project, or application.
	- document and map all components processing and storing cryptographic secrets.
	- Not all data is created equal - Pick the right approach - Security objectives of an application must be considered
		- Some cryptographic functions are more computational expensive/slow than others.
		- Not one size fits all

## Authentication vs Authorization
#### Authentication / AuthN
- What is Authentication
	- Ensuring that someone is who they claim to be
	- Match a person's claimed identity against one or more authentication factors that are bound to that credential.
	- Secure auth
	- entication calls for a multi-factor approach.
		- Combine multiple factors from two or more categories.
	- Sub-factors | heuristics:
		- location - where you are
		- time - when are you trying to authenticate
		We usually alert on any strange behavior if possible. This requires establishing a set of **baseline behaviors** for users. 
	- Authentication Factors:
		- Something you know | Memory/Knowledge-based:
			- Pin, password, ID number, Challenge question/image
		- Something you have | Possession/Property-based:
			- Virtual card, certificates, access card, key, key fob, ubikey device(hardware tokens)
		- Something you are | Inherent factors or Biologically based
			- Iris scan, finger print, facial recognition, DNA test 
- Features of Authentication
	- Responds with a 'yes' or 'no' depending on the result of a request - does not expose PII
	- Fail securely - handle exceptions gracefully incase of failure. Create fault tolerant systems
	- It should be auditable with tamper proof logs - organizational operators should be able pull this information
	- Should not enable tracking, profiling, etc - outside of the requirements for authentication and auditability.
	- Reduce threats - guessing, eavesdropping, replay/manipulation of comms.
- references:
	- https://id4d.worldbank.org/guide/authentication-mechanisms
#### Authorization / AuthZ
- Process of granting an **authenticated** party permission to do something - access a resource
- Authorization is the function of policy definitions
 **Ex:** giving someone admin access to an application or permission to download a particular file from a server.
	- Sometimes referred to as access control or client privilege.
	- Authorization specifies what data you can access and what you can do with that data.
	- permissions are **privileges** (or rights) when it becomes assigned to someone.
	- The breath of what people have access/privileges to is scope - the confines of their access

- Examples:
	- Most modern multi-user OSes use - Role Based Access Control - RBAC
		- Verified identities to consumers
		- Checks that consumers have been **authorized** to access the resource.
		- Defined by an **authority** like corporate security teams (corpsec)


____