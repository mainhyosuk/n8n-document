[ ](https://github.com/n8n-io/n8n-docs/edit/main/docs/integrations/builtin/core-nodes/n8n-nodes-base.manualworkflowtrigger.md "Edit this page")

# Manual Trigger node[#](#manual-trigger-node "Permanent link")

Use this node if you want to start a workflow by selecting **Test Workflow** and don't want any option for the workflow to run automatically.

Workflows always need a trigger, or start point. Most workflows start with a trigger node firing in response to an external event or the [Schedule Trigger](../n8n-nodes-base.scheduletrigger/) firing on a set schedule.

The Manual Trigger node serves as the workflow trigger for workflows that don't have an automatic trigger.

Use this trigger:

  * To test your workflow before you add an automatic trigger of some kind.
  * When you don't want the workflow to run automatically.



## Common issues[#](#common-issues "Permanent link")

Here are some common errors and issues with the Manual Trigger node and steps to resolve or troubleshoot them.

### Only one 'Manual Trigger' node is allowed in a workflow[#](#only-one-manual-trigger-node-is-allowed-in-a-workflow "Permanent link")

This error displays if you try to add a Manual Trigger node to a workflow which already includes a Manual Trigger node.

Remove your existing Manual Trigger or edit your workflow to connect that trigger to a different node.

Was this page helpful? 

Thanks for your feedback! 

Thanks for your feedback! Help us improve this page by submitting an issue or a fix in our [GitHub repo](https://github.com/n8n-io/n8n-docs). 
