[ ](https://github.com/n8n-io/n8n-docs/edit/main/docs/code/expressions.md "Edit this page")

# Expressions[#](#expressions "Permanent link")

Expressions are a powerful feature implemented in all n8n nodes. They allow node parameters to be set dynamically based on data from:

  * Previous node executions
  * The workflow
  * Your n8n environment



You can also execute JavaScript within an expression, making this a convenient and easy way to manipulate data into useful parameter values without writing extensive extra code.

n8n created and uses a templating language called [Tournament](https://github.com/n8n-io/tournament), and extends it with [custom methods and variables](../builtin/overview/) and [data transformation functions](../builtin/data-transformation-functions/). These features make it easier to perform common tasks like getting data from other nodes or accessing workflow metadata.

n8n additionally supports two libraries:

  * [Luxon](https://github.com/moment/luxon/), for working with dates and time.
  * [JMESPath](https://jmespath.org/), for querying JSON.



Data in n8n

When writing expressions, it's helpful to understand data structure and behavior in n8n. Refer to [Data](../../data/) for more information on working with data in your workflows.

## Writing expressions[#](#writing-expressions "Permanent link")

To use an expression to set a parameter value:

  1. Hover over the parameter where you want to use an expression.
  2. Select **Expressions** in the **Fixed/Expression** toggle.
  3. Write your expression in the parameter, or select **Open expression editor** ![Open expressions editor icon](../../_images/common-icons/open-expression-editor.png) to open the expressions editor. If you use the expressions editor, you can browse the available data in the **Variable selector**. All expressions have the format `{{ your expression here }}`.



### Example: Get data from webhook body[#](#example-get-data-from-webhook-body "Permanent link")

Consider the following scenario: you have a webhook trigger that receives data through the webhook body. You want to extract some of that data for use in the workflow.

Your webhook data looks similar to this:

```
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
```| ```
`[ { "headers":{ "host":"n8n.instance.address", ... }, "params":{}, "query":{}, "body":{ "name":"Jim", "age":30, "city":"New York" } } ] `
```  
---|---  
  
In the next node in the workflow, you want to get just the value of `city`. You can use the following expression:

```
1
```| ```
`{{$json.body.city}} `
```  
---|---  
  
This expression:

  1. Accesses the incoming JSON-formatted data using n8n's custom `$json` variable.
  2. Finds the value of `city` (in this example, "New York"). Note that this example uses JMESPath syntax to query the JSON data. You can also write this expression as `{{$json['body']['city']}}`.



### Example: Writing longer JavaScript[#](#example-writing-longer-javascript "Permanent link")

An expression contains one line of JavaScript. This means you cannot do things like variable assignments or multiple standalone operations.

To understand the limitations of JavaScript in expressions, and start thinking about workarounds, look at the following two pieces of code. Both code examples use the Luxon date and time library to find the time between two dates in months, and encloses the code in handlebar brackets, like an expression.

However, the first example isn't a valid n8n expression:

```
1 2 3 4 5 6 7 8 9 10 11
```| ```
`// This example is split over multiple lines for readability // It's still invalid when formatted as a single line {{ functionexample(){ letend=DateTime.fromISO('2017-03-13'); letstart=DateTime.fromISO('2017-02-13'); letdiffInMonths=end.diff(start,'months'); returndiffInMonths.toObject(); } example(); }} `
```  
---|---  
  
While the second example is valid:

```
1
```| ```
`{{DateTime.fromISO('2017-03-13').diff(DateTime.fromISO('2017-02-13'),'months').toObject()}} `
```  
---|---  
  
## Common issues[#](#common-issues "Permanent link")

For common errors or issues with expressions and suggested resolution steps, refer to [Common Issues](../cookbook/expressions/common-issues/).

Was this page helpful? 

Thanks for your feedback! 

Thanks for your feedback! Help us improve this page by submitting an issue or a fix in our [GitHub repo](https://github.com/n8n-io/n8n-docs). 
