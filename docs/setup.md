# Setup Guide

This guide walks you through setting up and running the Ai-GRC-Agent using n8n. No Docker setup is required.

---

## Prerequisites

- An n8n account (cloud or self-hosted)
    https://n8n.io

- A Slack workspace with permission to create a bot
    https://slack.com

- An LLM API key (e.g., OpenAI)

---

## Step 1: Access n8n



### n8n Cloud 
1. Go to https://n8n.io
2. Sign up / log in
3. Open your dashboard

---

## Step 2: Import the Workflow

1. Download the Ai-GRC-Agent workflow JSON (from the repository or provided file)

2. In n8n:
   - Click **“Import”** (top right)
   - Select **“Import from File”** or **“Paste JSON”**
   - Upload or paste the workflow

3. The workflow will appear in your workspace

---

## Step 3: Configure Credentials

### 1. Slack Bot Setup

1. Go to https://api.slack.com/apps  
2. Click **“Create New App” → “From Scratch”**  
3. Name your app and select your workspace  

4. Navigate to **OAuth & Permissions** and add the following Bot Token Scopes:
   - `chat:write`
   - `commands`
   - `im:write`
   - `im:read`

5. Install the app to your workspace  

6. Copy the **Bot User OAuth Token**

---

### 2. Add Slack Credentials in n8n

1. In n8n, go to **Credentials**
2. Click **“New Credential”**
3. Select **Slack API**
4. Paste the Bot Token from Slack
5. Save

---

### 3. Configure Slack Trigger (Webhook)

1. Open your workflow in n8n  
2. Click on the **Slack Trigger node**  
3. Copy the **Webhook URL**  

4. In Slack:
   - Go to **Event Subscriptions**
   - Enable events
   - Paste the Webhook URL into **Request URL**

5. Subscribe to events:
   - `app_mention`
   - `message.im`

6. Save changes

---

### 4. LLM API Setup

1. Obtain your API key (e.g., OpenAI)

2. In n8n:
   - Go to **Credentials**
   - Create a new credential (OpenAI or HTTP Request)
   - Paste your API key

3. Attach this credential to the relevant AI/HTTP nodes in the workflow

---

## Step 4: Activate the Workflow

1. Return to your workflow in n8n  
2. Click the **“Activate”** toggle (top right)  

Your workflow is now live and listening for Slack events.

---

## Step 5: Connect Slack Bot to Channel

1. Open Slack  
2. Go to the channel you want to use  
3. Invite the bot:
`/invite @Automated GRC Agent Bot`

---

## Step 6: Run the Agent

In Slack, type:
`@Automated GRC Agent Bot hello`


- You will receive a DM with a form  
- Fill out the requested information  
- Submit the form  

Processing takes about 2–7 minutes

---

## Step 7: Receive Results

The bot will respond with:

- Applicable regulations  
- Compliance gaps  
- Security weaknesses  
- Prioritized recommendations  

---

## Troubleshooting

### Bot not responding
- Ensure the workflow is **activated**
- Verify Slack bot is added to the channel
- Check webhook URL is correct

### Errors in workflow
- Open **Executions** in n8n
- Inspect failed nodes and logs

### No AI response
- Confirm API key is valid
- Check usage limits or billing status

---

## You're Ready

Your Ai-GRC-Agent is now fully set up and accessible through Slack using n8n.