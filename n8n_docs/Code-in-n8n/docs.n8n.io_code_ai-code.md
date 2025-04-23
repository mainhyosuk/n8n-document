[ ](https://github.com/n8n-io/n8n-docs/edit/main/docs/code/ai-code.md "Edit this page")

# AI coding with GPT[#](#ai-coding-with-gpt "Permanent link")

Not available on self-hosted. 

Python isn't supported. ///

## Use AI in the Code node[#](#use-ai-in-the-code-node "Permanent link")

Feature availability

AI assistance in the Code node is available to Cloud users. It isn't available in self-hosted n8n.

AI generated code overwrites your code

If you've already written some code on the **Code** tab, the AI generated code will replace it. n8n recommends using AI as a starting point to create your initial code, then editing it as needed.

To use ChatGPT to generate code in the Code node:

  1. In the Code node, set **Language** to **JavaScript**.
  2. Select the **Ask AI** tab.
  3. Write your query.
  4. Select **Generate Code**. n8n sends your query to ChatGPT, then displays the result in the **Code** tab.



## Usage limits[#](#usage-limits "Permanent link")

During the trial phase there are no usage limits. If n8n makes the feature permanent, there may be usage limits as part of your pricing tier.

## Feature limits[#](#feature-limits "Permanent link")

The ChatGPT implementation in n8n has the following limitations:

  * The AI writes code that manipulates data from the n8n workflow. You can't ask it to pull in data from other sources.
  * The AI doesn't know your data, just the schema, so you need to tell it things like how to find the data you want to extract, or how to check for null.
  * Nodes before the Code node must execute and deliver data to the Code node before you run your AI query.
  * Doesn't work with large incoming data schemas.
  * May have issues if there are a lot of nodes before the code node.



## Writing good prompts[#](#writing-good-prompts "Permanent link")

Writing good prompts increases the chance of getting useful code back.

Some general tips:

  * Provide examples: if possible, give a sample expected output. This helps the AI to better understand the transformation or logic you’re aiming for.
  * Describe the processing steps: if there are specific processing steps or logic that should apply to the data, list them in sequence. For example: "First, filter out all users under 18. Then, sort the remaining users by their last name."
  * Avoid ambiguities: while the AI understands various instructions, being clear and direct ensures you get the most accurate code. Instead of saying "Get the older users," you might say "Filter users who are 60 years and above."
  * Be clear about what you expect as the output. Do you want the data transformed, filtered, aggregated, or sorted? Provide as much detail as possible.



And some n8n-specific guidance:

  * Think about the input data: make sure ChatGPT knows which pieces of the data you want to access, and what the incoming data represents. You may need to tell ChatGPT about the availability of n8n's built-in methods and variables.
  * Declare interactions between nodes: if your logic involves data from multiple nodes, specify how they should interact. "Merge the output of 'Node A' with 'Node B' based on the 'userID' property". if you prefer data to come from certain nodes or to ignore others, be clear: "Only consider data from the 'Purchases' node and ignore the 'Refunds' node."
  * Ensure the output is compatible with n8n. Refer to [Data structure](../../data/data-structure/) for more information on the data structure n8n requires.



### Example prompts[#](#example-prompts "Permanent link")

These examples show a range of possible prompts and tasks.

#### Example 1: Find a piece of data inside a second dataset[#](#example-1-find-a-piece-of-data-inside-a-second-dataset "Permanent link")

To try the example yourself, [download the example workflow](../../_workflows/ai-code/find-a-piece-of-data.json) and import it into n8n.

In the third Code node, enter this prompt:

> The slack data contains only one item. The input data represents all Notion users. Sometimes the person property that holds the email can be null. I want to find the notionId of the Slack user and return it.

Take a look at the code the AI generates.

This is the JavaScript you need:

```
1 2 3 4 5 6 7 8 9
```| ```
`constslackUser=$("Mock Slack").all()[0]; constnotionUsers=$input.all(); constslackUserEmail=slackUser.json.email; constnotionUser=notionUsers.find( (user)=>user.json.person&&user.json.person.email===slackUserEmail ); returnnotionUser?[{json:{notionId:notionUser.json.id}}]:[]; `
```  
---|---  
  
#### Example 2: Data transformation[#](#example-2-data-transformation "Permanent link")

To try the example yourself, [download the example workflow](../../_workflows/ai-code/data-transformation.json) and import it into n8n.

In the **Join items** Code node, enter this prompt:

> Return a single line of text that has all usernames listed with a comma. Each username should be enquoted with a double quotation mark.

Take a look at the code the AI generates.

This is the JavaScript you need:

```
1 2 3 4
```| ```
`constitems=$input.all(); constusernames=items.map((item)=>`"${item.json.username}"`); constresult=usernames.join(", "); return[{json:{usernames:result}}]; `
```  
---|---  
  
#### Example 3: Summarize data and create a Slack message[#](#example-3-summarize-data-and-create-a-slack-message "Permanent link")

To try the example yourself, [download the example workflow](../../_workflows/ai-code/summarize-data.json) and import it into n8n.

In the **Summarize** Code node, enter this prompt:

> Create a markdown text for Slack that counts how many ideas, features and bugs have been submitted. The type of submission is saved in the property_type field. A feature has the property "Feature", a bug has the property "Bug" and an idea has the property "Bug". Also, list the five top submissions by vote in that message. Use "" as markdown for links.

Take a look at the code the AI generates.

This is the JavaScript you need:

```
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40
```| ```
`constsubmissions=$input.all(); // Count the number of ideas, features, and bugs letideaCount=0; letfeatureCount=0; letbugCount=0; submissions.forEach((submission)=>{ switch(submission.json.property_type[0]){ case"Idea": ideaCount++; break; case"Feature": featureCount++; break; case"Bug": bugCount++; break; } }); // Sort submissions by votes and take the top 5 consttopSubmissions=submissions .sort((a,b)=>b.json.property_votes-a.json.property_votes) .slice(0,5); lettopSubmissionText=""; topSubmissions.forEach((submission)=>{ topSubmissionText+=`<${submission.json.url}|${submission.json.name}> with ${submission.json.property_votes} votes\n`; }); // Construct the Slack message constslackMessage=`*Summary of Submissions*\n Ideas: ${ideaCount}\n Features: ${featureCount}\n Bugs: ${bugCount}\n Top 5 Submissions:\n ${topSubmissionText}`; return[{json:{slackMessage}}]; `
```  
---|---  
  
### Reference incoming node data explicitly[#](#reference-incoming-node-data-explicitly "Permanent link")

If your incoming data contains nested fields, using dot notation to reference them can help the AI understand what data you want.

[!["Screenshot of an n8n code node, highlighting how to reference data with dot notation in an AI query"](../../_images/code/ai-code/reference-data-dot-notation.png)](https://docs.n8n.io/_images/code/ai-code/reference-data-dot-notation.png)

To try the example yourself, [download the example workflow](../../_workflows/ai-code/reference-incoming-data-explicitly.json) and import it into n8n.

In the second Code node, enter this prompt:

> The data in "Mock data" represents a list of people. For each person, return a new item containing personal_info.first_name and work_info.job_title.

This is the JavaScript you need:

```
1 2 3 4 5 6 7 8 9 10 11 12
```| ```
`constitems=$input.all(); constnewItems=items.map((item)=>{ constfirstName=item.json.personal_info.first_name; constjobTitle=item.json.work_info.job_title; return{ json:{ firstName, jobTitle, }, }; }); returnnewItems; `
```  
---|---  
  
### Related resources[#](#related-resources "Permanent link")

Pluralsight offer a short guide on [How to use ChatGPT to write code](https://www.pluralsight.com/blog/software-development/how-use-chatgpt-programming-coding), which includes example prompts.

## Fixing the code[#](#fixing-the-code "Permanent link")

The AI-generated code may work without any changes, but you may have to edit it. You need to be aware of n8n's [Data structure](../../data/data-structure/). You may also find n8n's built-in methods and variables useful.

Was this page helpful? 

Thanks for your feedback! 

Thanks for your feedback! Help us improve this page by submitting an issue or a fix in our [GitHub repo](https://github.com/n8n-io/n8n-docs). 
