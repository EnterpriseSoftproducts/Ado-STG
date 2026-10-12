# Testing for Insecure Agent Pools
|ID          |
|------------|
|AdoSTG-AP-01, AdoSTG-AP-02, AdoSTG-AP-03|

# 1 - Summary
Agent pools are the organizational unit in ADO that represents a collection of agents. Agents in ADO are the pieces of software responsible for running the code in an ADO pipeline.

This effectively means that if you control the Agent or Agent Pool, then you have code execution on whatever the agent is running on. This can allow an attacker to use this for pivoting from ADO to wherever the agent is running.

When an agent pool is set to be "autoprovisioned," this means that whatever agents reside in this pool are automatically accessible for all pipelines. This is an issue for self-hosted agents, as this removes granular control over access to the agent and widens the potential attack surface.

# 2 - Test Objectives
- Identify excessive administrators for pools
- Identify self-hosted agents
- Identify auto-provisioned self-hosted agents

# 3 - How to Test
All of the above issues can be identified by inspecting the "Agent Pools" tab under "Organization settings" in the ADO web interface.

# 4 - Remediation
Enforce the principle of "least privilege" and ensure that self-hosted agents are only used sparingly. Ensure that auto-provisioned agents are not used and instead that agents are assigned to pipelines/projects as needed.

# 5 - References
- https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/pools-queues
