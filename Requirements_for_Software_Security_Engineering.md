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

Log managment applications such as Graylog, require that they remain secure in order to prevent the hiding of malicious activities.  Graylog has serveral features in place to address security requirements needed to make it a trustworthy system.
1. Graylog



http://docs.graylog.org/en/latest/pages/users_and_roles/users.html

http://docs.graylog.org/en/2.3/pages/users_and_roles/roles.html

http://docs.graylog.org/en/latest/pages/configuration/https.html

http://docs.graylog.org/en/2.3/pages/configuration/rest_api.html

https://discuss.elastic.co/t/how-should-i-encrypt-data-at-rest-with-elasticsearch/96


#### Graylog Installation and Configuration Security Issues  
  
