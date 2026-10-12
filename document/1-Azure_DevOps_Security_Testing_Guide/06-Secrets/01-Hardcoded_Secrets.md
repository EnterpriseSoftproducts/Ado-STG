# Testing for Issues Related to Secrets
|ID          |
|------------|
|AdoSTG-SE-02|

# 1 - Summary
Secrets in plaintext are one of the enduring issues for cybersecurity. Azure DevOps furthermore introduces several ways in which a developer can expose secrets, credentials, tokens, etc. Most of these issues revolve around either hardcoding secrets in files or implementing functionality that prints secrets stored in the .env file to somewhere accessible to an attacker.

# 2 - Test Objectives
- Identify hardcoded credentials

# 3 - How to Test
Review files, descriptions, commit messages, and history for hardcoded secrets and credentials.

# 4 - Remediation
To remediate these issues, please avoid using commands that expose secrets in stdout and logs. Additionally, please refrain from hardcoding credentials anywhere.

# 5 - References
- N/A
