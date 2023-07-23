## XSS

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
	- 
	- https://portswigger.net/web-security/cross-site-scripting/dom-based


## SQL Injections

## Private Keying/Key Management
## Authentication vs Authorization
## Cryptography - Encryption, private key vs public key, etc