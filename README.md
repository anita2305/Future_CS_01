 Assessment Overview

 
 This engagement evaluated the OWASP Juice Shop application to uncover security weaknesses using a
 combination of OWASP ZAP scanning and hands-on verification. Significant issues were discovered—including
 SQL Injection and configuration errors—that could allow unauthorized access and expose sensitive information. All
 results were aligned to the OWASP Top 10 (2021) and ordered by risk severity to aid remediation planning.





 
 Tools Utilized

 
  • Kali Linux

  
  • OWASP Juice Shop

  
  • OWASP ZAP




  
 Methodology

 
 The public deployment of OWASP Juice Shop hosted on Heroku served as the test environment, enabling realistic
 attack simulations without local setup. Automated active scanning in OWASP ZAP enumerated inputs and
 interaction points, while manual testing validated and expanded upon the scanner findings. Each identified issue
 was mapped to the applicable OWASP Top 10 category and paired with targeted remediation guidance.
 Target URL: https://juice-shop.herokuapp.com



 
 Key Findings

 
 SQL Injection (SQLi)

 
 A flaw in the authentication workflow permitted crafted inputs (e.g., 'OR 1=1--') to manipulate underlying queries,
 bypassing login controls and potentially granting administrative access.

 
 Impact: Full compromise of sensitive data and admin-level functionality.

 
 Risk Rating: High

 
 Recommended Mitigations:

 
  • Use parameterized queries / prepared statements.

  
  • Implement strict server-side input validation and output encoding where relevant.

  
  • Apply least-privilege permissions to database accounts.



  
 Cross-Domain Trust Misconfiguration

 
 Overly permissive cross-domain settings allowed untrusted origins to interact with the application, creating paths for
 malicious sites to perform actions on behalf of logged-in users.

 
Impact: Potential session hijacking and unauthorized request execution.


 Risk Rating: Medium

 
 Recommended Mitigations:

 
 • Restrict allowed origins to specific trusted domains; avoid wildcards.

 
  • Harden relevant security headers (e.g., CORS).



  
 Outdated JavaScript Library

 
 The application referenced an older jQuery release (2.2.4) with known vulnerabilities, increasing exposure to
 client-side attacks.

 
 Impact: Risk of XSS, code injection, or stability issues on the client side.

 
 Risk Rating: Medium

 
 Recommended Mitigations:

 
 • Upgrade to a supported, patched jQuery version and remove unused libraries.




 
 Content Security Policy (CSP) Gaps

 
 Missing or weak CSP directives heightened the chance of successful client-side attacks such as XSS, clickjacking,
 and data injection.

 
 Impact: Elevated probability of client-side exploitation.

 
 Risk Rating: Medium

 
 Recommended Mitigations:

 
 • Define a restrictive CSP (default-src 'none' with explicit allowlists).


 • Avoid wildcard sources; set safe fallbacks.
