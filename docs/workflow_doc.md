## AI Agent Documentation
This documentation goes through the logic used in our AI Agent for risk assessment, including the tools used for getting user input, formatting user input, and running the analysis. This project uses n8n to create the workflow, and Slack as the chat interface.
### Receiving User Input
This workflow uses Slack as its chat interface. We’ve created a channel in our Slack with a bot that can be called to execute the AI Agent. From this chat, we use webhooks in order to get the user input from Slack to serve as the initial chat input for the AI Agent to work from. Additionally, when more information needs to be requested, a webhook is sent back to the Slack channel, prompting the user to provide additional information, then the process of running analysis can begin.
### Information Extractor
The information extractor node uses OpenAI as its model in order to extract the information necessary for analysis from user input. It will then format the user input into a JSON that follows into nodes that confirm if all information has been obtained. The formatting is crucial for the workflow as it makes the information easily readable and appendable by different nodes in the workflow.
### Updating Information
After extracting information from the initial user input, the output of the information extractor goes to an if node that will check to determine if the location and the sector have been obtained. If all information is present, it moves directly onto the AI Agent. If information is missing, the output moves onto a switch where the location, sector, or both can be prompted by the AI Agent to the user in the Slack channel. This input will then go back through the information extractor in order to update the JSON properly and can then move onto the AI Agent body.

## Tools of the AI Agent
The following is descriptions of the tools the AI Agent can call on to perform different functions. The AI Agent is trained to know that it needs to call tools in order to perform its functions, and can appropriately determine when calling particular tools is necessary.
