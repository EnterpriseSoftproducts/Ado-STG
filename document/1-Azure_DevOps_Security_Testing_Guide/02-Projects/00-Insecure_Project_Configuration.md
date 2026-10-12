# Testing for Insecure Project Configuration
|ID          |
|------------|
|AdoSTG-PRO-01, 02|

# 1 - Summary
When a project in Azure DevOps is public, this means that anyone with the link can see the project and its contents. This exposes the code and any secrets or misconfigurations to public scrutiny. ADO has now made it impossible to create new public projects. If you need a public project, use GitHub or a similar service to host it, and ensure no sensitive information is disclosed within the project.

#2 - Test Objectives
- Identify public projects
- Identify Excessive Administrators for project

# 3 - How to Test
## 3.1 - Public Projects
Check the settings for the project to see if the project is set to "public".

## 3.2 - Excessive Administrators
To identify, check the number of administrators for the project; for larger projects, it is recommended that less than 10% of users be part of the administrators group or have administrative privileges.

# 4 - Remediation
## 4.1 - Public Projects
In the settings menu of the project, change the visibility of the project to private.

1. Sign in to your organization (https://dev.azure.com/{yourorganization}).
2. Go to your project and select Project settings.
3. Select Overview.
4. In the Visibility dropdown menu, choose Private.
5. Select Save.

## 4.2 - Excessive Administrators
Reduce the number of administrators to only people who have an explicit business need for these privileges.

# 5 - References
- https://learn.microsoft.com/en-us/azure/devops/organizations/projects/make-project-public?view=azure-devops
