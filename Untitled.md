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
**- deny by default**
- Implement strong access control mechanisms **uniformly** - do the same thing throughout the application. minimize Cross-Origin Resource Sharing(CORS) usage.
- Model access control should enforce and record ownership rather than allowing users to create/read/update/delete any record.
- Unique application limits should be enforced by domain security models based off of the business logic requirements.
- Disable web server directory listing and ensure that file metadata is not present in any web roots.
- Log access control failures, alert admins on repeated failures and when appropriate.
- Rate limit the API and controller access to further minimize hard from automated attacking tools.
- Stateful session identifiers should be invalidated on the server as soon as a user logs out. Stateless tokens like JWTs should be short-lived to minimized the opportunity for an attack.  
# **WebApp Penetration Testing**
 - Walkthrough
	1. **Reconnaissance**
		* Gather as much information about the target system as possible
			* Topology of the network, OSes in use, Applications, user accounts, anything of relevance.
			* Helps effectively plan the attack strategy
		* Active vs passive recon
			* Passive pulls information from sources that are already publicly available.
			* Active recon involves directly interacting with target systems to gain information.
		
	2. **Scanning**
		* Uses various tools to identify open ports, check network traffic, vulns, etc.
		* Outside of pentesting this is called - vulnerability scanning
			* vuln scanning w/o pentesting - cannot determine if a potential threat is actionable.
	3. **Vulnerability assessment**
		* Uses all the data gathering in recon & scanning to identify potential vulnerabilities and see if they are exploitable.
		* NVD = National Vulnerability Database
		* CVE = Common Vulnerabilities and Exposures
		* CVSS = Common Vulnerability Scoring System
	1. **Exploitation**
		* Attempt to access the target system and exploit identified vulnerabilities.
			* Metaspolit, other tools, etc - help to emulate real-world attack scenarios
	1. **Reporting**
		* Prepares a report with findings, remediation, suggestions, etc.
		* Puts vulns into context so organization can act on the associated risks.
			* Business impact, cvss scores, explanation of the difficulty of exploitation, technical risk, remediative advice, strategic suggestions.
 - Situational
# **Insider Threat**
* Threats that originate with authorized users - employees, contractors, business partners, etc
### **Malicious Insiders**
* intentional or accidental misuse of their legit access - or account hijacking
	* Incidents re: insider threat cost 4.9m on average
* Disgruntled current/former employees who have access still.
	* Revenge, financial benefit, sometimes both.
	* May work for a malicious outsider
		* Hacker, competitor, nation-state actor
	* Leak customer info, disrupt business ops, plant malware, tamper w/ files/apps, leak intellectual property, trade secrets, other sensitive data.
### **Negligent Insiders** - 56% of insider threat events
- Do not have malicious intent but through ignorance or carelessness, they cause security threats. 
	- phishing, bypassing sec controls to save time, losing a laptop, emailing the wrong file to someone.
### **Compromised insiders**
- legit users who have had their credentials stolen by external actors.
- Threats launched via compromised insiders are the most expensive threats - 804,997 on average
- often the result of social engineering credential stuffing, negligent behavior, etc.
# **Threat Modeling**
### Description
- Threat modeling helps **identify**, **communicate**, and **understand** **threats and mitigations** within the context of **protecting an asset**.
- Threat models are a **structured representation** of **information affecting the security of an application**.
- A view of the **application** and its **environment** through the **lens of security**.
- Can be applied to software, applications, systems, networks, distributed systems, Internet of Things (IoT) devices, and businesses processes.
- A Threat model usually includes
	- **Descriptions** of the subject to be modeled
	- **Assumptions** that can be checked or challenged in the future as the threat landscape changes
	- Potential **threats** to the system
	- Actions that can be taken to **mitigate** each threat
	- A way to **validate** the model and threats, and verification of success of actions taken
- Threat Modeling is a process for capturing, organizing, and analyzing all this information. 
	- Applied to software - it enables informed decision-making about application security risks.
	- Produces a model and a **prioritized list** of security **improvements** to the concept, requirements, design, or implementation of an application.
### Objectives
- Threat modeling is a planned activity for **identifying** and **assessing** **application threats/vulnerabilities**
- Improving security by identifying threats
	- defining **countermeasures** to **prevent/mitigate** the effects of those **threats** to the system
