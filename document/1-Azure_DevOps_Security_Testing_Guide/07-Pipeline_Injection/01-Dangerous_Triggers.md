# Testing for Dangerous Triggers
|ID          |
|------------|
|AdoSTG-PI-07|

# 1 - Summary
This section describes how a tester can check if it's possible to abuse pipeline triggers to kick off pipeline workflows.

These issues are not directly abusable, but when combined with user-controlled inputs such as creating forks and then running these to gain access to potentially sensitive information or code execution on systems.

# 2 - Test Objectives
- Identify pipelines where insecure triggers can be abused to run untrusted code

# 3 - How to Test
Wildcard triggers are triggers where any part after the `'*'` is matched. Thus, if a user controls any of this, it can be used for malicious actions.

```
trigger: 
 branches: 
 include: 
 - main 
 - develop 
 - release/* 
 - feature/* 
 exclude: 
 - feature/experimental-* 
 - feature/wip-* 
```
Especially dangerous since these are user-controlled:
```
refs/heads/* 
users/* 
feature/* 
```

# 4 - Remediation
Avoid wildcard branch triggers. Use explicit branch lists or protected branch patterns. Apply branch policies to prevent unauthorized branch creation.

# 5 - References
- https://github.com/praetorian-inc/trajan/blob/main/pkg/azuredevops/detections/pipelineinjection/pipelineinjection.go
- https://www.grizzlypeaksoftware.com/library/pipeline-triggers-ci-pr-and-scheduled-builds-doz6mky7
