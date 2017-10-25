## Requirements for Software Security Engineering

#### Graylog Assurance Claims

##### User Authorization
* **Top Claim**: Graylog prevents unauthorized modifications
* Graylog has a permission system based on roles which secures the access to its features
* Graylog allows for session timeout configuration.
* Customized permission levels and new Graylog roles can be created based on the level of authorization needed.
* Users with admin rights are unable to edit reader and admin roles.

##### Authentication
* **Top Claim**: GrayLog has acceptably reduced the risk of the authentication of unauthorized users.
* GrayLog mitigates malicious users bypassing LDAP authentication starting verision 0.92.
* Graylog requires the use HTTPS 
* GrayLog LDAP authentication requires complex password 
* GrayLog has been updated to it latest and most current version 
* Graylog LDAP Group is set up properly
* The user has admin permission and change the default password  
* Graylog User using LDAP authentication must be mapped in the LPDA group. 
* The user has setup other authentication provider such as API tokens.

##### Audit Logs
* **Top Claim**: Graylog audit log plugin sufficiently protects the integrity of the Graylog server from unauthorized alteration  
* Graylog utilizes audit log plugin to ensure adequate configuration tracking
* Graylog employs  documentation for  configuration setup to ensure users correctly deploy audit log plugin 
* Graylog's audit log plugin is built to support adequate advanced search functionality
* Graylog's audit Log plugin is built rigorously to PCI-DSS to ensure acceptable integrity 
* Graylog stores audit logs in mongoDB file system to ensure it is suitably protected 
* Graylog's documentation includes instructions for database setup to reduce the risk of improper installation 
* Graylog's audit log plugin supports free-text input as specific fields to provide a acceptable degree of fidelity
* MongoDB’s implementation default use of AES-256 for audit log plugin ensures acceptable integrity 
* AES-256 provides acceptable integrty

##### Encryption
* **Top Claim**: Graylog acceptably secures log data
* The system is using encryption at the file system level
* Security analysts configure the disk encryption subsystem
* The system logs all API requests
* The system log includes user name, remote address, and user agent
* The system can read the IP address from a supplied X-Forwarded-For HTTP header request

##### Access Tokens
* **Top Claim**: The Graylog REST API prevents unauthorized execution 
* All connections will require the use of HTTPS
* Access tokens will adequately secure the REST API 
* The signing key is adequately protected
* Access tokens can be invalidated
* Access tokens expire after a specified amount of time
* Access tokens are implemented according to industry best practices
* Security test contains no warnings
* The access test is executed properly


#### Graylog Security Requirements

* The Graylog dashboard shall require that users be authenticated by an authentication provider prior to gaining access to the system.
* The Graylog dashboard shall prevent malicous input from being used on the logon page in order to gain unathorized access.
* The Graylog dashboard shall prevent the use of brute force password attacks to gain unathorized access.
* The Graylog dashboard shall prevent unauthorized access to log data.
* The Graylog dashboard shall reduce the likelihood of an unauthorized user accessing the system from an unlocked workstation.
* The Graylog dashboard shall prevent network eavesdropping to obtain user credentials.
* Graylog shall ensure that log files can not be accessed directly outside of the dashboard or through API calls. 
* Graylog shall ensure that all attempts to modify system configuration settings are logged.
* Graylog shall ensure that all attempts to access log data are logged.
* Graylog shall prevent audit logs from being modified.
* The Graylog REST API shall prevent unauthorized users from executing APIs.
* The Graylog REST API shall prevent rouge users from acessing data that they are not authorized to access.
* The Graylog REST API shall prevent eavesdropping on network communications.
* The Graylog REST API shall allow for user access to be revoked by a system administrator.


#### Graylog Mis-use Case Diagram

https://www.lucidchart.com/documents/view/71d26345-1d5c-4b22-b79e-03bc3ab060d5/0
  
  
#### Alignment of Security Requirements with Graylog's Advertised Features

Log management applications such as Graylog, require that they remain secure in order to prevent the hiding of malicious activities.  Graylog has several features in place to address security requirements needed to make it a trustworthy system.

* Starting with Graylog 2.1.0, the system allows for the system administrator to select either an internal user database or pluggable authentication providers.  The plugins allow for providers such as LDAP and Single Sign-On.  http://docs.graylog.org/en/2.3/pages/users_and_roles.html#authentication-providers

* The Graylog documentation does not provide any information regarding input sanitization.

* The Graylog documentation does not provide any information regarding account lockouts after failed logon attempts.  

* Unauthorized access to log data is also provided with the use of roles.  Graylog provides for two default roles (Admin and Reader) that users can be assigned to.  System administrators can also create additional roles to provide customized user access. http://docs.graylog.org/en/2.3/pages/users_and_roles/roles.html# 

* Graylog allows the system administrator to configure a session inactivity timeout period.  http://docs.graylog.org/en/2.3/pages/users_and_roles/users.html#sessions

* Both the Graylog REST API and the web-based dashboard application can be configured to require the use of HTTPS to encrypt network communications.  http://docs.graylog.org/en/latest/pages/configuration/https.html

* Log files stored on the server should be encrypted to prevent access outside of the application.  Graylog is not directly responsible for encrypting this data.  System administrators need to make use of a third party tool such as dm-crypt to encrypt the Elasticsearch data.  https://discuss.elastic.co/t/how-should-i-encrypt-data-at-rest-with-elasticsearch/96

* The Graylog Audit Log plugin records all changes made by users into the system's database.  The application allows administrators to view events and filter on specific types of events. http://docs.graylog.org/en/2.3/pages/auditlog.html

* The Graylog REST API makes use of tokens provide user access.  Access tokens can be created to provide permenant access to the system.  Session tokens can be created to provide temporary access.  Session token expiration is defined in that user's profile.  Tokens may be revoked with a call to the REST API.  http://docs.graylog.org/en/2.3/pages/configuration/rest_api.html      


#### Graylog Installation and Configuration Security Issues  
There are several documented methods available to install Graylog server in a production environment. The Graylog documentation provides installation instructions and security precautions including security hardening configurational changes that should be made if deploying to a production environment. Graylog can be installed by the following: Virtual Machine Appliances, operating system packages, Docker, Amazon Web Services, and manual setup.

##### Graylog warns that the Graylog Open Virtual Appliance (OVA) is not recommended for operational environments without significant modification to the security posture. 

* The following are recommendations and precautions provided by Graylog’s documented installation instruction.

  * Change the Graylog OVA password from the default password of ubuntu/ubuntu.
 
  * Change the Graylog web interface password from the default password of admin/admin.
 
  * Disable all remote password logins in /etc/ssh/sshd_config and deploy proper SSH keys.
 
  * Isolated the Graylog host network from external access prevent Elasticsearch and MongoDB from being reachable by anyone on the outside.
 
  * Ensure that adequate additional RAM is allocated to the OVA to raise the java heap space.
 
  * Ensure that the graylog-ctl local-connect only the web interface is reachable from the outside.

##### Graylog documented installation instructions of Graylog Server via operating system packages does not include any special precautions.

* Other precautions outlined in the Graylog documentation
  * create your own unique installation where you understand each component and secure the environment by design
  * Expose only the services that are needed and secure them whenever possible with TLS/SSL and some kind of authentication
  * Graylog appliances are configured as to MongoDB and Elasticsearch is listening on the external interface, do not do this on production network
  * When using Amazon Web Services and our pre-configured AMI, never open all ports in the security group. Do not expose the server to the internet. Access Graylog only from within your VPC. Enable encryption for the communication.
  * Configure the trusted proxies setting in the Graylog configuration file to prevent against spoofing.
