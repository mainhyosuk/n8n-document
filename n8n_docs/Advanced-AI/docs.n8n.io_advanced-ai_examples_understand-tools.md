[ ](https://github.com/n8n-io/n8n-docs/edit/main/docs/advanced-ai/examples/understand-tools.md "Edit this page")

# What's a tool in AI?[#](#whats-a-tool-in-ai "Permanent link")

In AI, 'tools' has a specific meaning. Tools act like addons that your AI can use to access extra context or resources.

Here are a couple of other ways of expressing it:

> Tools are interfaces that an agent can use to interact with the world ([source](https://langchain-ai.github.io/langgraphjs/how-tos/tool-calling/))

> We can think of these tools as being almost like functions that your AI model can call ([source](https://www.udemy.com/course/chatgpt-and-langchain-the-complete-developers-masterclass/))

## AI tools in n8n[#](#ai-tools-in-n8n "Permanent link")

n8n provides tool [sub-nodes](../../../glossary/#sub-node-n8n) that you can connect to your [AI agent](../../../glossary/#ai-agent). As well as providing some popular tools, such as [Wikipedia](../../../integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolwikipedia/) and [SerpAPI](../../../integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolserpapi/), n8n provides three especially powerful tools:

  * [Call n8n Workflow Tool](../../../integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolworkflow/): use this to load any n8n workflow as a tool.
  * [Custom Code Tool](../../../integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolcode/): write code that your agent can run.
  * [HTTP Request Tool](../../../integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolhttprequest/): make calls to fetch a website or data from an API.



The next three examples highlight the Call n8n Workflow Tool:

  * [Chat with Google Sheets](../data-google-sheets/)
  * [Call an API to fetch data](../api-workflow-tool/)
  * [Set up a human fallback](../human-fallback/)



You can also learn how to [let AI dynamically specify parameters for tools with the `$fromAI()` function](../using-the-fromai-function/).

Was this page helpful? 

Thanks for your feedback! 

Thanks for your feedback! Help us improve this page by submitting an issue or a fix in our [GitHub repo](https://github.com/n8n-io/n8n-docs). 
