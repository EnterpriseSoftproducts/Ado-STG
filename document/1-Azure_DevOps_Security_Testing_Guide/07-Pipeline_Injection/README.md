# 1.7 - Pipeline Injection
ADO Pipelines is the way CI/CD is handled in Azure. These contain the information and code to be run by a given agent when a trigger is executed. Since pipelines serve a central role in the deployment and testing process, they often have access to secrets and endpoints. This section contains the methodology for testing whether a user can supply untrusted code to pipelines via variables, macros, parameters, templates, etc., and whether any dangerous triggers are used.

1.7.1 [Testing for Code Injection](00-Code_Injection.md)

1.7.2 [Testing for Dangerous Triggers](01-Dangerous_Triggers.md)

1.7.3 [Testing for Template Injection](02-Template_Injection.md)
