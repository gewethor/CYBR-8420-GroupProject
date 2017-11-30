## Code Analysis for Software Security Engineering

### Code Review Strategy 
Before diving into our code review, we needed to determine a review strategy that best fit the needs of our review and the level of experience of our team. The review strategy that we determined would be most effective is a Risk-based approach. In order to utilize this strategy and create the most optimal approach, we needed to brainstorm as a team to determine our best course of action. Model code review of a large-scale project requires concise analysis of many thousands or more of lines of code. To narrow down and thus reduce the overall effort of the manual code review, The Ghostbusters developed a couple methods to come up with top level issues to look for. The first method utilizes the Threat model developed in the Microsoft Treat Modeling Tool. The second utilizes the Misuse case diagrams the Ghostbusters developed in an earlier task. 

#### Threat model top level issues
 
To develop the threat model top threats, all 42 of the threats identified by the Microsoft threat modeling tool were imported into a spreadsheet and grouped together in accordance with their respective interactions. This list was then mapped to Common Weakness Enumeration IDs (CWE) and CAPEC-IDs for ranking analysis. Threats were ranked from low to high based on several factors including: interactions with threat boundaries, rate of occurrence, and potential for exploitation. 

![alt text](https://github.com/gewethor/CYBR-8420-GroupProject/blob/master/graylog%20threat%20modeling.JPG "Threat Modeling Spreadsheet")

#### Misuses cases top level issues
  
To develop the Misuse cases top threats, each of the five major security function cases were scrubbed for threats. Once complete, each threat was compiled into a list for comparison with the threats identified by the Microsoft Threat Modeling Tool for new threats and duplicates. It was determined that there were no significant differences between the two and that the more comprehensive list from the threat modeling tool would be used as the principal data set for manual code analysis. 

### Manual Code Review

**Key Findings in Manual Code Review**

   * High - Hard Coded Password for mapping purposes 
CWE-798 & CWE-259: Hard Coded Passwords
CAPEC-ID 190 & 167: Reverse Engineering
GrayLog2-server seems to have few hard-coded value that reads “password”. I believe these “hard-coded password” are just keys that are used for mapping purpose, however these keys are exposed in clear text and might lead to some backdoor in the future. Action Taken: Issue Open and Produce Possible Solution

   
   * Medium – 
   CWE-667: Improper Locking
   CAPEC-ID 25: Forced Deadlock
   The software does not properly acquire a lock on a resource, or it does not properly release a lock on a resource, leading to unexpected resource state changes and behaviors.
   Shared Resources Not Locked Action Taken: Code Fix (To reduce deadlock behaviors and object been reused Use Synchronize blocks instead of Synchronized function)

       
   * Medium – 
   CWE-667: Improper Locking
   CAPEC-ID 25: Forced Deadlock
   Resource Not Being Released Some Exceptions were not being handle correctly Action Taken: Code Fix

   
Since you have implemented graylog2-server/src/main/java/org/graylog2/security/AESTools.java for encryption and decryption; I would suggest reading these keys from a property file and utilizing AESTools.decyprt()
	.ie graylog-enc.properties
enc-key=ENC(your_encrypted_key_with_salt)
  
### Automated Code Scanning
  
**JavaScript Code Analysis**
* DeepScan: https://deepscan.io/dashboard/#view=project&pid=1237&bid=3218&subview=overview
* Retire.js: https://retirejs.github.io/retire.js/

**Java Code Analysis**
* AttackFlow: https://drive.google.com/file/d/1ISsZNzKGJOf6izpHfTQ-uMVGaRuMXoie/view?usp=sharing
* Visual Code Grepper: https://drive.google.com/file/d/17ZO648K4noEs576cyyJArC3DZozaT1nv/view?usp=sharing
* Find Security Bugs: https://github.com/find-sec-bugs/find-sec-bugs/wiki/Maven-configuration

**Automated Scan Results**

| Code Type | Analysis Tool | Critical | High | Medium | Low |
| --- | --- | --- | --- | --- | --- |
| JavaScript | DeepScan | 0 | 2 | 21 | 158 |
| Javascript | Retire | 0 | 0 | 49 | 1 |
| Java | Find Security Bugs | 0 | 4 | 79 | 0 |
| Java | AttackFlow | 0 | 54 | 1 | 264 |
| Java | Visual Code Grepper | 0 | 2 | 16 | 2382 | 

### Summary of Key Findings

**Key Findings in Automated Java Code Analysis**

* High - Use of Dangerous Regular Expressions  
CWE-185: Incorrect Regular Expression  
CPAEC-492: Regular Expression Exponential Blowup  
Complex Regular expression patterns can result in denial of service attacks.

* High - Insecure Random Number Generator  
CWE-338: Use of Cryptographically Weak Pseudo-Random Number Generator (PRNG)  
Random number generator produces predictable values for any given seed which are easily reproducible once the starting seed is identified.

* High - Hardcoded Password  
CWE-259: Use of Hard-coded Password  
CWE-798: Use of Hard-coded Credentials  
CWE-321: Use of Hard-coded Cryptographic Key  
The code may contain a hard-coded password which an attacker could obtain from the source or by dis-assembling the executable.

* High - Mutable Static Field  
CWE-500: Public Static Field Not Marked Final  
An object contains a public static field that is not marked final, which might allow it to be modified in unexpected ways.  

* Medium - Exposing Internal Representation  
CWE-767: Access to Critical Private Variable via Public Method  
The software defines a public method that reads or modifies a private variable.  

* Medium - Synchronized Code - Possible Performance Impact  
CWE-667: Improper Locking  
Synchronized code block should not unnecessarily lock shared resources which can result in performance impacts.  

* Medium - Failure To Release Resources In All Cases  
CWE-401: Improper Release of Memory Before Removing Last Reference ('Memory Leak')  
Failure to release resources can result in a denial of service due to excessive resource consumption.

* Medium - Class Implements Public 'clone' Method  
CWE-491: Public cloneable() Method Without Final ('Object Hijack')  
Cloning allows an attacker to instantiate a class without running any of the class constructors by deploying hostile code in the JVM.

**Key Findings in Automated JavaScript Code Analysis**

* High - Null Pointer  
CWE-476: NULL Pointer Dereference  
A NULL pointer dereference occurs when the application dereferences a pointer that it expects to be valid, but is NULL, typically causing a crash or exit.

* Medium - Mismatched Type of Arguments  
CWE-628: Function Call with Incorrectly Specified Arguments  
The product calls a function, procedure, or routine with arguments that are not correctly specified, leading to always-incorrect behavior and resultant weaknesses.

* Medium - No Effect Call  
CWE-665: Improper Initialization  
This rule applies when the result of built-in API call, which has no side effects, is not used.

* Medium - Uninitialized Local Variable  
CWE-457: Use of Uninitialized Variable  
The code uses a variable that has not been initialized, leading to unpredictable or unintended results.

* Medium - Unreachable Code  
CWE-561: Dead Code  
The software contains dead code, which can never be executed

* Medium - Insufficient Null Check  
CWE-476: NULL Pointer Dereference  
A NULL pointer dereference occurs when the application dereferences a pointer that it expects to be valid, but is NULL, typically causing a crash or exit.

* Medium - Bad Type Coercion  
CWE-843: Access of Resource Using Incompatible Type ('Type Confusion')  
The program allocates or initializes a resource such as a pointer, object, or variable using one type, but it later accesses that resource using a type that is incompatible with the original type.

* Medium - 3rd Party CORS Request May Execute  
CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')  
The software does not neutralize user-controllable input before it is placed in output that is used as a web page that is served to other users.  

* Medium - Selector interpreted as HTML  
CWE-80: Improper Neutralization of Script-Related HTML Tags in a Web Page ('Basic XSS')  
The software receives input from an upstream component, but it does not neutralize or incorrectly neutralizes special characters such as "<", ">", "&", "$" that could be interpreted as web-scripting elements when they are sent to a downstream component that processes web pages.  

* Medium - Jquery Exceeding Stack Call Limit (DoS)  
CWE-400: Uncontrolled Resource Consumption ('Resource Exhaustion')  
The software does not properly restrict the size or amount of resources that are requested or influenced by an actor, which can be used to consume more resources than intended.  

* Medium - Regular Expression Which Could Cause a DoS  
CWE-185: Incorrect Regular Expression  
The software specifies a regular expression in a way that causes data to be improperly matched or compared. 


### Links to any pull requests
  More

### Links to issue opened

Issue opened https://github.com/Graylog2/graylog2-server/issues/4379
