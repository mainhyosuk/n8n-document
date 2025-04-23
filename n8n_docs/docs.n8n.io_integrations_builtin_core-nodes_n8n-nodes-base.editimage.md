[ ](https://github.com/n8n-io/n8n-docs/edit/main/docs/integrations/builtin/core-nodes/n8n-nodes-base.editimage.md "Edit this page")

# Edit Image[#](#edit-image "Permanent link")

Use the Edit Image node to manipulate and edit images.

Dependencies

  1. If you aren't running n8n on Docker, you need to install [GraphicsMagick](http://www.graphicsmagick.org/README.html).
  2. You need to use a node such as the [Read/Write Files from Disk](../n8n-nodes-base.readwritefile/) node or the [HTTP Request](../n8n-nodes-base.httprequest/) node to pass the image file as a data property to the Edit Image node.



## Operations[#](#operations "Permanent link")

  * Add a **Blur** to the image to reduce sharpness
  * Add a **Border** to the image
  * **Composite** an image on top of another image
  * **Create** a new image
  * **Crop** the image
  * **Draw** on an image
  * **Get Information** about the image
  * **Multi Step** perform multiple operations on the image
  * **Resize** : Change the size of the image
  * **Rotate** the image
  * **Shear** image along the X or Y axis
  * Add **Text** to the image
  * Make a color in image **Transparent**



## Node parameters[#](#node-parameters "Permanent link")

The parameters for this node depend on the operation you select.

### Blur parameters[#](#blur-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Blur** : Enter a number to set how strong the blur should be, between 0 and 1000. Higher numbers create blurrier images.
  * **Sigma** : Enter a number to set the stigma for the blur, between 0 and 1000. Higher numbers create blurrier images.



Refer to [Node options](#node-options) for optional configuration options.

### Border parameters[#](#border-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Border Width** : Enter the width of the border.
  * **Border Height** : Enter the height of the border.
  * **Border Color** : Set the color for the border. You can either enter a hex or select the color swatch to open a color picker.



Refer to [Node options](#node-options) for optional configuration options.

### Composite parameters[#](#composite-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data. This image is your base image.
  * **Composite Image Property** : Enter the name of the binary property that stores image to composite on top of the **Property Name** image.
  * **Operator** : Select composite operator, which determines how the composite works. Options include:
    * **Add**
    * **Atop**
    * **Bumpmap**
    * **Copy**
    * **Copy Black**
    * **Copy Blue**
    * **Copy Cyan**
    * **Copy Green**
    * **Copy Magenta**
    * **Copy Opacity**
    * **Copy Red**
    * **Copy Yellow**
    * **Difference**
    * **Divide**
    * **In**
    * **Minus**
    * **Multiply**
    * **Out**
    * **Over**
    * **Plus**
    * **Subtract**
    * **Xor**
  * **Position X** : Enter the x axis position (horizontal) of the composite image.
  * **Position Y** : Enter the y axis position (vertical) of the composite image.



Refer to [Node options](#node-options) for optional configuration options.

### Create parameters[#](#create-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Background Color** : Set the background color for the image. You can either enter a hex or select the color swatch to open a color picker.
  * **Image Width** : Enter the width of the image.
  * **Image Height** : Enter the height of the image.



Refer to [Node options](#node-options) for optional configuration options.

### Crop parameters[#](#crop-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Width** : Enter the width you'd like to crop to.
  * **Height** : Enter the height you'd like to crop to.
  * **Position X** : Enter the x axis position (horizontal) to start the crop from.
  * **Position Y** : Enter the y axis position (vertical) to start the crop from.



Refer to [Node options](#node-options) for optional configuration options.

### Draw parameters[#](#draw-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Primitive** : Select the primitive shape to draw. Choose from:
    * **Circle**
    * **Line**
    * **Rectangle**
  * **Color** : Set the color for the primitive. You can either enter a hex or select the color swatch to open a color picker.
  * **Start Position X** : Enter the x axis position (horizontal) to start drawing from.
  * **Start Position Y** : Enter the y axis position (vertical) to start drawing from.
  * **End Position X** : Enter the x axis position (horizontal) to stop drawing at.
  * **End Position Y** : Enter the y axis position (vertical) to start drawing at.
  * **Corner Radius** : Enter a number to set the corner radius. Adding a corner radius will round the corners of the drawn primitive.



Refer to [Node options](#node-options) for optional configuration options.

### Get Information parameters[#](#get-information-parameters "Permanent link")

For this operation, you only need to add the **Property Name** of the binary property that stores the image data.

Refer to [Node options](#node-options) for optional configuration options.

### Multi Step parameters[#](#multi-step-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Operations** : Add the operations you want the multi step operation to perform. You can use any of the other operations.



Refer to [Node options](#node-options) for optional configuration options.

### Resize parameters[#](#resize-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Width** : Enter the new width you'd like for the image.
  * **Height** : Enter the new height you'd like for the image.
  * **Option** : Select how you'd like to resize the image. Choose from:
    * **Ignore Aspect Ratio** : Ignore the aspect ratio and resize to the exact height and width you've entered.
    * **Maximum Area** : The height and width you've entered is the maximum area/size for the image. The image maintains its aspect ratio and won't be larger than the height and/or width you've entered.
    * **Minimum Area** : The height and width you've entered is the minimum area/size for the image. The image maintains its aspect ratio and won't be smaller than the height and/or width you've entered.
    * **Only if Larger** : Resize the image only if it's larger than the width and height you entered. The image maintains its aspect ratio.
    * **Only if Smaller** : Resize the image only if it's smaller than the width and height you entered. The image maintains its aspect ratio.
    * **Percent** : Resize the image using the width and height as percentages of the original image.



Refer to [Node options](#node-options) for optional configuration options.

### Rotate parameters[#](#rotate-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Rotate** : Enter the number of degrees to rotate the image, from --360 to 360.
  * **Background Color** : Set the background color for the image. You can either enter a hex or select the color swatch to open a color picker. This color is used to fill in the empty background whenever the image is rotated by multiples of 90 degrees. If multipled of 90 degrees are used for the **Rotate** field, the background color isn't used.



Refer to [Node options](#node-options) for optional configuration options.

### Shear parameters[#](#shear-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Degrees X** : Enter the number of degrees to shear from the x axis.
  * **Degrees Y** : Enter the number of degrees to shear from the y axis.



Refer to [Node options](#node-options) for optional configuration options.

### Text parameters[#](#text-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Text** : Enter the text you'd like to write on the image.
  * **Font Size** : Select the font size for the text.
  * **Font Color** : Set the font color. You can either enter a hex or select the color swatch to open a color picker.
  * **Position X** : Enter the x axis position (horizontal) to begin the text at.
  * **Position Y** : Enter the y axis position (vertical) to begin the text at.
  * **Max Line Length** : Enter the maximum amount of characters in a line before adding a line break.



Refer to [Node options](#node-options) for optional configuration options.

### Transparent parameters[#](#transparent-parameters "Permanent link")

  * **Property Name** : Enter the name of the binary property that stores the image data.
  * **Color** : Set the color to make transparent. You can either enter a hex or select the color swatch to open a color picker.



Refer to [Node options](#node-options) for optional configuration options.

## Node options[#](#node-options "Permanent link")

  * **File Name** : Enter the filename of the output file.
  * **Format** : Enter the image format of the output file. Choose from:
    * **bmp**
    * **gif**
    * **jpeg**
    * **png**
    * **tiff**
    * **WebP**



The **Text** operation also includes the option for **Font Name or ID**. Select the text font from the dropdown or specify an ID using an [expression](../../../../code/expressions/).

## Templates and examples[#](#templates-and-examples "Permanent link")

**Flux AI Image Generator**

by Max Tkacz

[View template details](https://n8n.io/workflows/2417-flux-ai-image-generator/)

**Generate Instagram Content from Top Trends with AI Image Generation**

by mustafa kendigüzel

[View template details](https://n8n.io/workflows/2803-generate-instagram-content-from-top-trends-with-ai-image-generation/)

**Automate Image Validation Tasks using AI Vision**

by Jimleuk

[View template details](https://n8n.io/workflows/2420-automate-image-validation-tasks-using-ai-vision/)

[Browse Edit Image integration templates](https://n8n.io/integrations/edit-image/), or [search all templates](https://n8n.io/workflows/)

Was this page helpful? 

Thanks for your feedback! 

Thanks for your feedback! Help us improve this page by submitting an issue or a fix in our [GitHub repo](https://github.com/n8n-io/n8n-docs). 
