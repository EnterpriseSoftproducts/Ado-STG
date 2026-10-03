# Testing for Insecure Organization Configuration

## 1 - Summary
The "organization" is the fundamental building block in Azure DevOps; this is where all the projects, repos, files, and pipelines live.
Security and a secure setup are therefore key to remediating common security issues across all underlying projects.
The security of this is mostly related to user access control, package management, and audit logging.

The key values we are looking at here are:
- Validate SSH key expiration - Ensures that old SSH keys cannot be used
- Log audit events - Log key events for forensic investigation and debugging
- Restrict personal access token (PAT) creation - Many incidents are caused by the leakage of credentials and tokens; limiting the potential number of users who can create PATs helps limit the potential attack surface and which accounts might have credentials leaked
- Additional protections when using public package registries - Limiting access to external repositories greatly limits the risk of supply chain attacks.
- Enable IP Conditional Access policy validation on non-interactive flows - Conditional access policies add another layer of defense against abnormal activity, and restricting non-interactive flows reduces the chance of compromise and increases the complexity needed for a successful attack.
- External guest access - External guest access represents a risk since these users represent an attack vector; if the user or external tenant is compromised, then this might lead to an incident in this organization.
- Allow Microsoft to collect feedback from users - Having Microsoft collect data from the DevOps organization might lead to privacy-related issues.

## 2 - Test Objectives</h1>
- Identify insecure settings in an Azure DevOps organization

## 3 - How to Test
These issues can be assessed from the organization's settings page in the web interface: <code>https://dev.azure.com/{organization}/_settings/organizationOverview</code>.
Review the following items under 'security' -> 'policies':

```
Policy.ValidateSshKeyExpiration 
Policy.LogAuditEvents 
Policy.DisablePATCreation 
Policy.ArtifactsExternalPackageProtectionToken
Policy.EnforceAADConditionalAccess 
Policy.DisallowAadGuestUserAccess 
Policy.AllowFeedbackCollection 
```

## 4 - Remediation
Reconfigure the settings to the following:

```
'Policy.ValidateSshKeyExpiration':
{  
  "reccomendedValue"</span>: True 
}, 
'Policy.LogAuditEvents':
{  
  "reccomendedValue": True
}, 
'Policy.DisablePATCreation':
{  
  "reccomendedValue": True
}, 
'Policy.ArtifactsExternalPackageProtectionToken'
{  
  "reccomendedValue": True
}, 
'Policy.EnforceAADConditionalAccess'</span>:  
{  
  "reccomendedValue": True
}, 
'Policy.DisallowAadGuestUserAccess'</span>: 
{  
  "reccomendedValue": True
}, 
'Policy.AllowFeedbackCollection'</span>: 
{  
  "reccomendedValue": False
}, 
```

## 5 - References
- https://www.cloudthat.com/resources/blog/azure-devops-best-practices-part-1
