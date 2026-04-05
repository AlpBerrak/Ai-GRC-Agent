## AI Agent Documentation
This documentation goes through the logic used in our AI Agent for risk assessment, including the tools used for getting user input, formatting user input, and running the analysis. This project uses n8n to create the workflow, and Slack as the chat interface.
### Receiving User Input
This workflow uses Slack as its chat interface. We’ve created a channel in our Slack with a bot that can be called to execute the AI Agent. From this chat, we use webhooks in order to get the user input from Slack to serve as the initial chat input for the AI Agent to work from. Additionally, when more information needs to be requested, a webhook is sent back to the Slack channel, prompting the user to provide additional information, then the process of running analysis can begin.
### Information Extractor
The information extractor node uses OpenAI as its model in order to extract the information necessary for analysis from user input. It will then format the user input into a JSON that follows into nodes that confirm if all information has been obtained. The formatting is crucial for the workflow as it makes the information easily readable and appendable by different nodes in the workflow.
### Updating Information
After extracting information from the initial user input, the output of the information extractor goes to an if node that will check to determine if the location and the sector have been obtained. If all information is present, it moves directly onto the AI Agent. If information is missing, the output moves onto a switch where the location, sector, or both can be prompted by the AI Agent to the user in the Slack channel. This input will then go back through the information extractor in order to update the JSON properly and can then move onto the AI Agent body. After more information has been obtained, the data from the two branches will merge to have the full JSON of data for analysis.

## Tools of the AI Agent
The following is descriptions of the tools the AI Agent can call on to perform different functions. The AI Agent is trained to know that it needs to call tools in order to perform its functions, and can appropriately determine when calling particular tools is necessary.

### Vector Stores
The vector stores which are loaded using a RAG, are used by the AI to call on the JSONs created of regulations and recommendations when applicable. Each vector store contains a different subset of regulations and recommendations so that the AI Agent doesn't have to parse through information it does not need. The vector stores are divided as follows: US State Regulations, US Federal Regulations, International Regulations, NIST Recommendations, NIST Control Enhancements, and SOX Recommendations.

### US Subflow
The US Subflow is called when the organization is located in the US. This subflow asks the user for the states the orgnazation operates in and the number of users it collects data on excluding soley transactional data. This information is only needed when the organization is located in the US, therefore only called when the AI Agent recognizes that the US is in the list of locations. This information will be added to the JSON given to the AI Agent for proper analysis.

### Check Sector Subflow
This subflow is a guardrail for organizations in sectors that are not related to business or finance because it is out of scope for this AI Agent. The AI Agent will call this tool when the sector value in the input JSON is not business, finance, investment banking, banking, or financial advising. It will then send a message to the user that analysis cannot be run on it's system configurations because it is out of scope for the Agent.
