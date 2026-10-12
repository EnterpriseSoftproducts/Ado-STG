# Code Injection
|ID          |
|------------|
|AdoSTG-AI-02|

# 0 - Summary
This section describes how a tester can check if its possible to abuse "AI" functionality to inject untrusted code into a pipelines execution.
This can happen when the pipeline uses untrusted input from a user in a step, thsi can both be used for prompt and code injection.
Notably, this will need additional privileges to execute since this will not start a regular trigger for a pipeline.

# 1 - Test Objective
- Identify pipelines where untrusted input is passed to an "AI" aka. sinks (variables, parameters, macros, templates).
- Identify sources of untrusted inputs aka. sources.

# 2 - How to Test
For this to be an issue the following criteria has to be met:

The pipeline needs to be using an "AI" action, we can check for this by looking at the yaml file and look for strings indicating use of various "AI" providers (please note that this list only includes major well known providers other local of lesser known providers might be used):

```
majorProviders = ["claude", "gemini", "copilot", "openai", "codex", "deepseek"] 
aiAssistants = ["cursor", "coderabbit", "qodo", "pr-agent", "devin"] 
additionalAiProviders = ["sourcery", "ai-pr-review", "ai-code-review", "cline", "mistral", "llama", "anthropic", "cohere"] 
selfhostedRuntimes = ["chatgpt", "gpt-4", "gpt-3", "bing-chat", "bard", "phind", "perplexity", "you-ai", "jasper", "tabnine", "ollama"] 
mcp = ["mcp", "model-context-protocol"]
```
Then we need to provide untrusted input such as in commit message, branch names etc:
```
"Build.SourceVersionMessage",  # Commit message (user-controlled) 
"Build.SourceBranchName",  # Short branch name (user-controlled via PR) 
"Build.SourceBranch",  # Full branch ref e.g. refs/heads/feature/foo 
"Build.RequestedFor",  # Display name of person who triggered build 
"Build.RequestedForEmail",  # Email of person who triggered build 
"System.PullRequest.SourceBranch",  # PR source branch name 
"System.PullRequest.TargetBranch",  # PR target branch name 
```
# 3 - Remediation
Avoid passing user-controlled input directly to AI tasks. Validate and sanitize input before use.

# 4 - References
- https://githubcom/praetorian-inc/trajan/blob/main/pkg/azuredevops/detections/ai/ai.go
