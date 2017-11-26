### Code Review Strategy 
The review strategy that we opted to go with is a Risk-based approach.
  * Strategy Summary - Gabi  
  * Threat model top level issues - Will
  * Misuses cases top level issues - Fadila

### Manual Code Review
  * Fadila & Will
  
### Automated Code Scanning
  
**JavaScript Code Analysis**
* DeepScan: https://deepscan.io/dashboard/#view=project&pid=1237&bid=3218&subview=overview
* MORE HERE

**Java Code Analysis**
* AttackFlow: https://drive.google.com/file/d/1ISsZNzKGJOf6izpHfTQ-uMVGaRuMXoie/view?usp=sharing
* Visual Code Grepper: https://drive.google.com/file/d/17ZO648K4noEs576cyyJArC3DZozaT1nv/view?usp=sharing
* MORE HERE

**Automated Scan Results**

| Code Type | Analysis Tool | Critical | High | Medium | Low |
| --- | --- | --- | --- | --- | --- |
| JavaScript | DeepScan | 0 | 2 | 21 | 158 |
| JavaScript | XXXXXXXXX | X | X | X | X |
| Java | AttackFlow | 0 | 54 | 1 | 264 |
| Java | Visual Code Grepper | 0 | 2 | 16 | 2382 |
| Java | XXXXXXXX | X | X | X | X |

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
CWE-XXX TODO  
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

### Links to any pull requests
