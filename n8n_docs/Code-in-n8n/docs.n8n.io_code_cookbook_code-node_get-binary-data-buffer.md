[ ](https://github.com/n8n-io/n8n-docs/edit/main/docs/code/cookbook/code-node/get-binary-data-buffer.md "Edit this page")

# Get the binary data buffer[#](#get-the-binary-data-buffer "Permanent link")

The binary data buffer contains all the binary file data processed by a workflow. You need to access it if you want to perform operations on the binary data, such as:

  * Manipulating the data: for example, adding column headers to a CSV file.
  * Using the data in calculations: for example, calculating a hash value based on it.
  * Complex HTTP requests: for example, combining file upload with sending other data formats.



Not available in Python

`getBinaryDataBuffer()` isn't supported when using Python.

You can access the buffer using n8n's `getBinaryDataBuffer()` function:

```
1 2 3 4 5 6
```| ```
`/*  * itemIndex: number. The index of the item in the input data. * binaryPropertyName: string. The name of the binary property.  * The default in the Read/Write File From Disk node is 'data'.  */ letbinaryDataBufferItem=awaitthis.helpers.getBinaryDataBuffer(itemIndex,binaryPropertyName); `
```  
---|---  
  
For example:

```
1 2
```| ```
`letbinaryDataBufferItem=awaitthis.helpers.getBinaryDataBuffer(0,'data'); // Returns the data in the binary buffer for the first input item `
```  
---|---  
  
You should always use the `getBinaryDataBuffer()` function, and avoid using older methods of directly accessing the buffer, such as targeting it with expressions like `items[0].binary.data.data`.

Was this page helpful? 

Thanks for your feedback! 

Thanks for your feedback! Help us improve this page by submitting an issue or a fix in our [GitHub repo](https://github.com/n8n-io/n8n-docs). 
