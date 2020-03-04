# Insecure OTP Implementation
## Bypassing OTP by Redirecting it to another number

Control Method
Control Group
Control
Vulnerability
Audit Guidelines
Description
Impact
Recommendation
Reference

#### DYNAMIC ANALYSIS
#### Insecure OTP Implementation
#### Bypassing OTP by Redirecting it to another number
#### AUDIT GUIDELINES
##### Check if the OTP is passed in the request body
#### DESCRIPTION
During security assessment, it has been observed that the OTP is passed in the request body, attacker intercepted the request using a proxy tool such as Burp suite and replaced victim's mobile number with his mobile number and the OTP was redirected to his number. 
#### IMPACT
##### Intergrity Loss
#### RECOMMENDATIONS
Generation of OTP should be validated at the server side
#### REFERENCES 
[Link1](https://cheatsheetseries.owasp.org/cheatsheets/Transaction_Authorization_Cheat_Sheet.html)
