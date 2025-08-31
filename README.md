# Pixeldisplays
Repository for the **Pixeldisplays Diamondfire library**.

---

## Pipeline
To start the pipeline, you can either generate image data on the fly, keeping separate lists to hold the **R**, **G**, **B**, and (optional) **alpha (A)** values for each display (4 displays per image).  

After generating the R, G, B, and A lists, you must first **interlace** them using the `Interlace RGB` function. This transforms a single list of values (for example, R values) into 4 separate lists, each corresponding to the 4 text displays for the next step.  

Once the lists are interlaced, use the `RGBToTextList` function to parse the raw values for each text display into a **text list**. Note: the width and height provided to this function must be halved because the 3 large value lists were divided into 12 smaller lists during interlacing.

You can also load image data and parse it directly into a text list using the `LoadImages` function. To do this:  

- Define a function named `PixelDisplays.Img.<image name>` with a `CreateList` action and a local variable inside.  
- The list must contain the following **18 arguments in order**:  
  1. R values (1-4)  
  2. G values (1-4)  
  3. B values (1-4)  
  4. A values (1-4)  
  5. Width and height (in pixels) of the image  

All R, G, B, and A values are numbers in a **comma-separated list within a string**. A values can also be either `true` or `false`, with `true` equal to 1.  

Once processed, the image data is stored in **5 global variables**:  
- 4 variables containing the text lists: `Img.<image name>.TextList[1-4]`  
- 1 variable containing metadata: `Img.<image name>.Meta` (width and height of the image)  

Additionally, all loaded image names are stored in a global list called `LoadedImages` for easy access.

---

## Spawning Pixeldisplays
With parsed data from the previous section, you can spawn Pixeldisplays using the `CreateInterlaced` function. This function returns the **UUIDs of the text displays** and requires, among other arguments, the 4 text lists.  

Once the Pixeldisplay is spawned, you can update it to create animations or other effects using the `UpdateInterlaced` function.

