# Testing for Insecure Service Conenctions
|ID          |
|------------|
|AdoSTG-SC-01, AdoSTG-SC-02, AdoSTG-SC-03|

# 1 - Summary
ADO Service connections are authenticated connections between ADO and a remote/external resource where a task is executed.
Examples include databases, internet services like GitHub, and more.
If used incorrectly, these can become a security concern, as they might allow for pivoting and lateral movement.

# 2 - Test Objectives
- Check for dynamic expressions in service connections - these would allow an attacker to inject code and take over the service potentially
- Check for exposure in environmental variables, as these could leak to logs, etc.
- Check for 'Grant access to all pipelines'

# 3 - How to Test
## 3.1 - Dynamic Expressions
To assess whether this is an issue, inspect the pipeline for the presence of dynamic variables like ${{ }} Azure template expressions or $(( )) Azure variable expressions, and the presence of known service connections:
```
[ 
"azureSubscription", 
"connectedServiceName", 
"kubernetesServiceConnection", 
"dockerRegistryServiceConnection", 
"azureServiceConnection", 
"awsCredentials", 
"gcpConnection", 
]
```
 
## 3.2 - Exposed service connections
Check for service connections defined as variables and whether they are exposed in logs or have their contents printed to files, stdout, or anywhere an attacker might be able to see them.

## 3.3 - 'Grant access to all pipelines'
This can be found under the settings for the service connection; alternatively, if a service connection is used across many different pipelines, this might also indicate that the flag is set for a given connection.

# 4 - Remediation
## 4.1 - Dynamic Expressions
Never use parameters or variables in service connection names. Hardcode the connection name to prevent attackers from accessing arbitrary service connections.

## 4.2 - Exposed service connections
Avoid exposing service connections in environment variables as they may leak to logs. Use the task's built-in connection parameters instead.

## 4.3 - 'Grant access to all pipelines'
Disable 'Grant access to all pipelines' for service connections. Explicitly grant access only to pipelines that require it. This prevents compromised pipelines from accessing sensitive service connections.

# 5 - References
- https://learn.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints?view=azure-devops
