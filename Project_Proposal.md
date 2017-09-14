# Project Proposal

## Project Description of Graylog:
  Graylog is an open source log management platform capable of handing a wide variety of log management-based tasks. Graylog is able to collect and process logs, wire data, and event data from any source. It is capable of allowing users to search through and analyze log data in a web interface designed for users. Trigger actions can be set using the web interface for users to be alerted for security issues or performance degradations. 
  
#### System Architecture
  Graylog is comprised of three main components: Graylog, MongoDB, and ElasticSearch.
  * **ElasticSearch** is utilized for log management and provides full-text searching capabilities.
  * **MongoDB** is utilized for storing meta information and configuration data.
  * **Graylog**, as discussed above, provides log management solutions. Graylog's servers act as log parsers, processes messages, and communicates with non-server components. The web interface provides the user interface for analyzing and managing the logs.
  
  ![Graylog Architecture](http://docs.graylog.org/en/2.3/_images/architec_small_setup.png)
 
#### Languages 
 While about 80% of the project is java based, the following is a breakdown of the additional languages used within the Graylog platform.
  
  * Javascript - 15%
  * XML - 1.5%
  * CSS - 1.3%
  * Ruby - 0.6%
  * shell script - 0.2%
  * PHP - 0.2%
  * HTML - 0.1%
  
#### Activity 
 To date, Graylog has 18,025 commits, which date back to May of 2010, made by 107 contributors. Graylog's commit history peaked in May of 2015 with 1,007 total commits that month. However, it's 30 day commit history average is very low given it's once highly active history. Within the last 12 months, Graylog has seen 546 commits and only 14 in the last 30 days. While the number of commits is quite low, Graylog contributors continue to appear very active. Github issues appear to be responded to within a very short period of time (the most recent issue to date was responded to by a contributor within the same hour).
 
#### Popularity (graylog2-server repository)
 * Watchers - 222
 * Stars - 3,592
 * Forks - 537
 * Active Installations - 25,000
 
#### Documentation Sources
 * Github Repository Link: https://github.com/Graylog2/graylog2-server 
 * GrayLog's Official Website: https://www.graylog.org/
 * Graylog's Documentation Page: https://www.graylog.org/
 
## What about the License of Graylog?

  Graylog is released under the version 3.0 of the GNU GPL General Public License. This license which affords end users the freedom to “run, study, share and modify the software” for free. All copyright and license are required to be preserved.

## Procedures for Making Contributions:

  GrayLog’s very active community is built on being open and accepting of contributions. These contributions can be divided up in several different categories such as documentation, new ideas, code development, Issue identification, and code fixes. It is required that before contributions are made, that the Contributor Covenant Code of Conduct is read and understood. This action ensures that the individual preparing to indulge in contributing and thus being an active participant into the Graylog community respects the people and fellow contributors allowing for a welcoming environment. 
  
  For documentation contributions, you are to edit the documentation in the Graylog2 documentation repo and initiate a pull request. To make contributions to the code to add new features, its is identified in their contributor’s guide that the individual should first discuss the idea with the core team. Once this idea is approved, the user should develop this code then file a pull request. This pull request will then be reviewed by the core team before merging code into the project. Additionally, if a issue is identified, they must be reported on the project’s Graylog Server GitHub repo using the issue tracker. It is also highly encurged by the team to attempt to fix reported issues and file a pull request for code to be merged.

## Security Related History:
  Grayog2 to its latest and most current version 2.2.3 has no exploitable vulnerabilities.
Before version 9.2, one vulnerability of Medium severity was found on GrayLog2. This vulnerability is named CVE-2014-9217 and allows remote attackers to bypass LDAP authentication via crafted wildcards. CVE-2014-9217 was discovered back on Dec 08, 2014 and has been solved on Graylog2 version 9.2. According to National Vulnerability Database, this vulnerability is Network exploitable, was of a low complexity.
There are not been any known or exploitable vulnerabilities since the CVE-2014-9217

## Functional Security Requirements for Graylog:

Graylog centralizes the storage of log information from many different sources such as servers, network devices and software applications.  Security is a key aspect to the implementation of a log management system.  Log files can contain information regarding system errors or possible intrusions.  Organizations must be able to trust that the information contained in the system is accurate and remains unmodified.

1. User Accounts / Authentication
* The system shall require users to have a unique username and require that user to login using an authentication provider such as passwords managed by the system or LDAP/Active Directory. 
* Open user sessions shall expire after a specific period of inactivity.
2. User Authorization
* The system shall require users to be assigned one or more roles that will define what level of permissions they should have.
  * Administrative users will be allowed to modify system configurations.
  * Users will be allowed to view log information.
* The system shall allow the creation of customized roles that will allow more granular levels of system access.
3. Audit Log
* The system shall maintain an audit log of all configuration changes made by users.
* The audit log shall be secured to prevent unauthorized modifications.
4. Encryption of Data at Rest
* The system shall ensure that all log data is encrypted to prevent unauthorized access and modifications.
5. REST API
* The system shall ensure that all calls to the Graylog REST API can only be made with a valid access token. 


## What was Ghostbusters motivation for choosing Graylog?

Graylog is a powerful extensible open source and diverse log management platform. It is a major competitor to other titans such as the proprietary Solarwinds and Splunk in providing tools for exploiting Big Data analysis, network systems management, forensics, and (dare I say it) Cyber Security! Graylog has a very active multi-contributor community with 533+ commits within the last 12 months from a very diverse population of contributors. No one contributor stands out, and thats a good thing. Furthermore, Graylog is primarily written in Java which affords our team additional leverage as it is the most common language between the four of us. Additionally, its licensing allows for easy access to the code and the ability to freely contribute back to the community as non-regulars. Finally, Graylog also is familiar as its actively being used in the day-to-day operations at the place of employment for one of the team members. All in all, Graylog checks several boxes for open and active development community, GPL license, great guidance on how the community should contribute, great developer documentation, and the wealth of security functional requirements for us to explore.

## Github Repository Link:
https://github.com/gewethor/CYBR-8420-GroupProject




