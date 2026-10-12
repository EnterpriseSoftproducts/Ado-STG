# Testing for Code Injection

|ID          |
|------------|
|AdoSTG-PI-01, AdoSTG-PI-02, AdoSTG-PI-03, AdoSTG-PI-04|


# 1 - Summary
This section describes how a tester can check if it's possible to abuse variables, parameters, macros, and templates in pipelines to gain code execution.

The main difference between variables and parameters is evaluation.

Evaluation is syntax-dependent. Variables defined with macro syntax (`'$(var)'`) evaluate at runtime before a task runs and are used in scripts and tasks. Variables defined with runtime expressions (`'$[variables.var]'`) evaluate before a job or stage runs and are used in conditions or dynamic variable assignment.

# 2 - Test Objectives
- Identify pipelines where injection points allow users to pass untrusted code.

# 3 - How to Test
## 3.1 - Code injection
To test for this, examine the pipeline definition for compile-time template expressions `${{ }}`. If these are in the form of parameters, then they might be user-controlled and can be used for code injection in the pipeline.

## 3.2 - Variable from PR context
Check if variables can come from a PR context; for this to be the case, "variables." need to be used in the pipeline, and these must not be system-safe variables, i.e., not user-controlled. A list of these is presented below:
```
"Build_BuildId", 
"Build_BuildNumber", 
"Build_Repository_Name", 
"Build_Repository_Uri", 
"Build_SourceVersion", 
"Build_DefinitionName", 
"System_TeamProject", 
"System_CollectionUri", 
"System_DefinitionId", 
"System_TeamProjectId", 
"System_CollectionId", 
"System_HostType", 
"System_JobId", 
"System_PlanId", 
"System_StageId", 
"System_PhaseId", 
"System_TimelineId", 
"System_TaskInstanceId", 
"System_JobDisplayName", 
"System_StageDisplayName", 
"Agent_BuildDirectory", 
"Agent_Id", 
"Agent_MachineName", 
"Agent_Name", 
"Agent_OS", 
"Agent_OSArchitecture", 
"Agent_TempDirectory", 
"Agent_ToolsDirectory", 
"Agent_WorkFolder", 
"Agent_JobName", 
"Pipeline_Workspace", 
```
## 3.3 - Parameter interpolation in runtime expressions
This issue contains parameters and variables that are used together with runtime expressions `$[ ]`; if this is the case and the runtime user expression is user-controlled, then the user can inject untrusted code into the pipeline.

To check for this, look for runtime expressions `$[ ]` and "parameters." or "variables."

## 3.4 - Macro references an injectable context
To check for this issue:

- First determine if macro expressions `$(VarName)` are ised in the pipeline.
- Then determine if this is supplied via user-controlled "variables." or "parameters."
- Next, verify that the "variables." or "parameters." are not system safe:

```
"Build.BuildId", 
"Build.BuildNumber", 
"Build.SourceVersion", 
"Build.SourceVersionMessage", 
"Build.Repository.Name", 
"Build.Repository.Uri", 
"Build.DefinitionName", 
"Build.Reason", 
"System.TeamProject", 
"System.CollectionUri", 
"System.DefinitionId", 
"System.TeamProjectId", 
"System.CollectionId", 
"System.HostType", 
"System.JobId", 
"System.PlanId", 
"System.StageId", 
"System.PhaseId", 
"System.TimelineId", 
"System.TaskInstanceId", 
"System.JobDisplayName", 
"System.StageDisplayName", 
"Agent.BuildDirectory", 
"Agent.Id", 
"Agent.MachineName", 
"Agent.Name", 
"Agent.OS", 
"Agent.OSArchitecture", 
"Agent.TempDirectory", 
"Agent.ToolsDirectory", 
"Agent.WorkFolder", 
"Agent.JobName", 
"Pipeline.Workspace" 
```

# 4 - Exploitaiton
This section shows how this issue can be exploited.

## 4.1 - Privileges
The minimum privileges to execute this attack, given a vulnerable build definition was found, are:

Edit queue build configuration and Queue builds

## 4.2 - Abuse
For standard code injection, the user can add the command to be injected into the vulnerable variable.

A vulnerable .yaml file might look like this:
```
0trigger: 
1- main 
2pool: 
3 vmImage: ubuntu-latest 
4steps: 
5- script: | 
6 echo $(InjectionPoint) 
7 displayName: 'Use variable to perform code injection' 
Using a standard code injection such as && whoami produces the following:

0Condition evaluation 
1Starting: Use variable to perform code injection 
2============================================================================== 
3Task         : Command line 
4Description  : Run a command line script using Bash on Linux and macOS and cmd.exe on Windows 
5Version      : 2.279.0 
6Author       : Microsoft Corporation 
7Help         : https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/command-line 
8============================================================================== 
9[Host] Selected Node version: Node24 (Strategy: Node24Strategy) 
10Generating script. 
11Script contents: 
12echo  && whoami 
13========================== Starting Command Output =========================== 
14/usr/bin/bash --noprofile --norc /home/vsts/work/_temp/268acd86-4744-46ab-8373-471b0118bae6.sh 
15vsts 
16Finishing: Use a variable to perform code injection 
```


# 5 - Remediation
## 5.1 - Code injection
Use an environment variable instead of direct parameter interpolation in scripts. Set the parameter as an env var and reference it safely.

## 5.2 - Variable from PR context
Avoid using variables directly in scripts, as they may come from PR context. Use environment variables with validation instead.

## 5.3 - Parameter interpolation in runtime expressions
Runtime expressions with parameters or variables can be exploited. Use environment variables with validation instead of runtime expressions in scripts.

## 5.4 - Macro references an injectable context
Macro expression references an injectable variable. Use an environment variable instead of direct macro interpolation in scripts.

# 6 - References
- https://github.com/praetorian-inc/trajan/blob/main/pkg/azuredevops/detections/pipelineinjection/pipelineinjection.go
- https://learn.microsoft.com/en-us/azure/devops/pipelines/process/runtime-parameters?view=azure-devops
- https://pulsesecurity.co.nz/advisories/Azure-Devops-Command-Injection
- https://devblogs.microsoft.com/devops/pipeline-argument-injection/
