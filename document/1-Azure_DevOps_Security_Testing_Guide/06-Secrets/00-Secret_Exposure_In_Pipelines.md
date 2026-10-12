# Testing for Issues Related to Secrets
|ID          |
|------------|
|AdoSTG-SE-01|

# 1 - Summary
Secrets in plaintext are one of the enduring issues for cybersecurity. Azure DevOps furthermore introduces several ways in which a developer can expose secrets, credentials, tokens, etc. Most of these issues revolve around either hardcoding secrets in files or implementing functionality that prints secrets stored in the .env file to somewhere accessible to an attacker.

# 2 - Test Objectives
- Identify functionality exposing secrets

# 3 - How to Test
Review pipelines for the following:
- The use of `env |` or `set |` or `printenv` commands in pipelines
- Use of the `echo` command along with variable expansion `${}` or `$()`
- Sending secrets via `curl` or `wget`

# 4 - Remediation
To remediate these issues, please avoid using commands that expose secrets in stdout and logs. Additionally, please refrain from hardcoding credentials anywhere.

# 5 - References
- N/A
