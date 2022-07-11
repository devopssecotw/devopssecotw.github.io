# dos
## java
### security

#### OWASP
##### coding - checklist
###### Input Validation
- trusted systems
- trusted and untrusted sources
- data type, range and length of input
- Validating all data provided by the client/user
###### Output Encoding
- Cross-site scripting attacks
- Encoding all characters
###### Authentication & Password Management
- Require authentication for all resources/pages that link to CIA Triad.
- Prevent the re-using of passwords. 
- Notify users when password reset occurs.
- Report the number of login failure to the user upon their next successful login.
- Keep a short expiry time for temporary passwords that needs to be changed upon next login.
- Require passwords to be set on the basis of password complexity policy
###### Session Management
- Sessions and connections should be fully terminated upon logout
- Multiple logins should not be allowed against the same User ID.
- Based on the risks and business objectives, session inactivity timeout interval should be as low as possible
###### Access Control
- authorized users should have access to protected URLs, services, application data, user data, attributes etc.
- Account auditing should be implemented and unused accounts should be deleted.
- Accounts associated with different services to external or internal systems that are primarily used for non-critical tasks should be given least privilege.
- The number of transactions should be limited for a single user or device during a particular period of time
###### Cryptographic Practices
- A trusted system should be used to implement cryptographic functions to maintain confidentiality of sensitive data on the application
- The generation of random numbers, file names, GUIDs and strings should use an approved random number generator
- Cryptographic key management should be employed by developing and using processes and policies
- Master keys should be protected from unauthorized access
###### Error Handling & Logging
- Error handlers that do not throw out debugging information in case of unsolicited input should be used
- When error conditions occur, memory should be properly freed.
- Logs should not store sensitive information related to systems, sessions etc
- Logs related to input validation failures, authentication attempts, access control, system exceptions, unexpected changes to data and changes made to security configurations should be maintained and checked thoroughly
###### Data Protection
- Follow the principle of least privilege by limiting user rights and privileges to those systems, information and usability that are required to achieve the required goals and objectives.
- Exclude sensitive data from GET requests found in HTTP.
- Protect server-side code and prevent it from being accessible by the common user. Proper access control should be implemented for critical and sensitive data.
- Autocomplete feature should be excluded while entering data into forms on websites or applications
###### Communication Security
- failed connections should not downgrade to unsecure protocols
- For protection of sensitive information over external sources use TLS.
- All connections should be specified with character encoding
###### System Configuration
- Ensure that systems, frameworks and system components are running latest versions and patches.
- Application of least privilege should be on services accounts, webservers and processes.
- HTTP response headers should only include relevant information. OS, webserver version and software frameworks information should not be included.
- Test and development environments should be isolated from production environment
###### Database Security
- While accessing the database, the application should use lowest possible level of privilege
- Default passwords should be changed immediately. Password hygiene should be kept in mind while assigning passwords to accounts
- Enable multifactor authentication where applicable. Disable default accounts that are not necessary for business requirements
###### File Management
- Ensure authentication while uploading a file on the server.
- Files uploaded on the server should be validated by checking the file headers.
- Execution privileges should be turned off in the directories where files are uploaded.
- Absolute file path should never be sent to the client.
###### Memory Management
- Vulnerable functions such as print, strcat, strcpy etc. should be avoided.
- Buffer size should be checked for overflows.
- Input strings should be truncated properly before functions like copy and concatenation are used.

### references
- <https://owasp.org/www-project-top-ten/> 
- <https://owasp.org/www-pdf-archive/OWASP_SCP_Quick_Reference_Guide_v2.pdf>
- <https://www.owasp.org/index.php/OWASP_Top_Ten_Project>
- <https://www.securecoding.com/blog/owasp-secure-coding-checklist/>