# Testing for Token Exfiltration
|ID          |
|------------|
|AdoSTG-AI-01|

# 0 - Summary
This section describes how a tester can check if it's possible to abuse "AI" functionality to extract sensitive Tokens using an agent by providing untrusted input via a PR trigger.

The issue here is that if a user is able to provide input to an agent, they can prompt the agent to disclose sensitive information like tokens without the user having specific access to these secrets (they might be set as "secret" preventing direct access).

# 1 - Test Objectives
- Identify pipelines where untrusted input and triggers can be used to coerce "AI" to exfiltrate sensitive tokens

# 2 - How to Test
For this to be an issue, the following criteria have to be met:

The pipeline needs to be using an "AI" action; we can check for this by looking at the yaml file and looking for strings indicating use of various "AI" providers (please note that this list only includes major, well-known providers; other local or lesser-known providers might be used):

```
majorProviders = ["claude", "gemini", "copilot", "openai", "codex", "deepseek"] 
aiAssistants = ["cursor", "coderabbit", "qodo", "pr-agent", "devin"] 
additionalAiProviders = ["sourcery", "ai-pr-review", "ai-code-review", "cline", "mistral", "llama", "anthropic", "cohere"] 
selfhostedRuntimes = ["chatgpt", "gpt-4", "gpt-3", "bing-chat", "bard", "phind", "perplexity", "you-ai", "jasper", "tabnine", "ollama"] 
mcp = ["mcp", "model-context-protocol"] 
```

Next, the "AI" needs to have access to sensitive tokens like "SYSTEMACCESS_TOKEN" or "PAT"s
Then we need to provide untrusted input such as in commit messages, branch names, etc:

```
"Build.SourceVersionMessage", # Commit message (user-controlled) 
"Build.SourceBranchName", # Short branch name (user-controlled via PR) 
"Build.SourceBranch", # Full branch ref e.g. refs/heads/feature/foo 
"Build.RequestedFor", # Display name of person who triggered build 
"Build.RequestedForEmail", # Email of person who triggered build 
"System.PullRequest.SourceBranch", # PR source branch name 
"System.PullRequest.TargetBranch", # PR target branch name 
```

Lastly, for the above, we need to be able to trigger the pipeline via a user controlled trigger like a "pull request"

# 3 - Exploitaiton
User-controlled inputs can be used for code injection and thus used to exfiltrate tokens and other secrets.

# 4 - Remediation
Avoid passing untrusted input (Build.SourceVersionMessage, etc.) to AI tasks with token access.

Use separate trusted pipelines or remove token access from AI tasks.

# 5 - References
- https://githubcom/praetorian-inc/trajan/blob/main/pkg/azuredevops/detections/ai/ai.go