- A threat is a potential or actual event that may be **malicious** (DoS) or **incidental** (Failure of a storage device)
### Threat Modeling Across the Lifecycle
It best to apply threat modeling mentality throughout all stages of software development lifecycles(SDLC).
- High-level threat model should be defined during initial planning phase.
	- This should then be refined throughout the lifecycle.
	- When more details are added to the system, it will expose new attack vectors.
	- Ongoing thread modeling should examine, diagnose, and address these threats.
- Updating the thread model should happen when:
	- A new feature is released
	- Security incident occurs
	- Architectural or infrastructure changes

### Four Question Framework
Threats exist when the likelihood of a threat occurring and its impact is significant. Use these questions to organize the threat model.
- What are we working on?
- What can go wrong?
- What are we going to do about it?
- Did we do a good job?

There are many methods/techniques to answering these questions.
 - using a structured model helps efficiency/consistency.

Don't boil the ocean - trying to combine every permutation of agent, attack, vuln, impact, etc - waste of time/effort. refine the search space.
- **Assess Scope** - What are we working on? (Small - sprint | Large - Whole system)
- **Identify what can go wrong** - brainstorm sesh, STRIDE, Kill Chains, or Attack Trees
- **Identify countermeasures or manage risk** - What are you going to do about each threat. Mitigation, risk acceptance/exception/transference.
- **Assess your work** - Did you do a good enough job for the system at hand?

### Structured Threat Modeling Process
**Benefits**
- Clear 'line of sight' across a project that justifies security efforts
- Allows security decisions to be made rationally w/ all the info on the table
- Produces an assurance argument.
	- explains and defends the security of an application
	- Starts w/ high level claims and justifies them with subclaims or evidence
#### **1. Decompose the Application**
1. Create **use cases** (business logic) to understand how the application is used
2. Identify **entry points** - where an attacker could interact with the application
3. Identify **levels of trust** - representing the privileges applications grant to external entities.
Use all this to produce **data flow diagrams** (DFDs) and a document in the Threat Model document.
- DFSs show the different paths through a system, highlighting **privilege boundaries**.

1. External dependencies
2. Entry points
3. Exit points
4. Assets
5. Trust Levels
6. Data Flow Diagrams
#### 2. Determine and Rank Threats
Use a threat categorization methodology - STRIDE or other [Application Security Frameworks](https://pathlock.com/learn/what-are-application-security-frameworks/)(ASF) that define categories like:
- Auditing & Logging, Authentication, Authorization, Configuration Management, Data Protection in Storage and Transit, Data Validation, and Exception Management.
The goal of threat categorization is to help identify threats from both the attacker [STRIDE](https://en.wikipedia.org/wiki/STRIDE_%28security%29)  and defensive perspective.
- Use the DFDs produced in step 1 to help identify targets from the attacker's perspective
	- like data sources
	- processes
	- data flows
	- interactions with users
- These threats can be used further as the roots for threat trees - one tree for each threat goal
	- Identify threats as weaknesses of security controls using categorization
	- Common threat lists can help here
- Use and abuse cases can illustrate how existing measures can be bypassed or where they are lacking.
- Value-based risk models like DREAD(more subjective) can be used to ID the threat associated with a security risk.
- Can use qualitative risk model - based upon general risk factors (likelihood/impact)

1. Threat Categorization
	1. STRIDE
		1. Spoofing
		2. Tampering
		3. Repudiation
		4. Information Disclosure
		5. Denial of Service
		6. Elevation of Privilege
2. Threat Analysis
3. Ranking Threats
4. Subjective Model: DREAD
5. Qualitative Risk Model
6. Determine Countermeasures and Mitigation
7. STRIDE Threat & Mitigation Techniques
8. Complementing Code Review
#### 3. Determine Countermeasures and Mitigation
Implementing a countermeasure can mitigate a vuln. Once a risk is assigned a threat(Step 2) it is possible to sort threats from highest to lowest - prioritize mitigation efforts based on business impact.
- Accept: decide that the business impact is acceptable
- Eliminate: remove components that make the vulnerability possible
- Mitigate: add checks or controls that reduce the risk impact or the chances of occurrance.






- how do
- methodology/practice

### Sources
- https://owasp.org/www-community/Threat_Modeling
- https://owasp.org/www-community/Threat_Modeling_Process
# **Security Automation**