# Testing for Variable Group Permissions

|ID          |
|------------|
|AdoSTG-PAC-01|

# 1 - Summary
In ADO, variable groups are collections of defined variables that can be shared across pipelines. This can be configured with the option 'accessible to all pipelines'. This is a security risk, as it potentially exposes secrets in the variable group.

# 2 - Test Objectives
- Identify a variable group with 'accessible to all pipelines' enabled

# 3 - How to Test
For each variable group, inspect the pipeline access permissions and check for 'accessible to all pipelines'.

# 4 - Remediation
Restrict variable group access. Ensure variable groups are not marked as 'accessible to all pipelines'. Link variable groups explicitly to specific pipelines only.

# 5 - References
- https://oneuptime.com/blog/post/2026-02-16-how-to-use-variable-groups-and-secret-variables-in-azure-pipelines-yaml/view
