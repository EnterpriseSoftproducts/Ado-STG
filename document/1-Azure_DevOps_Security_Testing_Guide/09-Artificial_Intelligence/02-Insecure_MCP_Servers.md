# Testing for Insecure MCP Servers
|ID          |
|------------|
|AdoSTG-AI-03|

# 0 - Summary
Potential MCP-enabled task found with untrusted input and token access; this potentially means that the MCP connection can be abused to gain remote code execution or exfiltrate sensitive information.
MCP servers in Azure DevOps mainly serve to retrieve and analyze data from ADO projects.
In their documentation, Microsoft [001] describes this as a two-step process:
- Data retrieval (MCP Server)
- AI analysis (Your AI assistant)
The general risk here is that MCP servers or exposed tokens can be abused by attackers to compromise accounts.

# 1 - Test Objectives
- Identify the use of MCP servers in pipelines and assess if untrusted input is passed to the pipeline, and if the pipeline has token access

# 2 - How to Test
## 2.1 - Identifying MCP indicators
MCP servers can usually be identified by the word "MCP" in the pipeline YAML file.
For example, to have an MCP client, the official MCP documentation [002] has the following example for implementation.
```
import asyncio 
import sys 
 
from mcp import Client, StdioServerParameters 
from mcp.client.stdio import stdio_client 
from mcp_types import TextContent 
 
from anthropic import Anthropic 
from dotenv import load_dotenv 
 
load_dotenv() # load environment variables from .env 
 
MODEL = "claude-opus-5" 
anthropic = Anthropic() 
```
Likewise, the Microsoft documentation [003] also contains "mcp":
```
{ 
 "servers": { 
   "ado-remote-mcp": { 
       "url": "https://mcp.dev.azure.com/{organization}", 
       "type": "http", 
       "headers": { 
           "X-MCP-Toolsets": "repos,wiki,wit" 
           } 
       } 
  }, 
 "inputs": [] 
} 
```
Simply grepping for the word "mcp" should have very few false positives and help identify where MCP clients are in use.

## 2.2 - Identifying Token Access
Once an MCP-enabled pipeline has been found, we can check for token access. The easiest way to achieve this is to look for known dangerous tokens:
```
SYSTEM_ACCESSTOKEN, 
System.AccessToken, 
AZURE_DEVOPS_EXT_PAT 
```
## 2.3 - Identifying Untrusted Input
Lastly, we can check for untrusted input being passed to the MCP server from the pipeline.

The following list contains user-controlled ADO contexts:
```
"Build.SourceVersionMessage", # Commit message (user-controlled) 
"Build.SourceBranchName", # Short branch name (user-controlled via PR) 
"Build.SourceBranch", # Full branch ref e.g. refs/heads/feature/foo 
"Build.RequestedFor", # Display name of person who triggered build 
"Build.RequestedForEmail", # Email of person who triggered build 
"System.PullRequest.SourceBranch", # PR source branch name 
"System.PullRequest.TargetBranch", # PR target branch name 
```
# 3 - Remediation
Disable MCP functionality in AI tasks or ensure pipeline tokens are not provided. If MCP is necessary, restrict to trusted inputs only.

# 4 - References
- https://learnmicrosoftcom/en-us/azure/devops/mcp-server/remote-mcp-server?view=azure-devops
- https://modelcontextprotocolio/docs/2026-07-28/develop/build-client
- https://githubcom/praetorian-inc/trajan/blob/main/pkg/azuredevops/detections/ai/ai.go
