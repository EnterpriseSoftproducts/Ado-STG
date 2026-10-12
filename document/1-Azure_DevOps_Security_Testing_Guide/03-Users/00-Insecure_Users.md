# Testing for Insecure Users
|ID          |
|------------|
|AdoSTG-USR-01|

# 1 - Summary
The more access an account has, the greater the potential impact if said account is breached. Many cyberattacks and their consequences can be attributed to overly privileged accounts, such as the Novo Nordisk compromise in 2026, where a Private Access Token (PAT) was left in a client-side script. This then gave attackers access to the company's GitHub, where more credentials were found, which allowed further access. In this finding, access is checked for each user, and if they have certain privileges or memberships on 60% or more repos, the account is flagged.

Other issues, like administrators from external organizations, also represent a threat since these are not under the organization's control and enforced security. If the tenant or organization of the external administrator gets compromised, then this might lead to the attacker moving laterally to your ADO environment.

# 2 - Test Objectives
- Identify excessive repo/project access
- Identify excessive administrators for projects
- Identify external administrators

# 3 - How to Test
## 3.1 - Identify excessive repo/project access
Identifying excessive repo access is easiest done with a tool like DRAGONLADY; this involves requesting permission reports for each project and comparing access across repos. Dangerous permissions to look out for are:

```
"Contribute",  
"Bypass" policies when completing pull requests","  
"Bypass" policies when pushing","  
"Contribute" to pull requests","  
"Manage" permissions","  
"Read" 
```
## 3.2 - Identify excessive administrators for projects
Inspect the users of the project and check that the number of administrators is within reason. In general, no more than 10% of users should be administrators; however, this depends on the number of users and organization size.

## 3.3 - Identify external administrators
Check the administrators and identify users who do not belong to the Azure tenant connected to the Azure DevOps setup.

# 4 - Remediation
Enforce the principle of "least privilege" and ensure that all administrators originate from within the organization.

# 5 - References
- N/A
