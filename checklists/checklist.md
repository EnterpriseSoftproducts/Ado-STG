# Testing Checklist

The following is the list of items to test during the assessment:

> Note: The `Status` column can be set for values similar to "Pass", "Fail", "N/A".

| Test ID        | Test Name                                                         | Status | Notes |
|----------------|-------------------------------------------------------------------|--------|-------|
| **AdoSTG-ORG** | **Organization Settings**                                         |        |       |
| AdoSTG-ORG-01  | Insecure Organization Settings                                    |        |       |
| **AdoSTG-PRO** | **Project Settings**                                              |        |       |
| AdoSTG-PRO-01  | Project set to 'Public'                                           |        |       |
| AdoSTG-PRO-02  | Excessive Number of Admins found for Project(s)                   |        |       |
| **AdoSTG-PAC** | **Pipeline Access Control**                                       |        |       |
| AdoSTG-PAC-01  | Variable group accessible in environment variable                 |        |       |
| AdoSTG-PAC-02  | Lacking Approval Gates for Pipeline                               |        |       |
| AdoSTG-PAC-03  | Approvers Allowed to Approve Their Own Requests                   |        |       |
| **AdoSTG-USR** | **Users**                                                         |        |       |
| AdoSTG-USR-01  | External Administrators Found                                     |        |       |
| AdoSTG-USR-02  | Excessive Repository Access                                       |        |       |
| **AdoSTG-AP** | **Agent Pools**                                                    |        |       |
| AdoSTG-AP-01  | Self-hosted agent pool                                             |        |       |
| AdoSTG-AP-02  | Self-hosted agent pool AutoProvisioned                             |        |       |
| AdoSTG-AP-03  | Exessive Number of Agent Pool Admins                               |        |       |
| **AdoSTG-PI** | **Pipeline Injection**                                             |        |       |
| AdoSTG-PI-01  | Script (compile-time template expression) Injection point found    |        |       |
| AdoSTG-PI-02  | Parameter interpolation in runtime expressions                     |        |       |
| AdoSTG-PI-03  | Variable from PR context                                           |        |       |
| AdoSTG-PI-04  | Macro references an injectable context                             |        |       |
| AdoSTG-PI-05  | Dynamic template reference                                         |        |       |
| AdoSTG-PI-06  | Dynamic template reference with runtime expression                 |        |       |
| AdoSTG-PI-07  | Wildcard Triggers                                                  |        |       |
| **AdoSTG-SE** | **Secrets Exposure**                                               |        |       |
| AdoSTG-SE-01  | Echo command with variable expansion                               |        |       |
| AdoSTG-SE-02  | Secrets Sent via HTTP                                              |        |       |
| AdoSTG-SE-03  | Dumping of Enviornmental Variables: Printenv                       |        |       |
| AdoSTG-SE-04  | Dumping of Enviornmental Variables: set, env                       |        |       |
| AdoSTG-SE-05  | Hardcoded Secrets                                                  |        |       |
| **AdoSTG-AI** | **"AI"**                                                           |        |       |
| AdoSTG-AI-01  | 'AI' Token Exfiltration                                            |        |       |
| AdoSTG-AI-02  | 'AI' Receives Untrusted Input                                      |        |       |
| AdoSTG-AI-03  | Insecure MCP Setup                                                 |        |       |
| **AdoSTG-SC** | **Service Connections**                                            |        |       |
| AdoSTG-SC-01  | Dynamic Service Connection(s)                                      |        |       |
| AdoSTG-SC-02  | Exposed Service Connection(s) in Enviornmental Variable(s)         |        |       |
| AdoSTG-SC-03  | Possible use of 'Grant access to all pipelines' Service Connection |        |       |
