[ ](https://github.com/n8n-io/n8n-docs/edit/main/docs/integrations/builtin/core-nodes/n8n-nodes-base.sort.md "Edit this page")

# Sort[#](#sort "Permanent link")

Use the Sort node to organize lists of items in a desired ordering, or generate a random selection.

Array sort behavior

The Sort operation uses the default JavaScript operation where the elements to be sorted are converted into strings and their values compared. Refer to [Mozilla's guide to Array sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) to learn more.

## Node parameters[#](#node-parameters "Permanent link")

Configure this node using the **Type** parameter.

Use the dropdown to select how you want to input the sorting from these options.

### Simple[#](#simple "Permanent link")

Performs an ascending or descending sort using the selected fields.

When you select this **Type** :

  * Use the **Add Field To Sort By** button to input the **Field Name**.
  * Select whether to use **Ascending** or **Descending** order.



#### Simple options[#](#simple-options "Permanent link")

When you select **Simple** as the **Type** , you have the option to **Disable Dot Notation**. By default, n8n enables dot notation to reference child fields in the format `parent.child`. Use this option to disable dot notation (turned on) or to continue using dot (turned off).

### Random[#](#random "Permanent link")

Creates a random order in the list.

### Code[#](#code "Permanent link")

Input custom JavaScript code to perform the sort operation. This is a good option if a simple sort won't meet your needs.

Enter your custom JavaScript code in the **Code** input field.

## Templates and examples[#](#templates-and-examples "Permanent link")

**Automated Web Scraping: email a CSV, save to Google Sheets & Microsoft Excel**

by Mihai Farcas

[View template details](https://n8n.io/workflows/2275-automated-web-scraping-email-a-csv-save-to-google-sheets-and-microsoft-excel/)

**Transcribing Bank Statements To Markdown Using Gemini Vision AI**

by Jimleuk

[View template details](https://n8n.io/workflows/2421-transcribing-bank-statements-to-markdown-using-gemini-vision-ai/)

**Allow Users to Send a Sequence of Messages to an AI Agent in Telegram**

by Chris Carr

[View template details](https://n8n.io/workflows/2917-allow-users-to-send-a-sequence-of-messages-to-an-ai-agent-in-telegram/)

[Browse Sort integration templates](https://n8n.io/integrations/sort/), or [search all templates](https://n8n.io/workflows/)

## Related resources[#](#related-resources "Permanent link")

Learn more about [data structure and data flow](../../../../data/) in n8n workflows.

Was this page helpful? 

Thanks for your feedback! 

Thanks for your feedback! Help us improve this page by submitting an issue or a fix in our [GitHub repo](https://github.com/n8n-io/n8n-docs). 
