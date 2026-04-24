# Ai-GRC-Agent

Ai-GRC-Agent is an AI-powered platform designed to analyze system configurations for security weaknesses, compliance gaps, and regulatory adherence. The agent uses LLMs to provide actionable recommendations and insights.

## Features

- Parse system configurations
- Identify weak and strong security features
- Detect compliance gaps and regulatory violations
- Provide prioritized security recommendations
- Navigate through agent workflow node

## Live Workflow Access

View the live workflow (read-only):
   https://alpcartercapstone.app.n8n.cloud/workflow/rIF0oQ6DakaXzA5m

- Built using n8n (workflow automation platform)
- This link shows the structure and logic of the AI agent
- To run or modify it, import the workflow into your own n8n instance


## Slack Access (Run the Agent)

### 1. Join Slack Workspace
   https://join.slack.com/t/zt-3slu0k710-IOt~sabEuGNfxa7Z9b_vYQ

### 2. Requirements
- At least one user must host the workflow in n8n
- Once connected, anyone in the Slack workspace can use the agent

### 3. Trigger the Agent

In Slack: `@Automated GRC Agent Bot hello`

(or any message)

### 4. Complete the Form

You will receive a DM asking for:

- Organization location  
- Sector (currently business/finance)  
- Number of users/data subjects  
- Security self-assessment (1–10 scale)  
- Optional explanations  

> “I don’t know” is accepted — the agent will provide baseline recommendations.

### 5. Get Results

After ~2–3 minutes, the bot returns:

- Applicable regulations  
- Compliance gaps  
- Security weaknesses  
- Prioritized recommendations  


## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/AlpBerrak/Ai-GRC-Agent.git
   ```
2. Follow setup instructions in /docs/setup.md (TBD)

3. Run the agent workflow for system analysis

## Milestones

1. Data Compilation: Gather regulations and system info

2. LLM Training: Train models for security and compliance

3. Agent Logic: Build nodes and workflow

4. Security & Pentesting: Input sanitation, rate limiting, encryption


## Contact

For questions or collaboration, reach out to the contributors:

- **Alp Berrak** – [GitHub](https://github.com/AlpBerrak)  
- **Carter Jules** – [GitHub](https://github.com/CarterJules)

