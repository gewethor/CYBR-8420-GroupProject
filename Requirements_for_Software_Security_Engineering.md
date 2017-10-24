## Requirements for Software Security Engineering

#### Graylog Assurance Claims

*list of assurance claims here*


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
* There are several different documented methods available to install Graylog server. The Graylog documentation provides installation instructions including security hardening configurational changes that should be made if deploying to an operational environment. Graylog can be installed by the following: prebuilt Virtual Machine Appliances, operating System packages, Docker, Amazon Web Services, and manual setup.  

* When installing via the OVA virtualized appliance, which is not for operational use:

* The default password is ubuntu/ubuntu for the appliance and must be changed

* The default password for the web interface is admin/admin and must be changed

* Must disable remote password logins in /etc/ssh/sshd_config and deploy proper ssh keys

* Separate the box network-wise from the outside, otherwise Elasticsearch and MongoDB can be reached by anyone

* Add additional RAM to the appliance and raise the java heap!

* With graylog-ctl local-connect only the web interface is reachable from the outside.

