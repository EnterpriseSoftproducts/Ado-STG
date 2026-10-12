# Testing for Approval Gates
|ID          |
|------------|
|AdoSTG-PAC-02, AdoSTG-PAC-03|

# 1 - Summary
Approval gates in ADO are a set of features allowing for control over workflows defined in pipelines. Approval gates set the conditions for how and if a pipeline/job is allowed to execute. Various conditions can be specified, such as time of day or number of approvers. These gates and approvals can be specified along various parts of the CI/CD process; namely, they can be set for different phases of the deployment, such as before the pipeline is run or after. From a security perspective, what we are most concerned about here is that approval gates are configured such that a single compromised user cannot make changes to code and trigger a deployment.

# 2 - Test Objectives
- Identify a lack of approvers for pipelines
- Check that users cannot approve their own approval requests

# 3 - How to Test
To verify the configuration of pipelines, you need to inspect each project individually. Under "Pipelines" > "Environments," you will find the approver settings under each environment.

For each of these, check the following
- 2 or more approvers are required for pre-check approvals
- Approvers are not allowed to approve their own runs

# 4 - Remediation
Ensure that pipelines are configured to require a minimum of 2 approvers, and ensure that the users who request approval cannot approve their own requests.

# 5 - References
- https://learn.microsoft.com/en-us/azure/devops/pipelines/release/approvals/?view=azure-devops&tabs=yaml
