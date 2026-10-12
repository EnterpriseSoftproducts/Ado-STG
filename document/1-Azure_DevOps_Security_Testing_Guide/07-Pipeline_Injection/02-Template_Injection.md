# Testing for Template Injection
|ID          |
|------------|
|AdoSTG-AI-05, AdoSTG-PI-06|

# 1 - Summary
This section describes how a tester can check if it's possible to abuse pipeline templates.

The issue here is almost the same as with code injection in pipelines. However, here a template is defined with a user-controlled variable.

In pipelines the issues can look like:

```
- template: '${{ variables.varFileName }}'
```
This means that a user can potentially supply their own malicious template.

# 2 - Test Objectives
- Identify templates with dynamic expressions

# 3 - How to Test
To identify dynamic templates, look for the following in your pipelines:

runtime expressions `$[ ]`,  compile-time template expressions `${{ }}`, variable/parameter interpolation `$(var)` and `$[variables.var]`.

# 4 - Remediation
Ensure no templates use dynamic expressions (variables, parameters, or macros) in pipelines.

# 5 - References
- https://github.com/praetorian-inc/trajan/blob/main/pkg/azuredevops/detections/pipelineinjection/pipelineinjection.go
