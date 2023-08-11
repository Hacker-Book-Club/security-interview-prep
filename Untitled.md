# **OWASP Top 10**
## Broken Access Control
- 94% of applications were tested for forms of broken access control
- 3.81% incident rate - 318k occurrences
- 34 CWEs mapped to Broken Access Control had **more occurrences in apps than any other category**.
- Notable CWEs:
- 200 - exposure of sensitive information to an unauthorized actor
- 201 - insertion of sensitive information into sent data
- 352 - Cross-Site Request Forgery
### Description
- Access control enforces policies so that a user cannot act outside of their intended permissions. See [Authentication vs Authorization](Concepts.md#Authentication-vs-Authorization).
- Failure of this leads to **unauthorized information disclosure**, **modification**, **destruction** of data. - See C.I.A. Pillars of InfoSec.
#### **Common Vulnerabilities:**
- Violation of the principle of least privilege
	- Only give people what they need access to in order to do their jobs, nothing more and nothing less.
		- Be as impermissive as possible
- **Bypassing access control** checks by **modifying the URL**(parameter tampering or force browsing), internal application state, the html page, or using a tool(like burp or postman) to modify API requests.
- Permitting the **viewing or editing of another user's account** by providing their **unique ID (insecure direct object references)**
- Accessing **API with missing access controls** for POST, PUT, and DELETE.
- Escalation of privilege. Acting as a different user(with higher perms) that you are not currently legitimately logged into.(such as obtaining admin/root as a lower user)
- Metadata manipulation, replaying or tampering with a JSON Web Token(JWT) used for access control, a cookie or hidden field manipulated to elevate privileges or abuse JWT invalidation.
- CORS misconfig, allowing access from unauthorized/untrusted origins - potentially resulting in sensitive information disclosure.
### How to Prevent
Access control is effective when implements in trusted server-side code or server-less API, where an attacker cant modify access control checks and/or metadata.
- deny by default
- Implement strong access control mechanisms uniformly - do the same thing throughout the application. minimize Cross-Origin Resource Sharing(CORS) usage.
- Model access control should enforce and record ownership rather than allowing users to create/read/update/delete any record.
- Unique application limits should be enforced by domain security models based off of the business logic requirements.
- Disable web server directory listing and ensure that file metadata is not present in any web roots.
- Log access control failures, alert admins on repeated failures and when appropriate.
- Rate limit the API and controller access to further minimize hard from automated attacking tools.
- Stateful session identifiers should be invalidated on the server as soon as a user logs out. Stateless tokens like JWTs should be short-lived to minimized the opportunity for an attack.  
# **WebApp Penetration Testing**
 - Walkthrough
 - Situational
# **Insider Threat**
- principle of least privilege
# **Threat Modeling**
- how do
- methodology/practice
# **Security Automation**